---
title: Notification Hubs - Enterprise Push Architecture
description: Guidance on using Azure Notification Hubs in an enterprise environment
services: notification-hubs
documentationcenter: ''
author: ysxu
manager: erikre
editor: ''
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: fa1dfa43ace29907d45ac8e46a8fb3ea57d3b954
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551119"
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="d3bd1-103">Enterprise push architectural guidance</span><span class="sxs-lookup"><span data-stu-id="d3bd1-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="d3bd1-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span><span class="sxs-lookup"><span data-stu-id="d3bd1-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span></span> <span data-ttu-id="d3bd1-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span></span> <span data-ttu-id="d3bd1-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span></span>

<span data-ttu-id="d3bd1-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span></span> <span data-ttu-id="d3bd1-108">E.g.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-108">E.g.</span></span> <span data-ttu-id="d3bd1-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span></span>

<span data-ttu-id="d3bd1-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span></span> <span data-ttu-id="d3bd1-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span></span> <span data-ttu-id="d3bd1-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span></span> <span data-ttu-id="d3bd1-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span></span>
<span data-ttu-id="d3bd1-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span></span>

<span data-ttu-id="d3bd1-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span><span class="sxs-lookup"><span data-stu-id="d3bd1-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="d3bd1-116">Architecture</span><span class="sxs-lookup"><span data-stu-id="d3bd1-116">Architecture</span></span>
![][1]

<span data-ttu-id="d3bd1-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span><span class="sxs-lookup"><span data-stu-id="d3bd1-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="d3bd1-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span></span> <span data-ttu-id="d3bd1-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span></span> <span data-ttu-id="d3bd1-120">The backend systems will send messages to these topics.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-120">The backend systems will send messages to these topics.</span></span> <span data-ttu-id="d3bd1-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="d3bd1-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span></span> <span data-ttu-id="d3bd1-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span></span> <span data-ttu-id="d3bd1-124">Notification hubs then eventually delivers the message to the mobile app.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-124">Notification hubs then eventually delivers the message to the mobile app.</span></span> <span data-ttu-id="d3bd1-125">So to summarize the key components, we have:</span><span class="sxs-lookup"><span data-stu-id="d3bd1-125">So to summarize the key components, we have:</span></span>

1. <span data-ttu-id="d3bd1-126">Backend systems (LoB/Legacy systems)</span><span class="sxs-lookup"><span data-stu-id="d3bd1-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="d3bd1-127">Creates Service Bus Topic</span><span class="sxs-lookup"><span data-stu-id="d3bd1-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="d3bd1-128">Sends Message</span><span class="sxs-lookup"><span data-stu-id="d3bd1-128">Sends Message</span></span>
2. <span data-ttu-id="d3bd1-129">Mobile backend</span><span class="sxs-lookup"><span data-stu-id="d3bd1-129">Mobile backend</span></span>
   * <span data-ttu-id="d3bd1-130">Creates Service Subscription</span><span class="sxs-lookup"><span data-stu-id="d3bd1-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="d3bd1-131">Receives Message (from Backend system)</span><span class="sxs-lookup"><span data-stu-id="d3bd1-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="d3bd1-132">Sends notification to clients (via Azure Notification Hub)</span><span class="sxs-lookup"><span data-stu-id="d3bd1-132">Sends notification to clients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="d3bd1-133">Mobile Application</span><span class="sxs-lookup"><span data-stu-id="d3bd1-133">Mobile Application</span></span>
   * <span data-ttu-id="d3bd1-134">Receives and display notification</span><span class="sxs-lookup"><span data-stu-id="d3bd1-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="d3bd1-135">Benefits:</span><span class="sxs-lookup"><span data-stu-id="d3bd1-135">Benefits:</span></span>
1. <span data-ttu-id="d3bd1-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="d3bd1-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="d3bd1-138">Sample:</span><span class="sxs-lookup"><span data-stu-id="d3bd1-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="d3bd1-139">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d3bd1-139">Prerequisites</span></span>
<span data-ttu-id="d3bd1-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span><span class="sxs-lookup"><span data-stu-id="d3bd1-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="d3bd1-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span></span>
2. <span data-ttu-id="d3bd1-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="d3bd1-143">Sample code</span><span class="sxs-lookup"><span data-stu-id="d3bd1-143">Sample code</span></span>
<span data-ttu-id="d3bd1-144">The full sample code is available at [Notification Hub Samples].</span><span class="sxs-lookup"><span data-stu-id="d3bd1-144">The full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="d3bd1-145">It is split into three components:</span><span class="sxs-lookup"><span data-stu-id="d3bd1-145">It is split into three components:</span></span>

