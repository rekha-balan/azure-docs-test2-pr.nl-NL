---
title: Use IoT Hub events to trigger Azure Logic Apps | Microsoft Docs
description: Using the event routing service of Azure Event Grid, create automated processes to perform Azure Logic Apps actions based on IoT Hub events.
services: iot-hub
documentationcenter: ''
author: kgremban
manager: timlt
editor: ''
ms.service: iot-hub
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2018
ms.author: kgremban
ms.openlocfilehash: 43b317cd9d1c9384a58e9d525fdd15d18eb63968
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871488"
---
# <a name="send-email-notifications-about-azure-iot-hub-events-using-logic-apps"></a><span data-ttu-id="a6361-103">Send email notifications about Azure IoT Hub events using Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a6361-103">Send email notifications about Azure IoT Hub events using Logic Apps</span></span>

<span data-ttu-id="a6361-104">Azure Event Grid enables you to react to events in IoT Hub by triggering actions in your downstream business applications.</span><span class="sxs-lookup"><span data-stu-id="a6361-104">Azure Event Grid enables you to react to events in IoT Hub by triggering actions in your downstream business applications.</span></span>

<span data-ttu-id="a6361-105">This article walks through a sample configuration that uses IoT Hub and Event grid.</span><span class="sxs-lookup"><span data-stu-id="a6361-105">This article walks through a sample configuration that uses IoT Hub and Event grid.</span></span> <span data-ttu-id="a6361-106">By the end, you will have an Azure logic app set up to send a notification email every time a device is added to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6361-106">By the end, you will have an Azure logic app set up to send a notification email every time a device is added to your IoT hub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a6361-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a6361-107">Prerequisites</span></span>

