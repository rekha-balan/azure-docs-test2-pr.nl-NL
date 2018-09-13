---
title: Starting an Azure Automation runbook with a webhook | Microsoft Docs
description: A webhook that allows a client to start a runbook in Azure Automation from an HTTP call.  This article describes how to create a webhook and how to call one to start a runbook.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: df37011ec35ffcffc00768093e6f5b165bad3d5d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551141"
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="3ca61-104">Starting an Azure Automation runbook with a webhook</span><span class="sxs-lookup"><span data-stu-id="3ca61-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="3ca61-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="3ca61-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span><span class="sxs-lookup"><span data-stu-id="3ca61-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="3ca61-107">![WebhooksOverview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="3ca61-107">![WebhooksOverview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="3ca61-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="3ca61-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="3ca61-109">Details of a webhook</span><span class="sxs-lookup"><span data-stu-id="3ca61-109">Details of a webhook</span></span>
<span data-ttu-id="3ca61-110">The following table describes the properties that you must configure for a webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="3ca61-111">Property</span><span class="sxs-lookup"><span data-stu-id="3ca61-111">Property</span></span> | <span data-ttu-id="3ca61-112">Description</span><span class="sxs-lookup"><span data-stu-id="3ca61-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3ca61-113">Name</span><span class="sxs-lookup"><span data-stu-id="3ca61-113">Name</span></span> |<span data-ttu-id="3ca61-114">You can provide any name you want for a webhook since this is not exposed to the client.</span><span class="sxs-lookup"><span data-stu-id="3ca61-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="3ca61-115">It is only used for you to identify the runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3ca61-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="3ca61-116">As a best practice, you should give the webhook a name related to the client that will use it.</span><span class="sxs-lookup"><span data-stu-id="3ca61-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="3ca61-117">URL</span><span class="sxs-lookup"><span data-stu-id="3ca61-117">URL</span></span> |<span data-ttu-id="3ca61-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="3ca61-119">It is automatically generated when you create the webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="3ca61-120">You cannot specify a custom URL.</span><span class="sxs-lookup"><span data-stu-id="3ca61-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="3ca61-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span><span class="sxs-lookup"><span data-stu-id="3ca61-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="3ca61-122">For this reason, it should be treated like a password.</span><span class="sxs-lookup"><span data-stu-id="3ca61-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="3ca61-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span><span class="sxs-lookup"><span data-stu-id="3ca61-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="3ca61-124">You should note the URL in a secure location for future use.</span><span class="sxs-lookup"><span data-stu-id="3ca61-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="3ca61-125">Expiration date</span><span class="sxs-lookup"><span data-stu-id="3ca61-125">Expiration date</span></span> |<span data-ttu-id="3ca61-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span><span class="sxs-lookup"><span data-stu-id="3ca61-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="3ca61-127">This expiration date can be modified after the webhook is created.</span><span class="sxs-lookup"><span data-stu-id="3ca61-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="3ca61-128">Enabled</span><span class="sxs-lookup"><span data-stu-id="3ca61-128">Enabled</span></span> |<span data-ttu-id="3ca61-129">A webhook is enabled by default when it is created.</span><span class="sxs-lookup"><span data-stu-id="3ca61-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="3ca61-130">If you set it to Disabled, then no client will be able to use it.</span><span class="sxs-lookup"><span data-stu-id="3ca61-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="3ca61-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span><span class="sxs-lookup"><span data-stu-id="3ca61-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="3ca61-132">Parameters</span><span class="sxs-lookup"><span data-stu-id="3ca61-132">Parameters</span></span>
<span data-ttu-id="3ca61-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="3ca61-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span><span class="sxs-lookup"><span data-stu-id="3ca61-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="3ca61-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="3ca61-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span><span class="sxs-lookup"><span data-stu-id="3ca61-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="3ca61-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="3ca61-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Webhookdata properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="3ca61-140">The **$WebhookData** object will have the following properties:</span><span class="sxs-lookup"><span data-stu-id="3ca61-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="3ca61-141">Property</span><span class="sxs-lookup"><span data-stu-id="3ca61-141">Property</span></span> | <span data-ttu-id="3ca61-142">Description</span><span class="sxs-lookup"><span data-stu-id="3ca61-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3ca61-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="3ca61-143">WebhookName</span></span> |<span data-ttu-id="3ca61-144">The name of the webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-144">The name of the webhook.</span></span> |
| <span data-ttu-id="3ca61-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="3ca61-145">RequestHeader</span></span> |<span data-ttu-id="3ca61-146">Hash table containing the headers of the incoming POST request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="3ca61-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="3ca61-147">RequestBody</span></span> |<span data-ttu-id="3ca61-148">The body of the incoming POST request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="3ca61-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span><span class="sxs-lookup"><span data-stu-id="3ca61-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="3ca61-150">The runbook must be written to work with the data format that is expected.</span><span class="sxs-lookup"><span data-stu-id="3ca61-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="3ca61-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span><span class="sxs-lookup"><span data-stu-id="3ca61-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="3ca61-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span><span class="sxs-lookup"><span data-stu-id="3ca61-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="3ca61-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span><span class="sxs-lookup"><span data-stu-id="3ca61-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="3ca61-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="3ca61-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="3ca61-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span><span class="sxs-lookup"><span data-stu-id="3ca61-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![WebhookData parameter from UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="3ca61-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span><span class="sxs-lookup"><span data-stu-id="3ca61-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="3ca61-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="3ca61-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="3ca61-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="3ca61-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="3ca61-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="3ca61-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="3ca61-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span><span class="sxs-lookup"><span data-stu-id="3ca61-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="3ca61-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="3ca61-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Start WebhookData parameter from UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="3ca61-165">The values of all input parameters are logged with the runbook job.</span><span class="sxs-lookup"><span data-stu-id="3ca61-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="3ca61-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span><span class="sxs-lookup"><span data-stu-id="3ca61-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="3ca61-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span><span class="sxs-lookup"><span data-stu-id="3ca61-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="3ca61-168">Security</span><span class="sxs-lookup"><span data-stu-id="3ca61-168">Security</span></span>
<span data-ttu-id="3ca61-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span><span class="sxs-lookup"><span data-stu-id="3ca61-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="3ca61-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span><span class="sxs-lookup"><span data-stu-id="3ca61-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="3ca61-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="3ca61-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span><span class="sxs-lookup"><span data-stu-id="3ca61-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="3ca61-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span><span class="sxs-lookup"><span data-stu-id="3ca61-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="3ca61-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="3ca61-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="3ca61-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="3ca61-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span><span class="sxs-lookup"><span data-stu-id="3ca61-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="3ca61-177">Creating a webhook</span><span class="sxs-lookup"><span data-stu-id="3ca61-177">Creating a webhook</span></span>
<span data-ttu-id="3ca61-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3ca61-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="3ca61-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span><span class="sxs-lookup"><span data-stu-id="3ca61-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="3ca61-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span><span class="sxs-lookup"><span data-stu-id="3ca61-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br>
   <span data-ttu-id="3ca61-181">![Webhooks button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="3ca61-181">![Webhooks button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="3ca61-182">Click **Create new webhook** to open the **Create webhook blade**.</span><span class="sxs-lookup"><span data-stu-id="3ca61-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="3ca61-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span><span class="sxs-lookup"><span data-stu-id="3ca61-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="3ca61-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span><span class="sxs-lookup"><span data-stu-id="3ca61-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="3ca61-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="3ca61-186">Then record it in a safe place.</span><span class="sxs-lookup"><span data-stu-id="3ca61-186">Then record it in a safe place.</span></span>  <span data-ttu-id="3ca61-187">**Once you create the webhook, you cannot retrieve the URL again.**</span><span class="sxs-lookup"><span data-stu-id="3ca61-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br>
   <span data-ttu-id="3ca61-188">![Webhook URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="3ca61-188">![Webhook URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="3ca61-189">Click **Parameters** to provide values for the runbook parameters.</span><span class="sxs-lookup"><span data-stu-id="3ca61-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="3ca61-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span><span class="sxs-lookup"><span data-stu-id="3ca61-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="3ca61-191">Click **Create** to create the webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="3ca61-192">Using a webhook</span><span class="sxs-lookup"><span data-stu-id="3ca61-192">Using a webhook</span></span>
<span data-ttu-id="3ca61-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="3ca61-194">The syntax of the webhook will be in the following format.</span><span class="sxs-lookup"><span data-stu-id="3ca61-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="3ca61-195">The client will receive one of the following return codes from the POST request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="3ca61-196">Code</span><span class="sxs-lookup"><span data-stu-id="3ca61-196">Code</span></span> | <span data-ttu-id="3ca61-197">Text</span><span class="sxs-lookup"><span data-stu-id="3ca61-197">Text</span></span> | <span data-ttu-id="3ca61-198">Description</span><span class="sxs-lookup"><span data-stu-id="3ca61-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3ca61-199">202</span><span class="sxs-lookup"><span data-stu-id="3ca61-199">202</span></span> |<span data-ttu-id="3ca61-200">Accepted</span><span class="sxs-lookup"><span data-stu-id="3ca61-200">Accepted</span></span> |<span data-ttu-id="3ca61-201">The request was accepted, and the runbook was successfully queued.</span><span class="sxs-lookup"><span data-stu-id="3ca61-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="3ca61-202">400</span><span class="sxs-lookup"><span data-stu-id="3ca61-202">400</span></span> |<span data-ttu-id="3ca61-203">Bad Request</span><span class="sxs-lookup"><span data-stu-id="3ca61-203">Bad Request</span></span> |<span data-ttu-id="3ca61-204">The request was not accepted for one of the following reasons.</span><span class="sxs-lookup"><span data-stu-id="3ca61-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="3ca61-205">The webhook has expired.</span><span class="sxs-lookup"><span data-stu-id="3ca61-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="3ca61-206">The webhook is disabled.</span><span class="sxs-lookup"><span data-stu-id="3ca61-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="3ca61-207">The token in the URL is invalid.</span><span class="sxs-lookup"><span data-stu-id="3ca61-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="3ca61-208">404</span><span class="sxs-lookup"><span data-stu-id="3ca61-208">404</span></span> |<span data-ttu-id="3ca61-209">Not Found</span><span class="sxs-lookup"><span data-stu-id="3ca61-209">Not Found</span></span> |<span data-ttu-id="3ca61-210">The request was not accepted for one of the following reasons.</span><span class="sxs-lookup"><span data-stu-id="3ca61-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="3ca61-211">The webhook was not found.</span><span class="sxs-lookup"><span data-stu-id="3ca61-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="3ca61-212">The runbook was not found.</span><span class="sxs-lookup"><span data-stu-id="3ca61-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="3ca61-213">The account was not found.</span><span class="sxs-lookup"><span data-stu-id="3ca61-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="3ca61-214">500</span><span class="sxs-lookup"><span data-stu-id="3ca61-214">500</span></span> |<span data-ttu-id="3ca61-215">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="3ca61-215">Internal Server Error</span></span> |<span data-ttu-id="3ca61-216">The URL was valid, but an error occurred.</span><span class="sxs-lookup"><span data-stu-id="3ca61-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="3ca61-217">Please resubmit the request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-217">Please resubmit the request.</span></span> |

<span data-ttu-id="3ca61-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span><span class="sxs-lookup"><span data-stu-id="3ca61-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="3ca61-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span><span class="sxs-lookup"><span data-stu-id="3ca61-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="3ca61-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="3ca61-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ca61-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="3ca61-222">Example</span><span class="sxs-lookup"><span data-stu-id="3ca61-222">Example</span></span>
<span data-ttu-id="3ca61-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="3ca61-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span><span class="sxs-lookup"><span data-stu-id="3ca61-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="3ca61-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="3ca61-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="3ca61-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="3ca61-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span><span class="sxs-lookup"><span data-stu-id="3ca61-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="3ca61-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="3ca61-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Webhooks button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="3ca61-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="3ca61-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="3ca61-232">This is formatted as JSON because that was the format that was included in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="3ca61-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Webhooks button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="3ca61-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span><span class="sxs-lookup"><span data-stu-id="3ca61-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="3ca61-235">The job id is extracted from the response and converted to a string.</span><span class="sxs-lookup"><span data-stu-id="3ca61-235">The job id is extracted from the response and converted to a string.</span></span>

![Webhooks button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="3ca61-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span><span class="sxs-lookup"><span data-stu-id="3ca61-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate to Azure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="3ca61-238">Starting runbooks in response to Azure alerts</span><span class="sxs-lookup"><span data-stu-id="3ca61-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="3ca61-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3ca61-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="3ca61-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span><span class="sxs-lookup"><span data-stu-id="3ca61-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="3ca61-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span><span class="sxs-lookup"><span data-stu-id="3ca61-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="3ca61-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3ca61-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="3ca61-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span><span class="sxs-lookup"><span data-stu-id="3ca61-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="3ca61-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span><span class="sxs-lookup"><span data-stu-id="3ca61-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="3ca61-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![Webhooks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="3ca61-247">Alert context</span><span class="sxs-lookup"><span data-stu-id="3ca61-247">Alert context</span></span>
<span data-ttu-id="3ca61-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span><span class="sxs-lookup"><span data-stu-id="3ca61-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="3ca61-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span><span class="sxs-lookup"><span data-stu-id="3ca61-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="3ca61-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span><span class="sxs-lookup"><span data-stu-id="3ca61-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="3ca61-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span><span class="sxs-lookup"><span data-stu-id="3ca61-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="3ca61-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="3ca61-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span><span class="sxs-lookup"><span data-stu-id="3ca61-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="3ca61-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span><span class="sxs-lookup"><span data-stu-id="3ca61-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="3ca61-255">Example</span><span class="sxs-lookup"><span data-stu-id="3ca61-255">Example</span></span>
<span data-ttu-id="3ca61-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3ca61-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="3ca61-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span><span class="sxs-lookup"><span data-stu-id="3ca61-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="3ca61-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span><span class="sxs-lookup"><span data-stu-id="3ca61-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="3ca61-259">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ca61-259">Next steps</span></span>
* <span data-ttu-id="3ca61-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="3ca61-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="3ca61-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="3ca61-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="3ca61-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="3ca61-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>










