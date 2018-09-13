---
title: IoT remote monitoring and notifications with Azure Logic Apps | Microsoft Docs
description: Use Azure Logic Apps for IoT temperature monitoring on your IoT hub and automatically sending email notifications to your mailbox for anomalies detected.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot monitoring, iot notifications, iot temperature monitoring
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: xshi
ms.openlocfilehash: a3b212c0151cd041000e4754b6b1e5b628b5a0f5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549198"
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="86177-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span><span class="sxs-lookup"><span data-stu-id="86177-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="86177-105">Azure Logic Apps provides a way to automate processes as a series of steps.</span><span class="sxs-lookup"><span data-stu-id="86177-105">Azure Logic Apps provides a way to automate processes as a series of steps.</span></span> <span data-ttu-id="86177-106">A logic app can connect across various services and protocols.</span><span class="sxs-lookup"><span data-stu-id="86177-106">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="86177-107">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span><span class="sxs-lookup"><span data-stu-id="86177-107">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="86177-108">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span><span class="sxs-lookup"><span data-stu-id="86177-108">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="86177-109">What you learn</span><span class="sxs-lookup"><span data-stu-id="86177-109">What you learn</span></span>

<span data-ttu-id="86177-110">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span><span class="sxs-lookup"><span data-stu-id="86177-110">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="86177-111">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="86177-111">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span></span> <span data-ttu-id="86177-112">The message triggers the logic app to send you an email notification.</span><span class="sxs-lookup"><span data-stu-id="86177-112">The message triggers the logic app to send you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="86177-113">What you do</span><span class="sxs-lookup"><span data-stu-id="86177-113">What you do</span></span>

* <span data-ttu-id="86177-114">Create a service bus namespace and add a queue to it.</span><span class="sxs-lookup"><span data-stu-id="86177-114">Create a service bus namespace and add a queue to it.</span></span>
* <span data-ttu-id="86177-115">Add an endpoint and a routing rule to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="86177-115">Add an endpoint and a routing rule to your IoT hub.</span></span>
* <span data-ttu-id="86177-116">Create, configure, and test a logic app.</span><span class="sxs-lookup"><span data-stu-id="86177-116">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="86177-117">What you need</span><span class="sxs-lookup"><span data-stu-id="86177-117">What you need</span></span>

* <span data-ttu-id="86177-118">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span><span class="sxs-lookup"><span data-stu-id="86177-118">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  * <span data-ttu-id="86177-119">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="86177-119">An active Azure subscription.</span></span>
  * <span data-ttu-id="86177-120">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="86177-120">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="86177-121">A client application that sends messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="86177-121">A client application that sends messages to your Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-to-it"></a><span data-ttu-id="86177-122">Create service bus namespace and add a queue to it</span><span class="sxs-lookup"><span data-stu-id="86177-122">Create service bus namespace and add a queue to it</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="86177-123">Create a service bus namespace</span><span class="sxs-lookup"><span data-stu-id="86177-123">Create a service bus namespace</span></span>

