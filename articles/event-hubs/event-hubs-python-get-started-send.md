---
title: Send events to Azure Event Hubs using Python | Microsoft Docs
description: Get started sending events to Event Hubs using Python
services: event-hubs
author: sethmanheim
manager: femila
ms.service: event-hubs
ms.workload: core
ms.topic: article
ms.date: 07/26/2018
ms.author: sethm
ms.openlocfilehash: 762e21cfc7d16b614eb637c569f8bfc5b6115db1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868776"
---
# <a name="send-events-to-event-hubs-using-python"></a><span data-ttu-id="74fd8-103">Send events to Event Hubs using Python</span><span class="sxs-lookup"><span data-stu-id="74fd8-103">Send events to Event Hubs using Python</span></span>

<span data-ttu-id="74fd8-104">Azure Event Hubs is a highly scalable event management system that can handle millions of events per second, enabling applications to process and analyze massive amounts of data produced by connected devices and other systems.</span><span class="sxs-lookup"><span data-stu-id="74fd8-104">Azure Event Hubs is a highly scalable event management system that can handle millions of events per second, enabling applications to process and analyze massive amounts of data produced by connected devices and other systems.</span></span> <span data-ttu-id="74fd8-105">Once collected into an event hub, you can receive and handle events using in-process handlers or by forwarding to other analytics systems.</span><span class="sxs-lookup"><span data-stu-id="74fd8-105">Once collected into an event hub, you can receive and handle events using in-process handlers or by forwarding to other analytics systems.</span></span>

