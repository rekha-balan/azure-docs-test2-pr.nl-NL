---
title: IoT remote monitoring and notifications with Azure Logic Apps | Microsoft Docs
description: Use Azure Logic Apps for IoT temperature monitoring on your IoT hub and automatically send email notifications to your mailbox for any anomalies detected.
author: rangv
manager: ''
keywords: iot monitoring, iot notifications, iot temperature monitoring
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 04/11/2018
ms.author: rangv
ms.openlocfilehash: e59577e99114f1b2061a2f9075976da3f0b1811f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825760"
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="692d0-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span><span class="sxs-lookup"><span data-stu-id="692d0-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![End-to-end diagram](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="692d0-106">Azure Logic Apps provides a way to automate processes as a series of steps.</span><span class="sxs-lookup"><span data-stu-id="692d0-106">Azure Logic Apps provides a way to automate processes as a series of steps.</span></span> <span data-ttu-id="692d0-107">A logic app can connect across various services and protocols.</span><span class="sxs-lookup"><span data-stu-id="692d0-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="692d0-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span><span class="sxs-lookup"><span data-stu-id="692d0-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="692d0-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span><span class="sxs-lookup"><span data-stu-id="692d0-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="692d0-110">What you learn</span><span class="sxs-lookup"><span data-stu-id="692d0-110">What you learn</span></span>

<span data-ttu-id="692d0-111">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span><span class="sxs-lookup"><span data-stu-id="692d0-111">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="692d0-112">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="692d0-112">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span></span> <span data-ttu-id="692d0-113">The message triggers the logic app to send you an email notification.</span><span class="sxs-lookup"><span data-stu-id="692d0-113">The message triggers the logic app to send you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="692d0-114">What you do</span><span class="sxs-lookup"><span data-stu-id="692d0-114">What you do</span></span>

* <span data-ttu-id="692d0-115">Create a service bus namespace and add a queue to it.</span><span class="sxs-lookup"><span data-stu-id="692d0-115">Create a service bus namespace and add a queue to it.</span></span>
* <span data-ttu-id="692d0-116">Add an endpoint and a routing rule to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="692d0-116">Add an endpoint and a routing rule to your IoT hub.</span></span>
* <span data-ttu-id="692d0-117">Create, configure, and test a logic app.</span><span class="sxs-lookup"><span data-stu-id="692d0-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="692d0-118">What you need</span><span class="sxs-lookup"><span data-stu-id="692d0-118">What you need</span></span>

* <span data-ttu-id="692d0-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span><span class="sxs-lookup"><span data-stu-id="692d0-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  * <span data-ttu-id="692d0-120">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="692d0-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="692d0-121">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="692d0-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="692d0-122">A client application that sends messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="692d0-122">A client application that sends messages to your Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-to-it"></a><span data-ttu-id="692d0-123">Create service bus namespace and add a queue to it</span><span class="sxs-lookup"><span data-stu-id="692d0-123">Create service bus namespace and add a queue to it</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="692d0-124">Create a service bus namespace</span><span class="sxs-lookup"><span data-stu-id="692d0-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="692d0-125">On the [Azure portal](https://portal.azure.com/), click **Create a resource** > **Enterprise Integration** > **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="692d0-125">On the [Azure portal](https://portal.azure.com/), click **Create a resource** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="692d0-126">Provide the following information:</span><span class="sxs-lookup"><span data-stu-id="692d0-126">Provide the following information:</span></span>

   <span data-ttu-id="692d0-127">**Name**: The name of the service bus.</span><span class="sxs-lookup"><span data-stu-id="692d0-127">**Name**: The name of the service bus.</span></span>

   <span data-ttu-id="692d0-128">**Pricing tier**: Click **Basic** > **Select**.</span><span class="sxs-lookup"><span data-stu-id="692d0-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="692d0-129">The Basic tier is sufficient for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="692d0-129">The Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="692d0-130">**Resource group**: Use the same resource group that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="692d0-130">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="692d0-131">**Location**: Use the same location that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="692d0-131">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="692d0-132">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="692d0-132">Click **Create**.</span></span>

   ![Create a service bus namespace in the Azure portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="692d0-134">Add a service bus queue</span><span class="sxs-lookup"><span data-stu-id="692d0-134">Add a service bus queue</span></span>

1. <span data-ttu-id="692d0-135">Open the service bus namespace, and then click **+ Queue**.</span><span class="sxs-lookup"><span data-stu-id="692d0-135">Open the service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="692d0-136">Enter a name for the queue and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="692d0-136">Enter a name for the queue and then click **Create**.</span></span>
1. <span data-ttu-id="692d0-137">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="692d0-137">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="692d0-138">Enter a name for the policy, check **Manage**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="692d0-138">Enter a name for the policy, check **Manage**, and then click **Create**.</span></span>

   ![Add a service bus queue in the Azure portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-to-your-iot-hub"></a><span data-ttu-id="692d0-140">Add an endpoint and a routing rule to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="692d0-140">Add an endpoint and a routing rule to your IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="692d0-141">Add an endpoint</span><span class="sxs-lookup"><span data-stu-id="692d0-141">Add an endpoint</span></span>

1. <span data-ttu-id="692d0-142">Open your IoT hub, click Endpoints > + Add.</span><span class="sxs-lookup"><span data-stu-id="692d0-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="692d0-143">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="692d0-143">Enter the following information:</span></span>

   <span data-ttu-id="692d0-144">**Name**: The name of the endpoint.</span><span class="sxs-lookup"><span data-stu-id="692d0-144">**Name**: The name of the endpoint.</span></span>

   <span data-ttu-id="692d0-145">**Endpoint type**: Select **Service Bus Queue**.</span><span class="sxs-lookup"><span data-stu-id="692d0-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="692d0-146">**Service Bus namespace**: Select the namespace you created.</span><span class="sxs-lookup"><span data-stu-id="692d0-146">**Service Bus namespace**: Select the namespace you created.</span></span>

   <span data-ttu-id="692d0-147">**Service Bus queue**: Select the queue you created.</span><span class="sxs-lookup"><span data-stu-id="692d0-147">**Service Bus queue**: Select the queue you created.</span></span>
1. <span data-ttu-id="692d0-148">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="692d0-148">Click **OK**.</span></span>

   ![Add an endpoint to your IoT hub in the Azure portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="692d0-150">Add a routing rule</span><span class="sxs-lookup"><span data-stu-id="692d0-150">Add a routing rule</span></span>

1. <span data-ttu-id="692d0-151">In your IoT hub, click **Routes** > **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="692d0-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="692d0-152">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="692d0-152">Enter the following information:</span></span>

   <span data-ttu-id="692d0-153">**Name**: The name of the routing rule.</span><span class="sxs-lookup"><span data-stu-id="692d0-153">**Name**: The name of the routing rule.</span></span>

   <span data-ttu-id="692d0-154">**Data source**: Select **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="692d0-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="692d0-155">**Endpoint**: Select the endpoint you created.</span><span class="sxs-lookup"><span data-stu-id="692d0-155">**Endpoint**: Select the endpoint you created.</span></span>

   <span data-ttu-id="692d0-156">**Query string**: Enter `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="692d0-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="692d0-157">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="692d0-157">Click **Save**.</span></span>

   ![Add a routing rule in the Azure portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="692d0-159">Create and configure a logic app</span><span class="sxs-lookup"><span data-stu-id="692d0-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="692d0-160">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="692d0-160">Create a logic app</span></span>

1. <span data-ttu-id="692d0-161">In the [Azure portal](https://portal.azure.com/), click **Create a resource** > **Enterprise Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="692d0-161">In the [Azure portal](https://portal.azure.com/), click **Create a resource** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="692d0-162">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="692d0-162">Enter the following information:</span></span>

   <span data-ttu-id="692d0-163">**Name**: The name of the logic app.</span><span class="sxs-lookup"><span data-stu-id="692d0-163">**Name**: The name of the logic app.</span></span>

   <span data-ttu-id="692d0-164">**Resource group**: Use the same resource group that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="692d0-164">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="692d0-165">**Location**: Use the same location that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="692d0-165">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="692d0-166">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="692d0-166">Click **Create**.</span></span>

### <a name="configure-the-logic-app"></a><span data-ttu-id="692d0-167">Configure the logic app</span><span class="sxs-lookup"><span data-stu-id="692d0-167">Configure the logic app</span></span>

1. <span data-ttu-id="692d0-168">Open the logic app that opens into the Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="692d0-168">Open the logic app that opens into the Logic Apps Designer.</span></span>
1. <span data-ttu-id="692d0-169">In the Logic Apps Designer, click **Blank Logic App**.</span><span class="sxs-lookup"><span data-stu-id="692d0-169">In the Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Start with a blank logic app in the Azure portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="692d0-171">Click **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="692d0-171">Click **Service Bus**.</span></span>

   ![Select Service Bus to start creating your logic app in the Azure portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="692d0-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span><span class="sxs-lookup"><span data-stu-id="692d0-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="692d0-174">Create a service bus connection.</span><span class="sxs-lookup"><span data-stu-id="692d0-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="692d0-175">Enter a connection name.</span><span class="sxs-lookup"><span data-stu-id="692d0-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="692d0-176">Click the service bus namespace > the service bus policy > **Create**.</span><span class="sxs-lookup"><span data-stu-id="692d0-176">Click the service bus namespace > the service bus policy > **Create**.</span></span>

      ![Create a service bus connection for your logic app in the Azure portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="692d0-178">Click **Continue** after the service bus connection is created.</span><span class="sxs-lookup"><span data-stu-id="692d0-178">Click **Continue** after the service bus connection is created.</span></span>
   1. <span data-ttu-id="692d0-179">Select the queue that you created and enter `175` for **Maximum message count**</span><span class="sxs-lookup"><span data-stu-id="692d0-179">Select the queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Specify the maximum message count for the service bus connection in your logic app](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="692d0-181">Click "Save" button to save the changes.</span><span class="sxs-lookup"><span data-stu-id="692d0-181">Click "Save" button to save the changes.</span></span>

1. <span data-ttu-id="692d0-182">Create an SMTP service connection.</span><span class="sxs-lookup"><span data-stu-id="692d0-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="692d0-183">Click **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="692d0-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="692d0-184">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span><span class="sxs-lookup"><span data-stu-id="692d0-184">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span></span>

      ![Create an SMTP connection in your logic app in the Azure portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="692d0-186">Enter the SMTP information of your mailbox, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="692d0-186">Enter the SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Enter SMTP connection info in your logic app in the Azure portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="692d0-188">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="692d0-188">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="692d0-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span><span class="sxs-lookup"><span data-stu-id="692d0-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="692d0-190">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="692d0-190">Click **Save**.</span></span>

<span data-ttu-id="692d0-191">The logic app is in working order when you save it.</span><span class="sxs-lookup"><span data-stu-id="692d0-191">The logic app is in working order when you save it.</span></span>

## <a name="test-the-logic-app"></a><span data-ttu-id="692d0-192">Test the logic app</span><span class="sxs-lookup"><span data-stu-id="692d0-192">Test the logic app</span></span>

1. <span data-ttu-id="692d0-193">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="692d0-193">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="692d0-194">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span><span class="sxs-lookup"><span data-stu-id="692d0-194">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="692d0-195">You should receive an email notification sent by the logic app.</span><span class="sxs-lookup"><span data-stu-id="692d0-195">You should receive an email notification sent by the logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="692d0-196">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span><span class="sxs-lookup"><span data-stu-id="692d0-196">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="692d0-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="692d0-197">Next steps</span></span>

<span data-ttu-id="692d0-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span><span class="sxs-lookup"><span data-stu-id="692d0-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