1. <span data-ttu-id="86177-124">On the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="86177-124">On the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="86177-125">Provide the following information:</span><span class="sxs-lookup"><span data-stu-id="86177-125">Provide the following information:</span></span>

   <span data-ttu-id="86177-126">**Name**: The name of the service bus.</span><span class="sxs-lookup"><span data-stu-id="86177-126">**Name**: The name of the service bus.</span></span>

   <span data-ttu-id="86177-127">**Pricing tier**: Click **Basic** > **Select**.</span><span class="sxs-lookup"><span data-stu-id="86177-127">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="86177-128">The Basic tier is sufficient for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="86177-128">The Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="86177-129">**Resource group**: Use the same resource group that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="86177-129">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="86177-130">**Location**: Use the same location that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="86177-130">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="86177-131">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="86177-131">Click **Create**.</span></span>

   ![Create a service bus namespace in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="86177-133">Add a service bus queue</span><span class="sxs-lookup"><span data-stu-id="86177-133">Add a service bus queue</span></span>

1. <span data-ttu-id="86177-134">Open the service bus namespace, and then click **+ Queue**.</span><span class="sxs-lookup"><span data-stu-id="86177-134">Open the service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="86177-135">Enter a name for the queue and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="86177-135">Enter a name for the queue and then click **Create**.</span></span>
1. <span data-ttu-id="86177-136">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="86177-136">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="86177-137">Enter a name for the policy, check **Manage**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="86177-137">Enter a name for the policy, check **Manage**, and then click **Create**.</span></span>

   ![Add a service bus queue in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-to-your-iot-hub"></a><span data-ttu-id="86177-139">Add an endpoint and a routing rule to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="86177-139">Add an endpoint and a routing rule to your IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="86177-140">Add an endpoint</span><span class="sxs-lookup"><span data-stu-id="86177-140">Add an endpoint</span></span>

1. <span data-ttu-id="86177-141">Open your IoT hub, click Endpoints > + Add.</span><span class="sxs-lookup"><span data-stu-id="86177-141">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="86177-142">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="86177-142">Enter the following information:</span></span>

   <span data-ttu-id="86177-143">**Name**: The name of the endpoint.</span><span class="sxs-lookup"><span data-stu-id="86177-143">**Name**: The name of the endpoint.</span></span>

   <span data-ttu-id="86177-144">**Endpoint type**: Select **Service Bus Queue**.</span><span class="sxs-lookup"><span data-stu-id="86177-144">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="86177-145">**Service Bus namespace**: Select the namespace you created.</span><span class="sxs-lookup"><span data-stu-id="86177-145">**Service Bus namespace**: Select the namespace you created.</span></span>

   <span data-ttu-id="86177-146">**Service Bus queue**: Select the queue you created.</span><span class="sxs-lookup"><span data-stu-id="86177-146">**Service Bus queue**: Select the queue you created.</span></span>
1. <span data-ttu-id="86177-147">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="86177-147">Click **OK**.</span></span>

   ![Add an endpoint to your IoT hub in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="86177-149">Add a routing rule</span><span class="sxs-lookup"><span data-stu-id="86177-149">Add a routing rule</span></span>

1. <span data-ttu-id="86177-150">In your IoT hub, click **Routes** > **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="86177-150">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="86177-151">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="86177-151">Enter the following information:</span></span>

   <span data-ttu-id="86177-152">**Name**: The name of the routing rule.</span><span class="sxs-lookup"><span data-stu-id="86177-152">**Name**: The name of the routing rule.</span></span>

   <span data-ttu-id="86177-153">**Data source**: Select **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="86177-153">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="86177-154">**Endpoint**: Select the endpoint you created.</span><span class="sxs-lookup"><span data-stu-id="86177-154">**Endpoint**: Select the endpoint you created.</span></span>

   <span data-ttu-id="86177-155">**Query string**: Enter `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="86177-155">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="86177-156">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="86177-156">Click **Save**.</span></span>

   ![Add a routing rule in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="86177-158">Create and configure a logic app</span><span class="sxs-lookup"><span data-stu-id="86177-158">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="86177-159">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="86177-159">Create a logic app</span></span>

1. <span data-ttu-id="86177-160">In the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="86177-160">In the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="86177-161">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="86177-161">Enter the following information:</span></span>

   <span data-ttu-id="86177-162">**Name**: The name of the logic app.</span><span class="sxs-lookup"><span data-stu-id="86177-162">**Name**: The name of the logic app.</span></span>

   <span data-ttu-id="86177-163">**Resource group**: Use the same resource group that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="86177-163">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="86177-164">**Location**: Use the same location that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="86177-164">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="86177-165">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="86177-165">Click **Create**.</span></span>

### <a name="configure-the-logic-app"></a><span data-ttu-id="86177-166">Configure the logic app</span><span class="sxs-lookup"><span data-stu-id="86177-166">Configure the logic app</span></span>

1. <span data-ttu-id="86177-167">Open the logic app that opens into the Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="86177-167">Open the logic app that opens into the Logic Apps Designer.</span></span>
1. <span data-ttu-id="86177-168">In the Logic Apps Designer, click **Blank Logic App**.</span><span class="sxs-lookup"><span data-stu-id="86177-168">In the Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Start with a blank logic app in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="86177-170">Click **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="86177-170">Click **Service Bus**.</span></span>

   ![Select Service Bus to start creating your logic app in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="86177-172">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span><span class="sxs-lookup"><span data-stu-id="86177-172">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="86177-173">Create a service bus connection.</span><span class="sxs-lookup"><span data-stu-id="86177-173">Create a service bus connection.</span></span>
   1. <span data-ttu-id="86177-174">Enter a connection name.</span><span class="sxs-lookup"><span data-stu-id="86177-174">Enter a connection name.</span></span>
   1. <span data-ttu-id="86177-175">Click the service bus namespace > the service bus policy > **Create**.</span><span class="sxs-lookup"><span data-stu-id="86177-175">Click the service bus namespace > the service bus policy > **Create**.</span></span>

      ![Create a service bus connection for your logic app in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="86177-177">Click **Continue** after the service bus connection is created.</span><span class="sxs-lookup"><span data-stu-id="86177-177">Click **Continue** after the service bus connection is created.</span></span>
   1. <span data-ttu-id="86177-178">Select the queue that you created and enter `175` for **Maximum message count**</span><span class="sxs-lookup"><span data-stu-id="86177-178">Select the queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Specify the maximum message count for the service bus connection in your logic app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)

1. <span data-ttu-id="86177-180">Create an SMTP service connection.</span><span class="sxs-lookup"><span data-stu-id="86177-180">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="86177-181">Click **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="86177-181">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="86177-182">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span><span class="sxs-lookup"><span data-stu-id="86177-182">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span></span>

      ![Create an SMTP connection in your logic app in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="86177-184">Enter the SMTP information of your mailbox, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="86177-184">Enter the SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Enter SMTP connection info in your logic app in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="86177-186">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="86177-186">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="86177-187">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span><span class="sxs-lookup"><span data-stu-id="86177-187">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="86177-188">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="86177-188">Click **Save**.</span></span>

<span data-ttu-id="86177-189">The logic app is in working order when you save it.</span><span class="sxs-lookup"><span data-stu-id="86177-189">The logic app is in working order when you save it.</span></span>

## <a name="test-the-logic-app"></a><span data-ttu-id="86177-190">Test the logic app</span><span class="sxs-lookup"><span data-stu-id="86177-190">Test the logic app</span></span>

1. <span data-ttu-id="86177-191">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="86177-191">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="86177-192">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span><span class="sxs-lookup"><span data-stu-id="86177-192">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="86177-193">You should receive an email notification sent by the logic app.</span><span class="sxs-lookup"><span data-stu-id="86177-193">You should receive an email notification sent by the logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="86177-194">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span><span class="sxs-lookup"><span data-stu-id="86177-194">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86177-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="86177-195">Next steps</span></span>

<span data-ttu-id="86177-196">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span><span class="sxs-lookup"><span data-stu-id="86177-196">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]