<span data-ttu-id="74fd8-106">To learn more about Event Hubs, see the [Event Hubs overview][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="74fd8-106">To learn more about Event Hubs, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="74fd8-107">This tutorial describes how to send events to an event hub from an application written in Python.</span><span class="sxs-lookup"><span data-stu-id="74fd8-107">This tutorial describes how to send events to an event hub from an application written in Python.</span></span> <span data-ttu-id="74fd8-108">To receive events, see [the corresponding Receive article](event-hubs-python-get-started-receive.md).</span><span class="sxs-lookup"><span data-stu-id="74fd8-108">To receive events, see [the corresponding Receive article](event-hubs-python-get-started-receive.md).</span></span>

<span data-ttu-id="74fd8-109">Code in this tutorial is taken from [these GitHub samples](https://github.com/Azure/azure-event-hubs-python/tree/master/examples), which you can examine to see the full working application, including import statements and variable declarations.</span><span class="sxs-lookup"><span data-stu-id="74fd8-109">Code in this tutorial is taken from [these GitHub samples](https://github.com/Azure/azure-event-hubs-python/tree/master/examples), which you can examine to see the full working application, including import statements and variable declarations.</span></span> <span data-ttu-id="74fd8-110">Other examples are available in the same GitHub folder.</span><span class="sxs-lookup"><span data-stu-id="74fd8-110">Other examples are available in the same GitHub folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74fd8-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="74fd8-111">Prerequisites</span></span>

<span data-ttu-id="74fd8-112">To complete this tutorial, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="74fd8-112">To complete this tutorial, you need the following prerequisites:</span></span>

- <span data-ttu-id="74fd8-113">Python 3.4 or later.</span><span class="sxs-lookup"><span data-stu-id="74fd8-113">Python 3.4 or later.</span></span>
- <span data-ttu-id="74fd8-114">An existing Event Hubs namespace and event hub.</span><span class="sxs-lookup"><span data-stu-id="74fd8-114">An existing Event Hubs namespace and event hub.</span></span> <span data-ttu-id="74fd8-115">You can create these entities by following the instructions in [this article](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="74fd8-115">You can create these entities by following the instructions in [this article](event-hubs-create.md).</span></span> 

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]


## <a name="install-python-package"></a><span data-ttu-id="74fd8-116">Install Python package</span><span class="sxs-lookup"><span data-stu-id="74fd8-116">Install Python package</span></span>

<span data-ttu-id="74fd8-117">To install the Python package for Event Hubs, open a command prompt that has Python in its path, and then run this command:</span><span class="sxs-lookup"><span data-stu-id="74fd8-117">To install the Python package for Event Hubs, open a command prompt that has Python in its path, and then run this command:</span></span> 

```bash
pip install azure-eventhub
```

## <a name="create-a-python-script-to-send-events"></a><span data-ttu-id="74fd8-118">Create a Python script to send events</span><span class="sxs-lookup"><span data-stu-id="74fd8-118">Create a Python script to send events</span></span>

<span data-ttu-id="74fd8-119">Next, create a Python application that sends events to an event hub:</span><span class="sxs-lookup"><span data-stu-id="74fd8-119">Next, create a Python application that sends events to an event hub:</span></span>

1. <span data-ttu-id="74fd8-120">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="74fd8-120">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="74fd8-121">Create a script called **send.py**.</span><span class="sxs-lookup"><span data-stu-id="74fd8-121">Create a script called **send.py**.</span></span> <span data-ttu-id="74fd8-122">This script sends 100 events to your event hub.</span><span class="sxs-lookup"><span data-stu-id="74fd8-122">This script sends 100 events to your event hub.</span></span>
3. <span data-ttu-id="74fd8-123">Paste the following code into send.py, replacing the ADDRESS, USER, and KEY values with the values you obtained from the Azure portal in the previous section:</span><span class="sxs-lookup"><span data-stu-id="74fd8-123">Paste the following code into send.py, replacing the ADDRESS, USER, and KEY values with the values you obtained from the Azure portal in the previous section:</span></span> 

```python
import sys
import logging
import datetime
import time
import os

from azure.eventhub import EventHubClient, Sender, EventData

logger = logging.getLogger("azure")

# Address can be in either of these formats:
# "amqps://<URL-encoded-SAS-policy>:<URL-encoded-SAS-key>@<mynamespace>.servicebus.windows.net/myeventhub"
# "amqps://<mynamespace>.servicebus.windows.net/myeventhub"
# For example:
ADDRESS = "amqps://mynamespace.servicebus.windows.net/myeventhub"

# SAS policy and key are not required if they are encoded in the URL
USER = "RootManageSharedAccessKey"
KEY = "namespaceSASKey"

try:
    if not ADDRESS:
        raise ValueError("No EventHubs URL supplied.")

    # Create Event Hubs client
    client = EventHubClient(ADDRESS, debug=False, username=USER, password=KEY)
    sender = client.add_sender(partition="0")
    client.run()
    try:
        start_time = time.time()
        for i in range(100):
            print("Sending message: {}".format(i))
            sender.send(EventData(str(i)))
    except:
        raise
    finally:
        end_time = time.time()
        client.stop()
        run_time = end_time - start_time
        logger.info("Runtime: {} seconds".format(run_time))

except KeyboardInterrupt:
    pass
```

## <a name="send-events"></a><span data-ttu-id="74fd8-124">Send events</span><span class="sxs-lookup"><span data-stu-id="74fd8-124">Send events</span></span>

<span data-ttu-id="74fd8-125">To run the script, open a command prompt that has Python in its path, and then run this command:</span><span class="sxs-lookup"><span data-stu-id="74fd8-125">To run the script, open a command prompt that has Python in its path, and then run this command:</span></span>

```bash
start python send.py
```
 
## <a name="next-steps"></a><span data-ttu-id="74fd8-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="74fd8-126">Next steps</span></span>

<span data-ttu-id="74fd8-127">Now that you've sent events to an event hub using Python, to receive events see [the corresponding Receive article](event-hubs-python-get-started-receive.md).</span><span class="sxs-lookup"><span data-stu-id="74fd8-127">Now that you've sent events to an event hub using Python, to receive events see [the corresponding Receive article](event-hubs-python-get-started-receive.md).</span></span>

<span data-ttu-id="74fd8-128">Visit the following pages to learn more about Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="74fd8-128">Visit the following pages to learn more about Event Hubs:</span></span>

* <span data-ttu-id="74fd8-129">[Event Hubs overview][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="74fd8-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="74fd8-130">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="74fd8-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="74fd8-131">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="74fd8-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-about.md
[Visual Studio Code]: https://code.visualstudio.com/
[free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