1. <span data-ttu-id="d3bd1-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="d3bd1-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="d3bd1-147">a.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-147">a.</span></span> <span data-ttu-id="d3bd1-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span><span class="sxs-lookup"><span data-stu-id="d3bd1-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="d3bd1-149">b.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-149">b.</span></span> <span data-ttu-id="d3bd1-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="d3bd1-151">c.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-151">c.</span></span> <span data-ttu-id="d3bd1-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create the topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="d3bd1-153">d.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-153">d.</span></span> <span data-ttu-id="d3bd1-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span></span> <span data-ttu-id="d3bd1-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span></span> <span data-ttu-id="d3bd1-156">Normally there will be a backend system which will send messages when an event occurs.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds to the topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched to a different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. <span data-ttu-id="d3bd1-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="d3bd1-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="d3bd1-158">a.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-158">a.</span></span> <span data-ttu-id="d3bd1-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span><span class="sxs-lookup"><span data-stu-id="d3bd1-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="d3bd1-160">b.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-160">b.</span></span> <span data-ttu-id="d3bd1-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span></span> <span data-ttu-id="d3bd1-162">This will be part of your Mobile backend.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="d3bd1-163">c.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-163">c.</span></span> <span data-ttu-id="d3bd1-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span></span> <span data-ttu-id="d3bd1-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span><span class="sxs-lookup"><span data-stu-id="d3bd1-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create the subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="d3bd1-166">d.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-166">d.</span></span> <span data-ttu-id="d3bd1-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize the Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from the subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    <span data-ttu-id="d3bd1-168">e.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-168">e.</span></span> <span data-ttu-id="d3bd1-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span><span class="sxs-lookup"><span data-stu-id="d3bd1-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="d3bd1-170">f.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-170">f.</span></span> <span data-ttu-id="d3bd1-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="d3bd1-172">g.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-172">g.</span></span> <span data-ttu-id="d3bd1-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span><span class="sxs-lookup"><span data-stu-id="d3bd1-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span></span>
   
    ![][4]
3. <span data-ttu-id="d3bd1-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="d3bd1-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="d3bd1-175">a.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-175">a.</span></span> <span data-ttu-id="d3bd1-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="d3bd1-177">This is based on [Notification Hubs - Windows Universal tutorial].</span><span class="sxs-lookup"><span data-stu-id="d3bd1-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="d3bd1-178">b.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-178">b.</span></span> <span data-ttu-id="d3bd1-179">Ensure that your application is enabled to receive toast notifications.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-179">Ensure that your application is enabled to receive toast notifications.</span></span>
   
    <span data-ttu-id="d3bd1-180">c.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-180">c.</span></span> <span data-ttu-id="d3bd1-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="d3bd1-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="d3bd1-182">Running sample:</span><span class="sxs-lookup"><span data-stu-id="d3bd1-182">Running sample:</span></span>
1. <span data-ttu-id="d3bd1-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span><span class="sxs-lookup"><span data-stu-id="d3bd1-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span></span>
2. <span data-ttu-id="d3bd1-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span></span>
3. <span data-ttu-id="d3bd1-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span><span class="sxs-lookup"><span data-stu-id="d3bd1-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span></span>
   
    ![][5]
4. <span data-ttu-id="d3bd1-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="d3bd1-187">Once a message was received, a notification was created and sent to the mobile app.</span><span class="sxs-lookup"><span data-stu-id="d3bd1-187">Once a message was received, a notification was created and sent to the mobile app.</span></span> <span data-ttu-id="d3bd1-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span><span class="sxs-lookup"><span data-stu-id="d3bd1-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[Notification Hub Samples]: https://github.com/Azure/azure-notificationhubs-samples
[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/
[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[Service Bus Pub/Sub programming]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[Notification Hubs - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[Azure Classic Portal]: https://manage.windowsazure.com/






