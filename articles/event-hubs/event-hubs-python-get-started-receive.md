---
title: Receive events from Azure Event Hubs using Python | Microsoft Docs
description: Get started receiving events from Event Hubs using Python
services: event-hubs
author: sethmanheim
manager: femila
ms.service: event-hubs
ms.workload: core
ms.topic: article
ms.date: 07/26/2018
ms.author: sethm
ms.openlocfilehash: f5388f2de599d94f68a1d24a7d701a2cb4795915
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871589"
---
# <a name="receive-events-from-event-hubs-using-python"></a><span data-ttu-id="d10fa-103">Receive events from Event Hubs using Python</span><span class="sxs-lookup"><span data-stu-id="d10fa-103">Receive events from Event Hubs using Python</span></span>

<span data-ttu-id="d10fa-104">Azure Event Hubs is a highly scalable event management system that can handle millions of events per second, enabling applications to process and analyze massive amounts of data produced by connected devices and other systems.</span><span class="sxs-lookup"><span data-stu-id="d10fa-104">Azure Event Hubs is a highly scalable event management system that can handle millions of events per second, enabling applications to process and analyze massive amounts of data produced by connected devices and other systems.</span></span> <span data-ttu-id="d10fa-105">Once collected into an event hub, you can receive and handle events using in-process handlers or by forwarding to other analytics systems.</span><span class="sxs-lookup"><span data-stu-id="d10fa-105">Once collected into an event hub, you can receive and handle events using in-process handlers or by forwarding to other analytics systems.</span></span>