* <span data-ttu-id="a6361-108">An email account from any email provider that is supported by Azure Logic Apps, like Office 365 Outlook, Outlook.com, or Gmail.</span><span class="sxs-lookup"><span data-stu-id="a6361-108">An email account from any email provider that is supported by Azure Logic Apps, like Office 365 Outlook, Outlook.com, or Gmail.</span></span> <span data-ttu-id="a6361-109">This email account is used to send the event notifications.</span><span class="sxs-lookup"><span data-stu-id="a6361-109">This email account is used to send the event notifications.</span></span> <span data-ttu-id="a6361-110">For a complete list of supported Logic App connectors, see the [Connectors overview](https://docs.microsoft.com/connectors/)</span><span class="sxs-lookup"><span data-stu-id="a6361-110">For a complete list of supported Logic App connectors, see the [Connectors overview](https://docs.microsoft.com/connectors/)</span></span>
* <span data-ttu-id="a6361-111">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="a6361-111">An active Azure account.</span></span> <span data-ttu-id="a6361-112">If you don't have one, you can [create a free account](http://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6361-112">If you don't have one, you can [create a free account](http://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a6361-113">An IoT Hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6361-113">An IoT Hub in Azure.</span></span> <span data-ttu-id="a6361-114">If you haven't created one yet, see [Get started with IoT Hub](../iot-hub/iot-hub-csharp-csharp-getstarted.md) for a walkthrough.</span><span class="sxs-lookup"><span data-stu-id="a6361-114">If you haven't created one yet, see [Get started with IoT Hub](../iot-hub/iot-hub-csharp-csharp-getstarted.md) for a walkthrough.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="a6361-115">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="a6361-115">Create a logic app</span></span>

<span data-ttu-id="a6361-116">First, create a logic app and add an Event grid trigger that monitors the resource group for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a6361-116">First, create a logic app and add an Event grid trigger that monitors the resource group for your virtual machine.</span></span> 

### <a name="create-a-logic-app-resource"></a><span data-ttu-id="a6361-117">Create a logic app resource</span><span class="sxs-lookup"><span data-stu-id="a6361-117">Create a logic app resource</span></span>

1. <span data-ttu-id="a6361-118">In the [Azure portal](https://portal.azure.com), select **New** > **Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="a6361-118">In the [Azure portal](https://portal.azure.com), select **New** > **Integration** > **Logic App**.</span></span>

   ![Create logic app](./media/publish-iot-hub-events-to-logic-apps/select-logic-app.png)

2. <span data-ttu-id="a6361-120">Give your logic app a name that's unique in your subscription, then select the same subscription, resource group, and location as your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6361-120">Give your logic app a name that's unique in your subscription, then select the same subscription, resource group, and location as your IoT hub.</span></span> 
3. <span data-ttu-id="a6361-121">When you're ready, select **Pin to dashboard**, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6361-121">When you're ready, select **Pin to dashboard**, and choose **Create**.</span></span>

   <span data-ttu-id="a6361-122">You've now created an Azure resource for your logic app.</span><span class="sxs-lookup"><span data-stu-id="a6361-122">You've now created an Azure resource for your logic app.</span></span> <span data-ttu-id="a6361-123">After Azure deploys your logic app, the Logic Apps Designer shows you templates for common patterns so you can get started faster.</span><span class="sxs-lookup"><span data-stu-id="a6361-123">After Azure deploys your logic app, the Logic Apps Designer shows you templates for common patterns so you can get started faster.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="a6361-124">When you select **Pin to dashboard**, your logic app automatically opens in Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="a6361-124">When you select **Pin to dashboard**, your logic app automatically opens in Logic Apps Designer.</span></span> <span data-ttu-id="a6361-125">Otherwise, you can manually find and open your logic app.</span><span class="sxs-lookup"><span data-stu-id="a6361-125">Otherwise, you can manually find and open your logic app.</span></span>

4. <span data-ttu-id="a6361-126">In the Logic App Designer under **Templates**, choose **Blank Logic App** so that you can build your logic app from scratch.</span><span class="sxs-lookup"><span data-stu-id="a6361-126">In the Logic App Designer under **Templates**, choose **Blank Logic App** so that you can build your logic app from scratch.</span></span>

### <a name="select-a-trigger"></a><span data-ttu-id="a6361-127">Select a trigger</span><span class="sxs-lookup"><span data-stu-id="a6361-127">Select a trigger</span></span>

<span data-ttu-id="a6361-128">A trigger is a specific event that starts your logic app.</span><span class="sxs-lookup"><span data-stu-id="a6361-128">A trigger is a specific event that starts your logic app.</span></span> <span data-ttu-id="a6361-129">For this tutorial, the trigger that sets off the workflow is receiving a request over HTTP.</span><span class="sxs-lookup"><span data-stu-id="a6361-129">For this tutorial, the trigger that sets off the workflow is receiving a request over HTTP.</span></span>  

1. <span data-ttu-id="a6361-130">In the connectors and triggers search bar, type **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="a6361-130">In the connectors and triggers search bar, type **HTTP**.</span></span>
2. <span data-ttu-id="a6361-131">Select **Request - When an HTTP request is received** as the trigger.</span><span class="sxs-lookup"><span data-stu-id="a6361-131">Select **Request - When an HTTP request is received** as the trigger.</span></span> 

   ![Select HTTP request trigger](./media/publish-iot-hub-events-to-logic-apps/http-request-trigger.png)

3. <span data-ttu-id="a6361-133">Select **Use sample payload to generate schema**.</span><span class="sxs-lookup"><span data-stu-id="a6361-133">Select **Use sample payload to generate schema**.</span></span> 

   ![Select HTTP request trigger](./media/publish-iot-hub-events-to-logic-apps/sample-payload.png)

4. <span data-ttu-id="a6361-135">Paste the following sample JSON code into the text box, then select **Done**:</span><span class="sxs-lookup"><span data-stu-id="a6361-135">Paste the following sample JSON code into the text box, then select **Done**:</span></span>

```json
[{
  "id": "56afc886-767b-d359-d59e-0da7877166b2",
  "topic": "/SUBSCRIPTIONS/<subscription ID>/RESOURCEGROUPS/<resource group name>/PROVIDERS/MICROSOFT.DEVICES/IOTHUBS/<hub name>",
  "subject": "devices/LogicAppTestDevice",
  "eventType": "Microsoft.Devices.DeviceCreated",
  "eventTime": "2018-01-02T19:17:44.4383997Z",
  "data": {
    "twin": {
      "deviceId": "LogicAppTestDevice",
      "etag": "AAAAAAAAAAE=",
      "deviceEtag": "null",
      "status": "enabled",
      "statusUpdateTime": "0001-01-01T00:00:00",
      "connectionState": "Disconnected",
      "lastActivityTime": "0001-01-01T00:00:00",
      "cloudToDeviceMessageCount": 0,
      "authenticationType": "sas",
      "x509Thumbprint": {
        "primaryThumbprint": null,
        "secondaryThumbprint": null
      },
      "version": 2,
      "properties": {
        "desired": {
          "$metadata": {
            "$lastUpdated": "2018-01-02T19:17:44.4383997Z"
          },
          "$version": 1
        },
        "reported": {
          "$metadata": {
            "$lastUpdated": "2018-01-02T19:17:44.4383997Z"
          },
          "$version": 1
        }
      }
    },
    "hubName": "egtesthub1",
    "deviceId": "LogicAppTestDevice"
  },
  "dataVersion": "1",
  "metadataVersion": "1"
}]
```

5. <span data-ttu-id="a6361-136">You may receive a pop-up notification that says, **Remember to include a Content-Type header set to application/json in your request.**</span><span class="sxs-lookup"><span data-stu-id="a6361-136">You may receive a pop-up notification that says, **Remember to include a Content-Type header set to application/json in your request.**</span></span> <span data-ttu-id="a6361-137">You can safely ignore this suggestion, and move on to the next section.</span><span class="sxs-lookup"><span data-stu-id="a6361-137">You can safely ignore this suggestion, and move on to the next section.</span></span> 

### <a name="create-an-action"></a><span data-ttu-id="a6361-138">Create an action</span><span class="sxs-lookup"><span data-stu-id="a6361-138">Create an action</span></span>

<span data-ttu-id="a6361-139">Actions are any steps that occur after the trigger starts the logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="a6361-139">Actions are any steps that occur after the trigger starts the logic app workflow.</span></span> <span data-ttu-id="a6361-140">For this tutorial, the action is to send an email notification from your email provider.</span><span class="sxs-lookup"><span data-stu-id="a6361-140">For this tutorial, the action is to send an email notification from your email provider.</span></span> 

1. <span data-ttu-id="a6361-141">Select **New step**.</span><span class="sxs-lookup"><span data-stu-id="a6361-141">Select **New step**.</span></span> <span data-ttu-id="a6361-142">This will open a window to **Choose an action**.</span><span class="sxs-lookup"><span data-stu-id="a6361-142">This will open a window to **Choose an action**.</span></span>
2. <span data-ttu-id="a6361-143">Search for **Email**.</span><span class="sxs-lookup"><span data-stu-id="a6361-143">Search for **Email**.</span></span>
3. <span data-ttu-id="a6361-144">Based on your email provider, find and select the matching connector.</span><span class="sxs-lookup"><span data-stu-id="a6361-144">Based on your email provider, find and select the matching connector.</span></span> <span data-ttu-id="a6361-145">This tutorial uses **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="a6361-145">This tutorial uses **Office 365 Outlook**.</span></span> <span data-ttu-id="a6361-146">The steps for other email providers are similar.</span><span class="sxs-lookup"><span data-stu-id="a6361-146">The steps for other email providers are similar.</span></span> 

   ![Select email provider connector](./media/publish-iot-hub-events-to-logic-apps/o365-outlook.png)

4. <span data-ttu-id="a6361-148">Select the **Send an email** action.</span><span class="sxs-lookup"><span data-stu-id="a6361-148">Select the **Send an email** action.</span></span> 
5. <span data-ttu-id="a6361-149">If prompted, sign in to your email account.</span><span class="sxs-lookup"><span data-stu-id="a6361-149">If prompted, sign in to your email account.</span></span> 
6. <span data-ttu-id="a6361-150">Build your email template.</span><span class="sxs-lookup"><span data-stu-id="a6361-150">Build your email template.</span></span> 
   * <span data-ttu-id="a6361-151">**To**: Enter the email address to receive the notification emails.</span><span class="sxs-lookup"><span data-stu-id="a6361-151">**To**: Enter the email address to receive the notification emails.</span></span> <span data-ttu-id="a6361-152">For this tutorial, use an email account that you can access for testing.</span><span class="sxs-lookup"><span data-stu-id="a6361-152">For this tutorial, use an email account that you can access for testing.</span></span> 
   * <span data-ttu-id="a6361-153">**Subject** and **Body**: Write the text for your email.</span><span class="sxs-lookup"><span data-stu-id="a6361-153">**Subject** and **Body**: Write the text for your email.</span></span> <span data-ttu-id="a6361-154">Select JSON properties from the selector tool to include dynamic content based on event data.</span><span class="sxs-lookup"><span data-stu-id="a6361-154">Select JSON properties from the selector tool to include dynamic content based on event data.</span></span>  

   <span data-ttu-id="a6361-155">Your email template may look like this example:</span><span class="sxs-lookup"><span data-stu-id="a6361-155">Your email template may look like this example:</span></span>

   ![Fill out email information](./media/publish-iot-hub-events-to-logic-apps/email-content.png)

7. <span data-ttu-id="a6361-157">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="a6361-157">Save your logic app.</span></span> 

### <a name="copy-the-http-url"></a><span data-ttu-id="a6361-158">Copy the HTTP URL</span><span class="sxs-lookup"><span data-stu-id="a6361-158">Copy the HTTP URL</span></span>

<span data-ttu-id="a6361-159">Before you leave the Logic Apps Designer, copy the URL that your logic apps is listening to for a trigger.</span><span class="sxs-lookup"><span data-stu-id="a6361-159">Before you leave the Logic Apps Designer, copy the URL that your logic apps is listening to for a trigger.</span></span> <span data-ttu-id="a6361-160">You use this URL to configure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="a6361-160">You use this URL to configure Event Grid.</span></span> 

1. <span data-ttu-id="a6361-161">Expand the **When a HTTP request is received** trigger configuration box by clicking on it.</span><span class="sxs-lookup"><span data-stu-id="a6361-161">Expand the **When a HTTP request is received** trigger configuration box by clicking on it.</span></span> 
2. <span data-ttu-id="a6361-162">Copy the value of **HTTP POST URL** by selecting the copy button next to it.</span><span class="sxs-lookup"><span data-stu-id="a6361-162">Copy the value of **HTTP POST URL** by selecting the copy button next to it.</span></span> 

   ![Copy the HTTP POST URL](./media/publish-iot-hub-events-to-logic-apps/copy-url.png)

3. <span data-ttu-id="a6361-164">Save this URL so that you can refer to it in the next section.</span><span class="sxs-lookup"><span data-stu-id="a6361-164">Save this URL so that you can refer to it in the next section.</span></span> 

## <a name="configure-subscription-for-iot-hub-events"></a><span data-ttu-id="a6361-165">Configure subscription for IoT Hub events</span><span class="sxs-lookup"><span data-stu-id="a6361-165">Configure subscription for IoT Hub events</span></span>

<span data-ttu-id="a6361-166">In this section, you configure your IoT Hub to publish events as they occur.</span><span class="sxs-lookup"><span data-stu-id="a6361-166">In this section, you configure your IoT Hub to publish events as they occur.</span></span> 

1. <span data-ttu-id="a6361-167">In the Azure portal, navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6361-167">In the Azure portal, navigate to your IoT hub.</span></span> 
2. <span data-ttu-id="a6361-168">Select **Events**.</span><span class="sxs-lookup"><span data-stu-id="a6361-168">Select **Events**.</span></span>

   ![Open the Event Grid details](./media/publish-iot-hub-events-to-logic-apps/event-grid.png)

3. <span data-ttu-id="a6361-170">Select **Event subscription**.</span><span class="sxs-lookup"><span data-stu-id="a6361-170">Select **Event subscription**.</span></span> 

   ![Create new event subscription](./media/publish-iot-hub-events-to-logic-apps/event-subscription.png)

4. <span data-ttu-id="a6361-172">Create the event subscription with the following values:</span><span class="sxs-lookup"><span data-stu-id="a6361-172">Create the event subscription with the following values:</span></span> 
    * <span data-ttu-id="a6361-173">**Event Type**: Uncheck Subscribe to all event types and select **Device Created** from the menu.</span><span class="sxs-lookup"><span data-stu-id="a6361-173">**Event Type**: Uncheck Subscribe to all event types and select **Device Created** from the menu.</span></span>
    * <span data-ttu-id="a6361-174">**Endpoint Details**: Select Endpoint Type as **Web Hook** and click on select endpoint and paste the URL that you copied from your logic app and confirm selection.</span><span class="sxs-lookup"><span data-stu-id="a6361-174">**Endpoint Details**: Select Endpoint Type as **Web Hook** and click on select endpoint and paste the URL that you copied from your logic app and confirm selection.</span></span>

    ![select endpoint url](./media/publish-iot-hub-events-to-logic-apps/endpoint-url.png)

    * <span data-ttu-id="a6361-176">**Event Subscription Details**: Provide a descriptive name and select **Event Grid Schema**</span><span class="sxs-lookup"><span data-stu-id="a6361-176">**Event Subscription Details**: Provide a descriptive name and select **Event Grid Schema**</span></span>

  <span data-ttu-id="a6361-177">You could save the event subscription here, and receive notifications for every device that is created in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6361-177">You could save the event subscription here, and receive notifications for every device that is created in your IoT hub.</span></span> <span data-ttu-id="a6361-178">For this tutorial, though, let's use the optional fields to filter for specific devices:</span><span class="sxs-lookup"><span data-stu-id="a6361-178">For this tutorial, though, let's use the optional fields to filter for specific devices:</span></span> 

  * <span data-ttu-id="a6361-179">**Subject Begins With**: Enter `devices/Building1_` to filter for device events in building 1.</span><span class="sxs-lookup"><span data-stu-id="a6361-179">**Subject Begins With**: Enter `devices/Building1_` to filter for device events in building 1.</span></span>
  * <span data-ttu-id="a6361-180">**Subject Ends With**: Enter `_Temperature` to filter for device events related to temperature.</span><span class="sxs-lookup"><span data-stu-id="a6361-180">**Subject Ends With**: Enter `_Temperature` to filter for device events related to temperature.</span></span>

  <span data-ttu-id="a6361-181">When you're done, the form should look like the following example:</span><span class="sxs-lookup"><span data-stu-id="a6361-181">When you're done, the form should look like the following example:</span></span> 

    ![Sample event subscription form](./media/publish-iot-hub-events-to-logic-apps/subscription-form.png)
    
5. <span data-ttu-id="a6361-183">Select **Create** to save the event subscription.</span><span class="sxs-lookup"><span data-stu-id="a6361-183">Select **Create** to save the event subscription.</span></span>

## <a name="create-a-new-device"></a><span data-ttu-id="a6361-184">Create a new device</span><span class="sxs-lookup"><span data-stu-id="a6361-184">Create a new device</span></span>

<span data-ttu-id="a6361-185">Test your logic app by creating a new device to trigger an event notification email.</span><span class="sxs-lookup"><span data-stu-id="a6361-185">Test your logic app by creating a new device to trigger an event notification email.</span></span> 

1. <span data-ttu-id="a6361-186">From your IoT hub, select **IoT Devices**.</span><span class="sxs-lookup"><span data-stu-id="a6361-186">From your IoT hub, select **IoT Devices**.</span></span> 
2. <span data-ttu-id="a6361-187">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="a6361-187">Select **Add**.</span></span>
3. <span data-ttu-id="a6361-188">For **Device ID**, enter `Building1_Floor1_Room1_Temperature`.</span><span class="sxs-lookup"><span data-stu-id="a6361-188">For **Device ID**, enter `Building1_Floor1_Room1_Temperature`.</span></span>
4. <span data-ttu-id="a6361-189">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="a6361-189">Select **Save**.</span></span> 
5. <span data-ttu-id="a6361-190">You can add multiple devices with different device IDs to test the event subscription filters.</span><span class="sxs-lookup"><span data-stu-id="a6361-190">You can add multiple devices with different device IDs to test the event subscription filters.</span></span> <span data-ttu-id="a6361-191">Try these examples:</span><span class="sxs-lookup"><span data-stu-id="a6361-191">Try these examples:</span></span> 
   * <span data-ttu-id="a6361-192">Building1_Floor1_Room1_Light</span><span class="sxs-lookup"><span data-stu-id="a6361-192">Building1_Floor1_Room1_Light</span></span>
   * <span data-ttu-id="a6361-193">Building1_Floor2_Room2_Temperature</span><span class="sxs-lookup"><span data-stu-id="a6361-193">Building1_Floor2_Room2_Temperature</span></span>
   * <span data-ttu-id="a6361-194">Building2_Floor1_Room1_Temperature</span><span class="sxs-lookup"><span data-stu-id="a6361-194">Building2_Floor1_Room1_Temperature</span></span>
   * <span data-ttu-id="a6361-195">Building2_Floor1_Room1_Light</span><span class="sxs-lookup"><span data-stu-id="a6361-195">Building2_Floor1_Room1_Light</span></span>

<span data-ttu-id="a6361-196">Once you've added a few devices to your IoT hub, check your email to see which ones triggered the logic app.</span><span class="sxs-lookup"><span data-stu-id="a6361-196">Once you've added a few devices to your IoT hub, check your email to see which ones triggered the logic app.</span></span> 

## <a name="use-the-azure-cli"></a><span data-ttu-id="a6361-197">Use the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a6361-197">Use the Azure CLI</span></span>

<span data-ttu-id="a6361-198">Instead of using the Azure portal, you can accomplish the IoT Hub steps using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a6361-198">Instead of using the Azure portal, you can accomplish the IoT Hub steps using the Azure CLI.</span></span> <span data-ttu-id="a6361-199">For details, see the Azure CLI pages for [creating an event subscription](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription) and [creating an IoT device](https://docs.microsoft.com/cli/azure/ext/azure-cli-iot-ext/iot/hub/device-identity)</span><span class="sxs-lookup"><span data-stu-id="a6361-199">For details, see the Azure CLI pages for [creating an event subscription](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription) and [creating an IoT device](https://docs.microsoft.com/cli/azure/ext/azure-cli-iot-ext/iot/hub/device-identity)</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="a6361-200">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a6361-200">Clean up resources</span></span>

<span data-ttu-id="a6361-201">This tutorial used resources that incur charges on your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a6361-201">This tutorial used resources that incur charges on your Azure subscription.</span></span> <span data-ttu-id="a6361-202">When you're done trying out the tutorial and testing your results, disable or delete resources that you don't want to keep.</span><span class="sxs-lookup"><span data-stu-id="a6361-202">When you're done trying out the tutorial and testing your results, disable or delete resources that you don't want to keep.</span></span> 

<span data-ttu-id="a6361-203">If you don't want to lose the work on your logic app, disable it instead of deleting it.</span><span class="sxs-lookup"><span data-stu-id="a6361-203">If you don't want to lose the work on your logic app, disable it instead of deleting it.</span></span> 

1. <span data-ttu-id="a6361-204">Navigate to your logic app.</span><span class="sxs-lookup"><span data-stu-id="a6361-204">Navigate to your logic app.</span></span>
2. <span data-ttu-id="a6361-205">On the **Overview** blade select **Delete** or **Disable**.</span><span class="sxs-lookup"><span data-stu-id="a6361-205">On the **Overview** blade select **Delete** or **Disable**.</span></span> 

<span data-ttu-id="a6361-206">Each subscription can have one free IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6361-206">Each subscription can have one free IoT hub.</span></span> <span data-ttu-id="a6361-207">If you created a free hub for this tutorial, then you don't need to delete it to prevent charges.</span><span class="sxs-lookup"><span data-stu-id="a6361-207">If you created a free hub for this tutorial, then you don't need to delete it to prevent charges.</span></span>

1. <span data-ttu-id="a6361-208">Navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6361-208">Navigate to your IoT hub.</span></span> 
2. <span data-ttu-id="a6361-209">On the **Overview** blade select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="a6361-209">On the **Overview** blade select **Delete**.</span></span> 

<span data-ttu-id="a6361-210">Even if you keep your IoT hub, you may want to delete the event subscription that you created.</span><span class="sxs-lookup"><span data-stu-id="a6361-210">Even if you keep your IoT hub, you may want to delete the event subscription that you created.</span></span> 

1. <span data-ttu-id="a6361-211">In your IoT hub, select **Event Grid**.</span><span class="sxs-lookup"><span data-stu-id="a6361-211">In your IoT hub, select **Event Grid**.</span></span>
2. <span data-ttu-id="a6361-212">Select the event subscription that you want to remove.</span><span class="sxs-lookup"><span data-stu-id="a6361-212">Select the event subscription that you want to remove.</span></span> 
3. <span data-ttu-id="a6361-213">Select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="a6361-213">Select **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a6361-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6361-214">Next steps</span></span>

* <span data-ttu-id="a6361-215">Learn more about [Reacting to IoT Hub events by using Event Grid to trigger actions](../iot-hub/iot-hub-event-grid.md).</span><span class="sxs-lookup"><span data-stu-id="a6361-215">Learn more about [Reacting to IoT Hub events by using Event Grid to trigger actions](../iot-hub/iot-hub-event-grid.md).</span></span>
* [<span data-ttu-id="a6361-216">Learn how to order device connected and disconnected events</span><span class="sxs-lookup"><span data-stu-id="a6361-216">Learn how to order device connected and disconnected events</span></span>](../iot-hub/iot-hub-how-to-order-connection-state-events.md)
* <span data-ttu-id="a6361-217">Learn about what else you can do with [Event Grid](overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6361-217">Learn about what else you can do with [Event Grid](overview.md).</span></span>


