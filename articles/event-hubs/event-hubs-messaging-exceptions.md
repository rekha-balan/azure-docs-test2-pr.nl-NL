---
title: Azure Event Hubs messaging exceptions | Microsoft Docs
description: List of Azure Event Hubs messaging exceptions and suggested actions.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 2c6273de-0106-47e5-b45d-59040e51f2c5
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/07/2017
ms.author: sethm
ms.openlocfilehash: f88c4914478c3adf823fc22a0e049e73fb43e8db
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563266"
---
# <a name="event-hubs-messaging-exceptions"></a>Event Hubs messaging exceptions
This article lists some exceptions generated by the Azure Service Bus messaging APIs, which includes Event Hubs. This reference is subject to change, so check back for updates.

## <a name="exception-categories"></a>Exception categories
The Event Hubs APIs generate exceptions that can fall into the following categories, along with the associated action you can take to try to fix them.

1. User coding error: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). General action: try to fix the code before proceeding.
2. Setup/configuration error: [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). General action: review your configuration and change if necessary.
3. Transient exceptions: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception), [Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). General action: retry the operation or notify users.
4. Other exceptions: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](#timeoutexception), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception). General action: specific to the exception type; please refer to the table in the following section. 

## <a name="exception-types"></a>Exception types
The following table lists messaging exception types, and their causes, and notes suggested action you can take.

| **Exception Type** | **Description/Cause/Examples** | **Suggested Action** | **Note on automatic/immediate retry** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |The server did not respond to the requested operation within the specified time, which is controlled by [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). The server may have completed the requested operation. This can happen due to network or other infrastructure delays. |Check the system state for consistency and retry if necessary.<br /> See [TimeoutException](#timeoutexception). |Retry might help in some cases; add retry logic to code. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |The requested user operation is not allowed within the server or service. See the exception message for details. For example, [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) generates this exception if the message was received in [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode. |Check the code and the documentation. Make sure the requested operation is valid. |Retry will not help. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |An attempt is made to invoke an operation on an object that has already been closed, aborted or disposed. In rare cases, the ambient transaction is already disposed. |Check the code and make sure it does not invoke operations on a disposed object. |Retry will not help. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) object could not acquire a token, the token is invalid, or the token does not contain the claims required to perform the operation. |Make sure the token provider is created with the correct values. Check the configuration of the Access Control service. |Retry might help in some cases; add retry logic to code. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |One or more arguments supplied to the method are invalid. The URI supplied to [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) or [Create](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) contains path segment(s). The URI scheme supplied to [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) or [Create](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) is invalid. The property value is larger than 32KB. |Check the calling code and make sure the arguments are correct. |Retry will not help. |
| [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /> [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) |Entity associated with the operation does not exist or it has been deleted. |Make sure the entity exists. |Retry will not help. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Attempt to receive a message with a particular sequence number. This message is not found. |Make sure the message has not been received already. Check the deadletter queue to see if the message has been deadlettered. |Retry will not help. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Client is not able to establish a connection to Event Hub. |Make sure the supplied host name is correct and the host is reachable. |Retry might help if there are intermittent connectivity issues. |
| [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) |Service is not able to process the request at this time. |Client can wait for a period of time, then retry the operation. <br /> See [ServerBusyException](#serverbusyexception). |Client may retry after certain interval. If a retry results in a different exception, check retry behavior of that exception. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Lock token associated with the message has expired, or the lock token is not found. |Dispose the message. |Retry will not help. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Lock associated with this session is lost. | Abort the [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) object. |Retry will not help. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Generic messaging exception that may be thrown in the following cases: An attempt is made to create a [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) using a name or path that belongs to a different entity type (for example, a topic). An attempt is made to send a message larger than 256KB. The server or service encountered an error during processing of the request. Please see the exception message for details. This is usually a transient exception. |Check the code and ensure that only serializable objects are used for the message body (or use a custom serializer). Check the documentation for the supported value types of the properties and only use supported types. Check the [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) property. If it is **true**, you can retry the operation. |Retry behavior is undefined and might not help. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Attempt to create an entity with a name that is already used by another entity in that service namespace. |Delete the existing entity or choose a different name for the entity to be created. |Retry will not help. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |The messaging entity has reached its maximum allowable size. This can happen if the maximum number of receivers (which is 5) has already been opened on a per-consumer group level. |Create space in the entity by receiving messages from the entity or its sub-queues. <br /> See [QuotaExceededException](#quotaexceededexception) |Retry might help if messages have been removed in the meantime. |
|  | | | |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Attempt to accept a session with a specific session ID, but the session is currently locked by another client. |Make sure the session is unlocked by other clients. |Retry might help if the session has been released in the interim. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Too many operations are part of the transaction. |Reduce the number of operations that are part of this transaction. |Retry will not help. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Request for a runtime operation on a disabled entity. |Activate the entity. |Retry might help if the entity has been activated in the interim. |
| [Microsoft.ServiceBus.Messaging.MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /> [Microsoft.Azure.EventHubs.MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | A message payload exceeds the 256K limit. Note that the 256k limit is the total message size, which can include system properties and any .NET overhead. |Reduce the size of the message payload, then retry the operation. |Retry will not help. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |The ambient transaction (*Transaction.Current*) is invalid. It may have been completed or aborted. Inner exception may provide additional information. | |Retry will not help. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |An operation is attempted on a transaction that is in doubt, or an attempt is made to commit the transaction and the transaction becomes in doubt. |Your application must handle this exception (as a special case), as the transaction may have already been committed. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indicates that a quota for a specific entity has been exceeded.

This can happen if the maximum number of receivers (5) has already been opened on a per-consumer group level.

### <a name="event-hubs"></a>Event Hubs
Event Hubs has a limit of 20 consumer groups per Event Hub. When you attempt to create more, you receive a [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indicates that a user-initiated operation is taking longer than the operation timeout. 

For Event Hubs, the timeout is specified either as part of the connection string, or through [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). The error message itself might vary, but it always contains the timeout value specified for the current operation. 

### <a name="common-causes"></a>Common causes
There are two common causes for this error: incorrect configuration, or a transient service error.

1. **Incorrect configuration** The operation timeout might be too small for the operational condition. The default value for the operation timeout in the client SDK is 60 seconds. Check to see if your code has the value set to something too small. Note that the condition of the network and CPU usage can affect the time it takes for a particular operation to complete, so the operation timeout should not be set to a very small value.
2. **Transient service error** Sometimes the Event Hubs service can experience delays in processing requests; for example, during periods of high traffic. In such cases, you can retry your operation after a delay, until the operation is successful. If the same operation still fails after multiple attempts, please visit the [Azure service status site](https://azure.microsoft.com/status/) to see if there are any known service outages.

## <a name="serverbusyexception"></a>ServerBusyException

A [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) or [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) indicates that a server is overloaded. There are two relevant error codes for this exception.

### <a name="error-code-50002"></a>Error code 50002

This error can occur for one of two reasons:

1. The load is not evenly distributed across all partitions on the Event Hub, and one partition hits the local throughput unit limitation.
    
    Resolution: Revising the partition distribution strategy or trying [EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) might help.

2. The Event Hubs namespace does not have sufficient throughput units (you can check the **Metrics** blade on Event Hubs namespace blade in the [Azure portal](https://portal.azure.com) to confirm). Note that the portal shows aggregated (1 minute) information, but we measure the throughput in real time – so it is only an estimate.

    Resolution: Increasing the throughput units on the namespace can help. You can do this on the portal, in the **Scale** blade of the Event Hubs namespace blade.

### <a name="error-code-50001"></a>Error code 50001

This error should rarely occur. It happens when the container running code for your namespace is low on CPU – not more than a few seconds before the Event Hubs load balancer begins.


## <a name="next-steps"></a>Next steps
You can learn more about Event Hubs by visiting the following links:

* [Event Hubs overview](event-hubs-what-is-event-hubs.md)
* [Create an Event Hub](event-hubs-create.md)
* [Event Hubs FAQ](event-hubs-faq.md)