<span data-ttu-id="d10fa-106">To learn more about Event Hubs, see the [Event Hubs overview][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="d10fa-106">To learn more about Event Hubs, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="d10fa-107">This tutorial describes how to receive events from an event hub from an application written in Python.</span><span class="sxs-lookup"><span data-stu-id="d10fa-107">This tutorial describes how to receive events from an event hub from an application written in Python.</span></span> <span data-ttu-id="d10fa-108">To send events, see [the corresponding Send article](event-hubs-python-get-started-send.md).</span><span class="sxs-lookup"><span data-stu-id="d10fa-108">To send events, see [the corresponding Send article](event-hubs-python-get-started-send.md).</span></span>

<span data-ttu-id="d10fa-109">Code in this tutorial is taken from [these GitHub samples](https://github.com/Azure/azure-event-hubs-python/tree/master/examples), which you can examine to see the full working application, including import statements and variable declarations.</span><span class="sxs-lookup"><span data-stu-id="d10fa-109">Code in this tutorial is taken from [these GitHub samples](https://github.com/Azure/azure-event-hubs-python/tree/master/examples), which you can examine to see the full working application, including import statements and variable declarations.</span></span> <span data-ttu-id="d10fa-110">Other examples are available in the same GitHub folder.</span><span class="sxs-lookup"><span data-stu-id="d10fa-110">Other examples are available in the same GitHub folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d10fa-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d10fa-111">Prerequisites</span></span>

<span data-ttu-id="d10fa-112">To complete this tutorial, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="d10fa-112">To complete this tutorial, you need the following prerequisites:</span></span>

- <span data-ttu-id="d10fa-113">Python 3.4 or later.</span><span class="sxs-lookup"><span data-stu-id="d10fa-113">Python 3.4 or later.</span></span>
- <span data-ttu-id="d10fa-114">An existing Event Hubs namespace and event hub.</span><span class="sxs-lookup"><span data-stu-id="d10fa-114">An existing Event Hubs namespace and event hub.</span></span> <span data-ttu-id="d10fa-115">You can create these entities by following the instructions in [this article](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="d10fa-115">You can create these entities by following the instructions in [this article](event-hubs-create.md).</span></span> 

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]


## <a name="install-python-package"></a><span data-ttu-id="d10fa-116">Install Python package</span><span class="sxs-lookup"><span data-stu-id="d10fa-116">Install Python package</span></span>

<span data-ttu-id="d10fa-117">To install the Python package for Event Hubs, open a command prompt that has Python in its path, and then run this command:</span><span class="sxs-lookup"><span data-stu-id="d10fa-117">To install the Python package for Event Hubs, open a command prompt that has Python in its path, and then run this command:</span></span> 

```bash
pip install azure-eventhub
```

## <a name="create-a-python-script-to-receive-events"></a><span data-ttu-id="d10fa-118">Create a Python script to receive events</span><span class="sxs-lookup"><span data-stu-id="d10fa-118">Create a Python script to receive events</span></span>

<span data-ttu-id="d10fa-119">Next, create a Python application that receives events from an event hub:</span><span class="sxs-lookup"><span data-stu-id="d10fa-119">Next, create a Python application that receives events from an event hub:</span></span>

1. <span data-ttu-id="d10fa-120">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="d10fa-120">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="d10fa-121">Create a script called **recv.py**.</span><span class="sxs-lookup"><span data-stu-id="d10fa-121">Create a script called **recv.py**.</span></span>
3. <span data-ttu-id="d10fa-122">Paste the following code into recv.py, replacing the ADDRESS, USER, and KEY values with the values you obtained from the Azure portal in the previous section:</span><span class="sxs-lookup"><span data-stu-id="d10fa-122">Paste the following code into recv.py, replacing the ADDRESS, USER, and KEY values with the values you obtained from the Azure portal in the previous section:</span></span> 

```python
import os
import sys
import logging
import time
from azure.eventhub import EventHubClient, Receiver, Offset

logger = logging.getLogger("azure")

# Address can be in either of these formats:
# "amqps://<URL-encoded-SAS-policy>:<URL-encoded-SAS-key>@<mynamespace>.servicebus.windows.net/myeventhub"
# "amqps://<mynamespace>.servicebus.windows.net/myeventhub"
# For example:
ADDRESS = "amqps://mynamespace.servicebus.windows.net/myeventhub"

# SAS policy and key are not required if they are encoded in the URL
USER = "RootManageSharedAccessKey"
KEY = "namespaceSASKey"
CONSUMER_GROUP = "$default"
OFFSET = Offset("-1")
PARTITION = "0"

total = 0
last_sn = -1
last_offset = "-1"
client = EventHubClient(ADDRESS, debug=False, username=USER, password=KEY)
try:
    receiver = client.add_receiver(CONSUMER_GROUP, PARTITION, prefetch=5000, offset=OFFSET)
    client.run()
    start_time = time.time()
    for event_data in receiver.receive(timeout=100):
        last_offset = event_data.offset
        last_sn = event_data.sequence_number
        print("Received: {}, {}".format(last_offset, last_sn))
        total += 1

    end_time = time.time()
    client.stop()
    run_time = end_time - start_time
    print("Received {} messages in {} seconds".format(total, run_time))

except KeyboardInterrupt:
    pass
finally:
    client.stop()
```

## <a name="receive-events"></a><span data-ttu-id="d10fa-123">Receive events</span><span class="sxs-lookup"><span data-stu-id="d10fa-123">Receive events</span></span>

<span data-ttu-id="d10fa-124">To run the script, open a command prompt that has Python in its path, and then run this command:</span><span class="sxs-lookup"><span data-stu-id="d10fa-124">To run the script, open a command prompt that has Python in its path, and then run this command:</span></span>

```bash
start python recv.py
```
 
## <a name="next-steps"></a><span data-ttu-id="d10fa-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="d10fa-125">Next steps</span></span>

<span data-ttu-id="d10fa-126">To send events, see [the corresponding Send article](event-hubs-python-get-started-send.md).</span><span class="sxs-lookup"><span data-stu-id="d10fa-126">To send events, see [the corresponding Send article](event-hubs-python-get-started-send.md).</span></span>

<span data-ttu-id="d10fa-127">Visit the following pages to learn more about Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="d10fa-127">Visit the following pages to learn more about Event Hubs:</span></span>

* <span data-ttu-id="d10fa-128">[Event Hubs overview][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="d10fa-128">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="d10fa-129">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="d10fa-129">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="d10fa-130">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="d10fa-130">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-about.md
[Visual Studio Code]: https://code.visualstudio.com/
[free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
