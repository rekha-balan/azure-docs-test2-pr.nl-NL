---
title: Debug Azure microservices in Linux | Microsoft Docs
description: Learn how to monitor and diagnose your services written using Microsoft Azure Service Fabric on a local development machine.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: subramar
ms.openlocfilehash: 86ed3f25f0bdd6bb5d8a93f124a0d2bcd7e2b07a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555887"
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="9d5f4-103">Monitor and diagnose services in a local machine development setup</span><span class="sxs-lookup"><span data-stu-id="9d5f4-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="9d5f4-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="9d5f4-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="9d5f4-108">Adopting a similar model during development of services ensures that the diagnostic pipeline works when you move to a production environment.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-108">Adopting a similar model during development of services ensures that the diagnostic pipeline works when you move to a production environment.</span></span> <span data-ttu-id="9d5f4-109">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-109">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="9d5f4-110">Debugging Service Fabric Java applications</span><span class="sxs-lookup"><span data-stu-id="9d5f4-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="9d5f4-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="9d5f4-112">Since `java.util.logging` is the default option with the JRE, it is also used for the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9d5f4-112">Since `java.util.logging` is the default option with the JRE, it is also used for the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="9d5f4-113">The following discussion explains how to configure the `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-113">The following discussion explains how to configure the `java.util.logging` framework.</span></span>

<span data-ttu-id="9d5f4-114">Using java.util.logging you can redirect your application logs to memory, output streams, console files, or sockets.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-114">Using java.util.logging you can redirect your application logs to memory, output streams, console files, or sockets.</span></span> <span data-ttu-id="9d5f4-115">For each of these options, there are default handlers already provided in the framework.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-115">For each of these options, there are default handlers already provided in the framework.</span></span> <span data-ttu-id="9d5f4-116">You can create a `app.properties` file to configure the file handler for your application to redirect all logs to a local file.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-116">You can create a `app.properties` file to configure the file handler for your application to redirect all logs to a local file.</span></span>

<span data-ttu-id="9d5f4-117">The following code snippet contains an example configuration:</span><span class="sxs-lookup"><span data-stu-id="9d5f4-117">The following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="9d5f4-118">The folder pointed to by the `app.properties` file must exist.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-118">The folder pointed to by the `app.properties` file must exist.</span></span> <span data-ttu-id="9d5f4-119">After the `app.properties` file is created, you need to also modify your entry point script, `entrypoint.sh` in the `<applicationfolder>/<servicePkg>/Code/` folder to set the property `java.util.logging.config.file` to `app.propertes` file.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-119">After the `app.properties` file is created, you need to also modify your entry point script, `entrypoint.sh` in the `<applicationfolder>/<servicePkg>/Code/` folder to set the property `java.util.logging.config.file` to `app.propertes` file.</span></span> <span data-ttu-id="9d5f4-120">The entry should look like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="9d5f4-120">The entry should look like the following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path to app.properties> -jar <service name>.jar
```


<span data-ttu-id="9d5f4-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="9d5f4-122">The log file in this case is named mysfapp%u.%g.log where:</span><span class="sxs-lookup"><span data-stu-id="9d5f4-122">The log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="9d5f4-123">**%u** is a unique number to resolve conflicts between simultaneous Java processes.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-123">**%u** is a unique number to resolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="9d5f4-124">**%g** is the generation number to distinguish between rotating logs.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-124">**%g** is the generation number to distinguish between rotating logs.</span></span>

<span data-ttu-id="9d5f4-125">By default if no handler is explicitly configured, the console handler is registered.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-125">By default if no handler is explicitly configured, the console handler is registered.</span></span> <span data-ttu-id="9d5f4-126">One can view the logs in syslog under /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-126">One can view the logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="9d5f4-127">For more information, see the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9d5f4-127">For more information, see the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="9d5f4-128">Debugging Service Fabric C# applications</span><span class="sxs-lookup"><span data-stu-id="9d5f4-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="9d5f4-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="9d5f4-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span><span class="sxs-lookup"><span data-stu-id="9d5f4-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="9d5f4-131">Since EventSource is familiar to C# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-131">Since EventSource is familiar to C# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="9d5f4-132">The first step is to include System.Diagnostics.Tracing so that you can write your logs to memory, output streams, or console files.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-132">The first step is to include System.Diagnostics.Tracing so that you can write your logs to memory, output streams, or console files.</span></span>  <span data-ttu-id="9d5f4-133">For logging using EventSource, add the following project to your project.json:</span><span class="sxs-lookup"><span data-stu-id="9d5f4-133">For logging using EventSource, add the following project to your project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="9d5f4-134">You can use a custom EventListener to listen for the service event and then appropriately redirect them to trace files.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-134">You can use a custom EventListener to listen for the service event and then appropriately redirect them to trace files.</span></span> <span data-ttu-id="9d5f4-135">The following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span><span class="sxs-lookup"><span data-stu-id="9d5f4-135">The following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need to add method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


<span data-ttu-id="9d5f4-136">The preceding snippet outputs the logs to a file in `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-136">The preceding snippet outputs the logs to a file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="9d5f4-137">This file name needs to be appropriately updated.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-137">This file name needs to be appropriately updated.</span></span> <span data-ttu-id="9d5f4-138">In case you want to redirect the logs to console, use the following snippet in your customized EventListener class:</span><span class="sxs-lookup"><span data-stu-id="9d5f4-138">In case you want to redirect the logs to console, use the following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="9d5f4-139">The samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener to log events to a file.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-139">The samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener to log events to a file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="9d5f4-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d5f4-140">Next steps</span></span>
<span data-ttu-id="9d5f4-141">The same tracing code added to your application also works with the diagnostics of your application on an Azure cluster.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-141">The same tracing code added to your application also works with the diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="9d5f4-142">Check out these articles that discuss the different options for the tools and describe how to set them up.</span><span class="sxs-lookup"><span data-stu-id="9d5f4-142">Check out these articles that discuss the different options for the tools and describe how to set them up.</span></span>
* [<span data-ttu-id="9d5f4-143">How to collect logs with Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="9d5f4-143">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
