---
title: Overview of AMQP 1.0 in Azure Service Bus | Microsoft Docs
description: Learn about using the Advanced Message Queuing Protocol (AMQP) 1.0 in Azure.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 0e8d19cc-de36-478e-84ae-e089bbc2d515
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2017
ms.author: sethm
ms.openlocfilehash: 0f6f4dc3c0fa13cac3b5d7537b824bbe4c988e4c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671963"
---
# <a name="amqp-10-support-in-service-bus"></a><span data-ttu-id="ea7ff-103">AMQP 1.0 support in Service Bus</span><span class="sxs-lookup"><span data-stu-id="ea7ff-103">AMQP 1.0 support in Service Bus</span></span>
<span data-ttu-id="ea7ff-104">Both the Azure Service Bus cloud service and on-premises [Service Bus for Windows Server (Service Bus 1.1)](https://msdn.microsoft.com/library/dn282144.aspx) support the Advanced Message Queueing Protocol (AMQP) 1.0.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-104">Both the Azure Service Bus cloud service and on-premises [Service Bus for Windows Server (Service Bus 1.1)](https://msdn.microsoft.com/library/dn282144.aspx) support the Advanced Message Queueing Protocol (AMQP) 1.0.</span></span> <span data-ttu-id="ea7ff-105">AMQP enables you to build cross-platform, hybrid applications using an open standard protocol.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-105">AMQP enables you to build cross-platform, hybrid applications using an open standard protocol.</span></span> <span data-ttu-id="ea7ff-106">You can construct applications using components that are built using different languages and frameworks, and that run on different operating systems.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-106">You can construct applications using components that are built using different languages and frameworks, and that run on different operating systems.</span></span> <span data-ttu-id="ea7ff-107">All these components can connect to Service Bus and seamlessly exchange structured business messages efficiently and at full fidelity.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-107">All these components can connect to Service Bus and seamlessly exchange structured business messages efficiently and at full fidelity.</span></span>

## <a name="introduction-what-is-amqp-10-and-why-is-it-important"></a><span data-ttu-id="ea7ff-108">Introduction: What is AMQP 1.0 and why is it important?</span><span class="sxs-lookup"><span data-stu-id="ea7ff-108">Introduction: What is AMQP 1.0 and why is it important?</span></span>
<span data-ttu-id="ea7ff-109">Traditionally, message-oriented middleware products have used proprietary protocols for communication between client applications and brokers.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-109">Traditionally, message-oriented middleware products have used proprietary protocols for communication between client applications and brokers.</span></span> <span data-ttu-id="ea7ff-110">This means that once you've selected a particular vendor's messaging broker, you must use that vendor's libraries to connect your client applications to that broker.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-110">This means that once you've selected a particular vendor's messaging broker, you must use that vendor's libraries to connect your client applications to that broker.</span></span> <span data-ttu-id="ea7ff-111">This results in a degree of dependence on that vendor, since porting an application to a different product requires code changes in all the connected applications.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-111">This results in a degree of dependence on that vendor, since porting an application to a different product requires code changes in all the connected applications.</span></span> 

<span data-ttu-id="ea7ff-112">Furthermore, connecting messaging brokers from different vendors is tricky.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-112">Furthermore, connecting messaging brokers from different vendors is tricky.</span></span> <span data-ttu-id="ea7ff-113">This typically requires application-level bridging to move messages from one system to another and to translate between their proprietary message formats.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-113">This typically requires application-level bridging to move messages from one system to another and to translate between their proprietary message formats.</span></span> <span data-ttu-id="ea7ff-114">This is a common requirement; for example, when you must provide a new unified interface to older disparate systems, or integrate IT systems following a merger.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-114">This is a common requirement; for example, when you must provide a new unified interface to older disparate systems, or integrate IT systems following a merger.</span></span>

<span data-ttu-id="ea7ff-115">The software industry is a fast-moving business; new programming languages and application frameworks are introduced at a sometimes bewildering pace.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-115">The software industry is a fast-moving business; new programming languages and application frameworks are introduced at a sometimes bewildering pace.</span></span> <span data-ttu-id="ea7ff-116">Similarly, the requirements of IT systems evolve over time and developers want to take advantage of the latest platform features.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-116">Similarly, the requirements of IT systems evolve over time and developers want to take advantage of the latest platform features.</span></span> <span data-ttu-id="ea7ff-117">However, sometimes the selected messaging vendor does not support these platforms.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-117">However, sometimes the selected messaging vendor does not support these platforms.</span></span> <span data-ttu-id="ea7ff-118">Because messaging protocols are proprietary, it's not possible for others to provide libraries for these new platforms.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-118">Because messaging protocols are proprietary, it's not possible for others to provide libraries for these new platforms.</span></span> <span data-ttu-id="ea7ff-119">Therefore, you must use approaches such as building gateways or bridges that enable you to continue to use the messaging product.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-119">Therefore, you must use approaches such as building gateways or bridges that enable you to continue to use the messaging product.</span></span>

<span data-ttu-id="ea7ff-120">The development of the Advanced Message Queuing Protocol (AMQP) 1.0 was motivated by these issues.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-120">The development of the Advanced Message Queuing Protocol (AMQP) 1.0 was motivated by these issues.</span></span> <span data-ttu-id="ea7ff-121">It originated at JP Morgan Chase, who, like most financial services firms, are heavy users of message-oriented middleware.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-121">It originated at JP Morgan Chase, who, like most financial services firms, are heavy users of message-oriented middleware.</span></span> <span data-ttu-id="ea7ff-122">The goal was simple: to create an open-standard messaging protocol that made it possible to build message-based applications using components built using different languages, frameworks, and operating systems, all using best-of-breed components from a range of suppliers.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-122">The goal was simple: to create an open-standard messaging protocol that made it possible to build message-based applications using components built using different languages, frameworks, and operating systems, all using best-of-breed components from a range of suppliers.</span></span>

## <a name="amqp-10-technical-features"></a><span data-ttu-id="ea7ff-123">AMQP 1.0 technical features</span><span class="sxs-lookup"><span data-stu-id="ea7ff-123">AMQP 1.0 technical features</span></span>
<span data-ttu-id="ea7ff-124">AMQP 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform, messaging applications.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-124">AMQP 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform, messaging applications.</span></span> <span data-ttu-id="ea7ff-125">The protocol has a simple goal: to define the mechanics of the secure, reliable, and efficient transfer of messages between two parties.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-125">The protocol has a simple goal: to define the mechanics of the secure, reliable, and efficient transfer of messages between two parties.</span></span> <span data-ttu-id="ea7ff-126">The messages themselves are encoded using a portable data representation that enables heterogeneous senders and receivers to exchange structured business messages at full fidelity.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-126">The messages themselves are encoded using a portable data representation that enables heterogeneous senders and receivers to exchange structured business messages at full fidelity.</span></span> <span data-ttu-id="ea7ff-127">The following is a summary of the most important features:</span><span class="sxs-lookup"><span data-stu-id="ea7ff-127">The following is a summary of the most important features:</span></span>

* <span data-ttu-id="ea7ff-128">**Efficient**: AMQP 1.0 is a connection-oriented protocol that uses a binary encoding for the protocol instructions and the business messages transferred over it.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-128">**Efficient**: AMQP 1.0 is a connection-oriented protocol that uses a binary encoding for the protocol instructions and the business messages transferred over it.</span></span> <span data-ttu-id="ea7ff-129">It incorporates sophisticated flow-control schemes to maximize the utilization of the network and the connected components.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-129">It incorporates sophisticated flow-control schemes to maximize the utilization of the network and the connected components.</span></span> <span data-ttu-id="ea7ff-130">That said, the protocol was designed to strike a balance between efficiency, flexibility and interoperability.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-130">That said, the protocol was designed to strike a balance between efficiency, flexibility and interoperability.</span></span>
* <span data-ttu-id="ea7ff-131">**Reliable**: The AMQP 1.0 protocol allows messages to be exchanged with a range of reliability guarantees, from fire-and-forget to reliable, exactly-once acknowledged delivery.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-131">**Reliable**: The AMQP 1.0 protocol allows messages to be exchanged with a range of reliability guarantees, from fire-and-forget to reliable, exactly-once acknowledged delivery.</span></span>
* <span data-ttu-id="ea7ff-132">**Flexible**: AMQP 1.0 is a flexible protocol that can be used to support different topologies.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-132">**Flexible**: AMQP 1.0 is a flexible protocol that can be used to support different topologies.</span></span> <span data-ttu-id="ea7ff-133">The same protocol can be used for client-to-client, client-to-broker, and broker-to-broker communications.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-133">The same protocol can be used for client-to-client, client-to-broker, and broker-to-broker communications.</span></span>
* <span data-ttu-id="ea7ff-134">**Broker-model independent**: The AMQP 1.0 specification does not make any requirements on the messaging model used by a broker.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-134">**Broker-model independent**: The AMQP 1.0 specification does not make any requirements on the messaging model used by a broker.</span></span> <span data-ttu-id="ea7ff-135">This means that it's possible to easily add AMQP 1.0 support to existing messaging brokers.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-135">This means that it's possible to easily add AMQP 1.0 support to existing messaging brokers.</span></span>

## <a name="amqp-10-is-a-standard-with-a-capital-s"></a><span data-ttu-id="ea7ff-136">AMQP 1.0 is a Standard (with a capital 'S')</span><span class="sxs-lookup"><span data-stu-id="ea7ff-136">AMQP 1.0 is a Standard (with a capital 'S')</span></span>
<span data-ttu-id="ea7ff-137">AMQP 1.0 is an international standard, approved by ISO and IEC as ISO/IEC 19464:2014.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-137">AMQP 1.0 is an international standard, approved by ISO and IEC as ISO/IEC 19464:2014.</span></span>

<span data-ttu-id="ea7ff-138">AMQP 1.0 has been in development since 2008 by a core group of more than 20 companies, both technology suppliers and end-user firms.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-138">AMQP 1.0 has been in development since 2008 by a core group of more than 20 companies, both technology suppliers and end-user firms.</span></span> <span data-ttu-id="ea7ff-139">During that time, user firms have contributed their real-world business requirements and the technology vendors have evolved the protocol to meet those requirements.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-139">During that time, user firms have contributed their real-world business requirements and the technology vendors have evolved the protocol to meet those requirements.</span></span> <span data-ttu-id="ea7ff-140">Throughout the process, vendors have participated in workshops in which they collaborated to validate the interoperability between their implementations.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-140">Throughout the process, vendors have participated in workshops in which they collaborated to validate the interoperability between their implementations.</span></span>

<span data-ttu-id="ea7ff-141">In October 2011, the development work transitioned to a technical committee within the Organization for the Advancement of Structured Information Standards (OASIS) and the OASIS AMQP 1.0 Standard was released in October 2012.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-141">In October 2011, the development work transitioned to a technical committee within the Organization for the Advancement of Structured Information Standards (OASIS) and the OASIS AMQP 1.0 Standard was released in October 2012.</span></span> <span data-ttu-id="ea7ff-142">The following firms participated in the technical committee during the development of the standard:</span><span class="sxs-lookup"><span data-stu-id="ea7ff-142">The following firms participated in the technical committee during the development of the standard:</span></span>

* <span data-ttu-id="ea7ff-143">**Technology vendors**: Axway Software, Huawei Technologies, IIT Software, INETCO Systems, Kaazing, Microsoft, Mitre Corporation, Primeton Technologies, Progress Software, Red Hat, SITA, Software AG, Solace Systems, VMware, WSO2, Zenika.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-143">**Technology vendors**: Axway Software, Huawei Technologies, IIT Software, INETCO Systems, Kaazing, Microsoft, Mitre Corporation, Primeton Technologies, Progress Software, Red Hat, SITA, Software AG, Solace Systems, VMware, WSO2, Zenika.</span></span>
* <span data-ttu-id="ea7ff-144">**User firms**: Bank of America, Credit Suisse, Deutsche Boerse, Goldman Sachs, JPMorgan Chase.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-144">**User firms**: Bank of America, Credit Suisse, Deutsche Boerse, Goldman Sachs, JPMorgan Chase.</span></span>

<span data-ttu-id="ea7ff-145">Some of the commonly cited benefits of open standards include:</span><span class="sxs-lookup"><span data-stu-id="ea7ff-145">Some of the commonly cited benefits of open standards include:</span></span>

* <span data-ttu-id="ea7ff-146">Less chance of vendor lock-in</span><span class="sxs-lookup"><span data-stu-id="ea7ff-146">Less chance of vendor lock-in</span></span>
* <span data-ttu-id="ea7ff-147">Interoperability</span><span class="sxs-lookup"><span data-stu-id="ea7ff-147">Interoperability</span></span>
* <span data-ttu-id="ea7ff-148">Broad availability of libraries and tooling</span><span class="sxs-lookup"><span data-stu-id="ea7ff-148">Broad availability of libraries and tooling</span></span>
* <span data-ttu-id="ea7ff-149">Protection against obsolescence</span><span class="sxs-lookup"><span data-stu-id="ea7ff-149">Protection against obsolescence</span></span>
* <span data-ttu-id="ea7ff-150">Availability of knowledgeable staff</span><span class="sxs-lookup"><span data-stu-id="ea7ff-150">Availability of knowledgeable staff</span></span>
* <span data-ttu-id="ea7ff-151">Lower and manageable risk</span><span class="sxs-lookup"><span data-stu-id="ea7ff-151">Lower and manageable risk</span></span>

## <a name="amqp-10-and-service-bus"></a><span data-ttu-id="ea7ff-152">AMQP 1.0 and Service Bus</span><span class="sxs-lookup"><span data-stu-id="ea7ff-152">AMQP 1.0 and Service Bus</span></span>
<span data-ttu-id="ea7ff-153">AMQP 1.0 support in Azure Service Bus means that you can now leverage the Service Bus queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-153">AMQP 1.0 support in Azure Service Bus means that you can now leverage the Service Bus queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="ea7ff-154">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-154">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="ea7ff-155">The following figure illustrates an example deployment in which Java clients running on Linux, written using the standard Java Message Service (JMS) API and .NET clients running on Windows, exchange messages via Service Bus using AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-155">The following figure illustrates an example deployment in which Java clients running on Linux, written using the standard Java Message Service (JMS) API and .NET clients running on Windows, exchange messages via Service Bus using AMQP 1.0.</span></span>

![][0]

<span data-ttu-id="ea7ff-156">**Figure 1: Example deployment scenario showing cross-platform messaging using Service Bus and AMQP 1.0**</span><span class="sxs-lookup"><span data-stu-id="ea7ff-156">**Figure 1: Example deployment scenario showing cross-platform messaging using Service Bus and AMQP 1.0**</span></span>

<span data-ttu-id="ea7ff-157">At this time the following client libraries are known to work with Service Bus:</span><span class="sxs-lookup"><span data-stu-id="ea7ff-157">At this time the following client libraries are known to work with Service Bus:</span></span>

| <span data-ttu-id="ea7ff-158">Language</span><span class="sxs-lookup"><span data-stu-id="ea7ff-158">Language</span></span> | <span data-ttu-id="ea7ff-159">Library</span><span class="sxs-lookup"><span data-stu-id="ea7ff-159">Library</span></span> |
| --- | --- |
| <span data-ttu-id="ea7ff-160">Java</span><span class="sxs-lookup"><span data-stu-id="ea7ff-160">Java</span></span> |<span data-ttu-id="ea7ff-161">Apache Qpid Java Message Service (JMS) client</span><span class="sxs-lookup"><span data-stu-id="ea7ff-161">Apache Qpid Java Message Service (JMS) client</span></span><br/><span data-ttu-id="ea7ff-162">IIT Software SwiftMQ Java client</span><span class="sxs-lookup"><span data-stu-id="ea7ff-162">IIT Software SwiftMQ Java client</span></span> |
| <span data-ttu-id="ea7ff-163">C</span><span class="sxs-lookup"><span data-stu-id="ea7ff-163">C</span></span> |<span data-ttu-id="ea7ff-164">Apache Qpid Proton-C</span><span class="sxs-lookup"><span data-stu-id="ea7ff-164">Apache Qpid Proton-C</span></span> |
| <span data-ttu-id="ea7ff-165">PHP</span><span class="sxs-lookup"><span data-stu-id="ea7ff-165">PHP</span></span> |<span data-ttu-id="ea7ff-166">Apache Qpid Proton-PHP</span><span class="sxs-lookup"><span data-stu-id="ea7ff-166">Apache Qpid Proton-PHP</span></span> |
| <span data-ttu-id="ea7ff-167">Python</span><span class="sxs-lookup"><span data-stu-id="ea7ff-167">Python</span></span> |<span data-ttu-id="ea7ff-168">Apache Qpid Proton-Python</span><span class="sxs-lookup"><span data-stu-id="ea7ff-168">Apache Qpid Proton-Python</span></span> |
| <span data-ttu-id="ea7ff-169">C#</span><span class="sxs-lookup"><span data-stu-id="ea7ff-169">C#</span></span> |<span data-ttu-id="ea7ff-170">AMQP .Net Lite</span><span class="sxs-lookup"><span data-stu-id="ea7ff-170">AMQP .Net Lite</span></span> |

<span data-ttu-id="ea7ff-171">**Figure 2: Table of AMQP 1.0 client libraries**</span><span class="sxs-lookup"><span data-stu-id="ea7ff-171">**Figure 2: Table of AMQP 1.0 client libraries**</span></span>

## <a name="summary"></a><span data-ttu-id="ea7ff-172">Summary</span><span class="sxs-lookup"><span data-stu-id="ea7ff-172">Summary</span></span>
* <span data-ttu-id="ea7ff-173">AMQP 1.0 is an open, reliable messaging protocol that you can use to build cross-platform, hybrid applications.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-173">AMQP 1.0 is an open, reliable messaging protocol that you can use to build cross-platform, hybrid applications.</span></span> <span data-ttu-id="ea7ff-174">AMQP 1.0 is an OASIS standard.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-174">AMQP 1.0 is an OASIS standard.</span></span>
* <span data-ttu-id="ea7ff-175">AMQP 1.0 support is now available in Azure Service Bus as well as Service Bus for Windows Server (Service Bus 1.1).</span><span class="sxs-lookup"><span data-stu-id="ea7ff-175">AMQP 1.0 support is now available in Azure Service Bus as well as Service Bus for Windows Server (Service Bus 1.1).</span></span> <span data-ttu-id="ea7ff-176">Pricing is the same as for the existing protocols.</span><span class="sxs-lookup"><span data-stu-id="ea7ff-176">Pricing is the same as for the existing protocols.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea7ff-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea7ff-177">Next steps</span></span>
<span data-ttu-id="ea7ff-178">Ready to learn more?</span><span class="sxs-lookup"><span data-stu-id="ea7ff-178">Ready to learn more?</span></span> <span data-ttu-id="ea7ff-179">Visit the following links:</span><span class="sxs-lookup"><span data-stu-id="ea7ff-179">Visit the following links:</span></span>

* <span data-ttu-id="ea7ff-180">[Using Service Bus from .NET with AMQP]</span><span class="sxs-lookup"><span data-stu-id="ea7ff-180">[Using Service Bus from .NET with AMQP]</span></span>
* <span data-ttu-id="ea7ff-181">[Using Service Bus from Java with AMQP]</span><span class="sxs-lookup"><span data-stu-id="ea7ff-181">[Using Service Bus from Java with AMQP]</span></span>
* <span data-ttu-id="ea7ff-182">[Using Service Bus from Python with AMQP]</span><span class="sxs-lookup"><span data-stu-id="ea7ff-182">[Using Service Bus from Python with AMQP]</span></span>
* <span data-ttu-id="ea7ff-183">[Using Service Bus from PHP with AMQP]</span><span class="sxs-lookup"><span data-stu-id="ea7ff-183">[Using Service Bus from PHP with AMQP]</span></span>
* <span data-ttu-id="ea7ff-184">[Installing Apache Qpid Proton-C on an Azure Linux VM]</span><span class="sxs-lookup"><span data-stu-id="ea7ff-184">[Installing Apache Qpid Proton-C on an Azure Linux VM]</span></span>
* <span data-ttu-id="ea7ff-185">[AMQP in Service Bus for Windows Server]</span><span class="sxs-lookup"><span data-stu-id="ea7ff-185">[AMQP in Service Bus for Windows Server]</span></span>

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-amqp-overview/service-bus-amqp-1.png
[Using Service Bus from .NET with AMQP]: service-bus-amqp-dotnet.md
[Using Service Bus from Java with AMQP]: service-bus-amqp-java.md
[Using Service Bus from Python with AMQP]: service-bus-amqp-python.md
[Using Service Bus from PHP with AMQP]: service-bus-amqp-php.md
[Installing Apache Qpid Proton-C on an Azure Linux VM]: service-bus-amqp-apache.md
[AMQP in Service Bus for Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
