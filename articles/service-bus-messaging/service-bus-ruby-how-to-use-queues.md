---
title: How to use Azure Service Bus queues with Ruby | Microsoft Docs
description: Learn how to use Service Bus queues in Azure. Code samples written in Ruby.
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 01/11/2017
ms.author: sethm
ms.openlocfilehash: 343dc0d39f284488f03e1d1ba3df21ae616e97d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556482"
---
# <a name="how-to-use-service-bus-queues"></a>How to use Service Bus queues
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

This guide describes how to use Service Bus queues. The samples are written in Ruby and use the Azure gem. The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**. For more information about Service Bus queues, see the [Next Steps](#next-steps) section.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
## <a name="create-a-ruby-application"></a>Create a Ruby application
Create a Ruby application. For instructions, see [Create a Ruby Application on Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-to-use-service-bus"></a>Configure your application to use Service Bus
To use Azure Service Bus, download and use the Ruby Azure package, which includes a set of convenience libraries that communicate with the storage REST services.

### <a name="use-rubygems-to-obtain-the-package"></a>Use RubyGems to obtain the package
1. Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).
2. Type "gem install azure" in the command window to install the gem and dependencies.

### <a name="import-the-package"></a>Import the package
Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:

```
require "azure"
```

## <a name="set-up-an-azure-service-bus-connection"></a>Set up an Azure Service Bus connection
The Azure module reads the environment variables **AZURE\_SERVICEBUS\_NAMESPACE** and **AZURE\_SERVICEBUS\_ACCESS_KEY** for information required to connect to your Service Bus namespace. If these environment variables are not set, you must specify the namespace information before using **Azure::ServiceBusService** with the following code:

```ruby
Azure.config.sb_namespace = "<your azure service bus namespace>"
Azure.config.sb_access_key = "<your azure service bus access key>"
```

Set the namespace value to the value you created, rather than the entire URL. For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".

## <a name="how-to-create-a-queue"></a>How to create a queue
The **Azure::ServiceBusService** object enables you to work with queues. To create a queue, use the **create_queue()** method. The following example creates a queue or prints out any errors.

```ruby
azure_service_bus_service = Azure::ServiceBusService.new
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

You can also pass a **Azure::ServiceBus::Queue** object with additional options, which enables you to override the default queue settings, such as message time to live or maximum queue size. The following example shows how to set the maximum queue size to 5GB and time to live to 1 minute:

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-to-send-messages-to-a-queue"></a>How to send messages to a queue
To send a message to a Service Bus queue, your application calls the **send\_queue\_message()** method on the **Azure::ServiceBusService** object. Messages sent to (and received from) Service Bus queues are **Azure::ServiceBus::BrokeredMessage** objects, and have a set of standard properties (such as **label** and **time\_to\_live**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data. An application can set the body of the message by passing a string value as the message and any required standard properties will be populated with default values.

The following example demonstrates how to send a test message to the queue named "test-queue" using **send\_queue\_message()**:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md). The header, which includes the standard and custom application properties, can have a maximum size of 64 KB. There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue. This queue size is defined at creation time, with an upper limit of 5 GB.

## <a name="how-to-receive-messages-from-a-queue"></a>How to receive messages from a queue
Messages are received from a queue using the **receive\_queue\_message()** method on the **Azure::ServiceBusService** object. By default, messages are read and locked without being deleted from the queue. However, you can delete messages from the queue as they are read by setting the **:peek_lock** option to **false**.

The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages. When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application. After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **delete\_queue\_message()** method and providing the message to be deleted as a parameter. The **delete\_queue\_message()** method will mark the message as being consumed and remove it from the queue.

If the **:peek\_lock** parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure. To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it. Because Service Bus will have marked the message as being consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.

The following example demonstrates how to receive and process messages using **receive\_queue\_message()**. The example first receives and deletes a message by using **:peek\_lock** set to **false**, then it receives another message and then deletes the message using **delete\_queue\_message()**:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>How to handle application crashes and unreadable messages
Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message. If a receiver application is unable to process the message for some reason, then it can call the **unlock\_queue\_message()** method on the **Azure::ServiceBusService** object. This causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.

There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.

In the event that the application crashes after processing the message but before the **delete\_queue\_message()** method is called, then the message will be redelivered to the application when it restarts. This is often called **At Least Once Processing**; that is, each message is processed at least once but in certain situations the same message may be redelivered. If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery. This is often achieved using the **message\_id** property of the message, which remains constant across delivery attempts.

## <a name="next-steps"></a>Next steps
Now that you've learned the basics of Service Bus queues, follow these links to learn more.

* Overview of [queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).
* Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.

For a comparison between the Azure Service Bus queues discussed in this article and Azure Queues discussed in the [How to use Queue storage from Ruby](../storage/storage-ruby-how-to-use-queue-storage.md) article, see [Azure Queues and Azure Service Bus Queues - Compared and Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

