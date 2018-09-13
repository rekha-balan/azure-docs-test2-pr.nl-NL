---
title: Azure Service Bus WCF Relay tutorial | Microsoft Docs
description: Build a Service Bus client application and service using Service Bus WCF Relay.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/15/2017
ms.author: sethm
ms.openlocfilehash: 28eb74070a379f9408a3f6bea581deb7c54dc720
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554158"
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="29121-103">Azure WCF Relay tutorial</span><span class="sxs-lookup"><span data-stu-id="29121-103">Azure WCF Relay tutorial</span></span>
<span data-ttu-id="29121-104">This tutorial describes how to build a simple WCF Relay client application and service using Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="29121-104">This tutorial describes how to build a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="29121-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="29121-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="29121-106">Working through this tutorial gives you an understanding of the steps that are required to create a WCF Relay client and service application.</span><span class="sxs-lookup"><span data-stu-id="29121-106">Working through this tutorial gives you an understanding of the steps that are required to create a WCF Relay client and service application.</span></span> <span data-ttu-id="29121-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span><span class="sxs-lookup"><span data-stu-id="29121-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="29121-108">The endpoint of a service specifies an address where the service can be found, a binding that contains the information that a client must communicate with the service, and a contract that defines the functionality provided by the service to its clients.</span><span class="sxs-lookup"><span data-stu-id="29121-108">The endpoint of a service specifies an address where the service can be found, a binding that contains the information that a client must communicate with the service, and a contract that defines the functionality provided by the service to its clients.</span></span> <span data-ttu-id="29121-109">The main difference between WCF and WCF Relay is that the endpoint is exposed in the cloud instead of locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="29121-109">The main difference between WCF and WCF Relay is that the endpoint is exposed in the cloud instead of locally on your computer.</span></span>

<span data-ttu-id="29121-110">After you work through the sequence of topics in this tutorial, you will have a running service, and a client that can invoke the operations of the service.</span><span class="sxs-lookup"><span data-stu-id="29121-110">After you work through the sequence of topics in this tutorial, you will have a running service, and a client that can invoke the operations of the service.</span></span> <span data-ttu-id="29121-111">The first topic describes how to set up an account.</span><span class="sxs-lookup"><span data-stu-id="29121-111">The first topic describes how to set up an account.</span></span> <span data-ttu-id="29121-112">The next steps describe how to define a service that uses a contract, how to implement the service, and how to configure the service in code.</span><span class="sxs-lookup"><span data-stu-id="29121-112">The next steps describe how to define a service that uses a contract, how to implement the service, and how to configure the service in code.</span></span> <span data-ttu-id="29121-113">They also describe how to host and run the service.</span><span class="sxs-lookup"><span data-stu-id="29121-113">They also describe how to host and run the service.</span></span> <span data-ttu-id="29121-114">The service that is created is self-hosted and the client and service run on the same computer.</span><span class="sxs-lookup"><span data-stu-id="29121-114">The service that is created is self-hosted and the client and service run on the same computer.</span></span> <span data-ttu-id="29121-115">You can configure the service by using either code or a configuration file.</span><span class="sxs-lookup"><span data-stu-id="29121-115">You can configure the service by using either code or a configuration file.</span></span>

<span data-ttu-id="29121-116">The final three steps describe how to create a client application, configure the client application, and create and use a client that can access the functionality of the host.</span><span class="sxs-lookup"><span data-stu-id="29121-116">The final three steps describe how to create a client application, configure the client application, and create and use a client that can access the functionality of the host.</span></span>

<span data-ttu-id="29121-117">All of the topics in this section assume that you are using Visual Studio as the development environment.</span><span class="sxs-lookup"><span data-stu-id="29121-117">All of the topics in this section assume that you are using Visual Studio as the development environment.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="29121-118">Create a service namespace</span><span class="sxs-lookup"><span data-stu-id="29121-118">Create a service namespace</span></span>

<span data-ttu-id="29121-119">The first step is to create a namespace, and to obtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span><span class="sxs-lookup"><span data-stu-id="29121-119">The first step is to create a namespace, and to obtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="29121-120">A namespace provides an application boundary for each application exposed through the relay service.</span><span class="sxs-lookup"><span data-stu-id="29121-120">A namespace provides an application boundary for each application exposed through the relay service.</span></span> <span data-ttu-id="29121-121">A SAS key is automatically generated by the system when a service namespace is created.</span><span class="sxs-lookup"><span data-stu-id="29121-121">A SAS key is automatically generated by the system when a service namespace is created.</span></span> <span data-ttu-id="29121-122">The combination of service namespace and SAS key provides the credentials for Azure to authenticate access to an application.</span><span class="sxs-lookup"><span data-stu-id="29121-122">The combination of service namespace and SAS key provides the credentials for Azure to authenticate access to an application.</span></span> <span data-ttu-id="29121-123">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span><span class="sxs-lookup"><span data-stu-id="29121-123">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="29121-124">Define a WCF service contract</span><span class="sxs-lookup"><span data-stu-id="29121-124">Define a WCF service contract</span></span>
<span data-ttu-id="29121-125">The service contract specifies what operations (the web service terminology for methods or functions) the service supports.</span><span class="sxs-lookup"><span data-stu-id="29121-125">The service contract specifies what operations (the web service terminology for methods or functions) the service supports.</span></span> <span data-ttu-id="29121-126">Contracts are created by defining a C++, C#, or Visual Basic interface.</span><span class="sxs-lookup"><span data-stu-id="29121-126">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="29121-127">Each method in the interface corresponds to a specific service operation.</span><span class="sxs-lookup"><span data-stu-id="29121-127">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="29121-128">Each interface must have the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied to it, and each operation must have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied to it.</span><span class="sxs-lookup"><span data-stu-id="29121-128">Each interface must have the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied to it, and each operation must have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied to it.</span></span> <span data-ttu-id="29121-129">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span><span class="sxs-lookup"><span data-stu-id="29121-129">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="29121-130">The code for these tasks is provided in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="29121-130">The code for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="29121-131">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span><span class="sxs-lookup"><span data-stu-id="29121-131">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span></span>

### <a name="to-create-a-relay-contract-with-an-interface"></a><span data-ttu-id="29121-132">To create a relay contract with an interface</span><span class="sxs-lookup"><span data-stu-id="29121-132">To create a relay contract with an interface</span></span>
1. <span data-ttu-id="29121-133">Open Visual Studio as an administrator by right-clicking the program in the **Start** menu and selecting **Run as administrator**.</span><span class="sxs-lookup"><span data-stu-id="29121-133">Open Visual Studio as an administrator by right-clicking the program in the **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="29121-134">Create a new console application project.</span><span class="sxs-lookup"><span data-stu-id="29121-134">Create a new console application project.</span></span> <span data-ttu-id="29121-135">Click the **File** menu and select **New**, then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="29121-135">Click the **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="29121-136">In the **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span><span class="sxs-lookup"><span data-stu-id="29121-136">In the **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="29121-137">Click the **Console Application** template, and name it **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="29121-137">Click the **Console Application** template, and name it **EchoService**.</span></span> <span data-ttu-id="29121-138">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="29121-138">Click **OK** to create the project.</span></span>

    ![][2]
3. <span data-ttu-id="29121-139">Install the Service Bus NuGet package.</span><span class="sxs-lookup"><span data-stu-id="29121-139">Install the Service Bus NuGet package.</span></span> <span data-ttu-id="29121-140">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="29121-140">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="29121-141">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables you to programmatically access the basic features of WCF.</span><span class="sxs-lookup"><span data-stu-id="29121-141">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables you to programmatically access the basic features of WCF.</span></span> <span data-ttu-id="29121-142">Service Bus uses many of the objects and attributes of WCF to define service contracts.</span><span class="sxs-lookup"><span data-stu-id="29121-142">Service Bus uses many of the objects and attributes of WCF to define service contracts.</span></span>

    <span data-ttu-id="29121-143">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="29121-143">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="29121-144">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="29121-144">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="29121-145">Ensure that the project name is selected in the **Version(s)** box.</span><span class="sxs-lookup"><span data-stu-id="29121-145">Ensure that the project name is selected in the **Version(s)** box.</span></span> <span data-ttu-id="29121-146">Click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="29121-146">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="29121-147">In Solution Explorer, double-click the Program.cs file to open it in the editor, if it is not already open.</span><span class="sxs-lookup"><span data-stu-id="29121-147">In Solution Explorer, double-click the Program.cs file to open it in the editor, if it is not already open.</span></span>
5. <span data-ttu-id="29121-148">Add the following using statements at the top of the file:</span><span class="sxs-lookup"><span data-stu-id="29121-148">Add the following using statements at the top of the file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="29121-149">Change the namespace name from its default name of **EchoService** to **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="29121-149">Change the namespace name from its default name of **EchoService** to **Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="29121-150">This tutorial uses the C# namespace **Microsoft.ServiceBus.Samples**, which is the namespace of the contract managed type that is used in the configuration file in the [Configure the WCF client](#configure-the-wcf-client) step.</span><span class="sxs-lookup"><span data-stu-id="29121-150">This tutorial uses the C# namespace **Microsoft.ServiceBus.Samples**, which is the namespace of the contract managed type that is used in the configuration file in the [Configure the WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="29121-151">You can specify any namespace you want when you build this sample; however, the tutorial will not work unless you then modify the namespaces of the contract and service accordingly, in the application configuration file.</span><span class="sxs-lookup"><span data-stu-id="29121-151">You can specify any namespace you want when you build this sample; however, the tutorial will not work unless you then modify the namespaces of the contract and service accordingly, in the application configuration file.</span></span> <span data-ttu-id="29121-152">The namespace specified in the App.config file must be the same as the namespace specified in your C# files.</span><span class="sxs-lookup"><span data-stu-id="29121-152">The namespace specified in the App.config file must be the same as the namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="29121-153">Directly after the `Microsoft.ServiceBus.Samples` namespace declaration, but within the namespace, define a new interface named `IEchoContract` and apply the `ServiceContractAttribute` attribute to the interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="29121-153">Directly after the `Microsoft.ServiceBus.Samples` namespace declaration, but within the namespace, define a new interface named `IEchoContract` and apply the `ServiceContractAttribute` attribute to the interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="29121-154">The namespace value differs from the namespace that you use throughout the scope of your code.</span><span class="sxs-lookup"><span data-stu-id="29121-154">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="29121-155">Instead, the namespace value is used as a unique identifier for this contract.</span><span class="sxs-lookup"><span data-stu-id="29121-155">Instead, the namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="29121-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span><span class="sxs-lookup"><span data-stu-id="29121-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="29121-157">Typically, the service contract namespace contains a naming scheme that includes version information.</span><span class="sxs-lookup"><span data-stu-id="29121-157">Typically, the service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="29121-158">Including version information in the service contract namespace enables services to isolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span><span class="sxs-lookup"><span data-stu-id="29121-158">Including version information in the service contract namespace enables services to isolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="29121-159">In this manner, clients can continue to use the old service contract without having to be updated.</span><span class="sxs-lookup"><span data-stu-id="29121-159">In this manner, clients can continue to use the old service contract without having to be updated.</span></span> <span data-ttu-id="29121-160">Version information can consist of a date or a build number.</span><span class="sxs-lookup"><span data-stu-id="29121-160">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="29121-161">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="29121-161">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="29121-162">For the purposes of this tutorial, the naming scheme of the service contract namespace does not contain version information.</span><span class="sxs-lookup"><span data-stu-id="29121-162">For the purposes of this tutorial, the naming scheme of the service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="29121-163">Within the `IEchoContract` interface, declare a method for the single operation the `IEchoContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public WCF Relay contract.</span><span class="sxs-lookup"><span data-stu-id="29121-163">Within the `IEchoContract` interface, declare a method for the single operation the `IEchoContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public WCF Relay contract.</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="29121-164">Directly after the `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also to the `IClientChannel` interface, as shown here:</span><span class="sxs-lookup"><span data-stu-id="29121-164">Directly after the `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also to the `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="29121-165">A channel is the WCF object through which the host and client pass information to each other.</span><span class="sxs-lookup"><span data-stu-id="29121-165">A channel is the WCF object through which the host and client pass information to each other.</span></span> <span data-ttu-id="29121-166">Later, you will write code against the channel to echo information between the two applications.</span><span class="sxs-lookup"><span data-stu-id="29121-166">Later, you will write code against the channel to echo information between the two applications.</span></span>
10. <span data-ttu-id="29121-167">From the **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** to confirm the accuracy of your work so far.</span><span class="sxs-lookup"><span data-stu-id="29121-167">From the **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="29121-168">Example</span><span class="sxs-lookup"><span data-stu-id="29121-168">Example</span></span>
<span data-ttu-id="29121-169">The following code shows a basic interface that defines a WCF Relay contract.</span><span class="sxs-lookup"><span data-stu-id="29121-169">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="29121-170">Now that the interface is created, you can implement the interface.</span><span class="sxs-lookup"><span data-stu-id="29121-170">Now that the interface is created, you can implement the interface.</span></span>

## <a name="implement-the-wcf-contract"></a><span data-ttu-id="29121-171">Implement the WCF contract</span><span class="sxs-lookup"><span data-stu-id="29121-171">Implement the WCF contract</span></span>
<span data-ttu-id="29121-172">Creating an Azure relay requires that you first create the contract, which is defined by using an interface.</span><span class="sxs-lookup"><span data-stu-id="29121-172">Creating an Azure relay requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="29121-173">For more information about creating the interface, see the previous step.</span><span class="sxs-lookup"><span data-stu-id="29121-173">For more information about creating the interface, see the previous step.</span></span> <span data-ttu-id="29121-174">The next step is to implement the interface.</span><span class="sxs-lookup"><span data-stu-id="29121-174">The next step is to implement the interface.</span></span> <span data-ttu-id="29121-175">This involves creating a class named `EchoService` that implements the user-defined `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="29121-175">This involves creating a class named `EchoService` that implements the user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="29121-176">After you implement the interface, you then configure the interface using an App.config configuration file.</span><span class="sxs-lookup"><span data-stu-id="29121-176">After you implement the interface, you then configure the interface using an App.config configuration file.</span></span> <span data-ttu-id="29121-177">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span><span class="sxs-lookup"><span data-stu-id="29121-177">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="29121-178">The code used for these tasks is provided in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="29121-178">The code used for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="29121-179">For a more general discussion about how to implement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in the WCF documentation.</span><span class="sxs-lookup"><span data-stu-id="29121-179">For a more general discussion about how to implement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in the WCF documentation.</span></span>

1. <span data-ttu-id="29121-180">Create a new class named `EchoService` directly after the definition of the `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="29121-180">Create a new class named `EchoService` directly after the definition of the `IEchoContract` interface.</span></span> <span data-ttu-id="29121-181">The `EchoService` class implements the `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="29121-181">The `EchoService` class implements the `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="29121-182">Similar to other interface implementations, you can implement the definition in a different file.</span><span class="sxs-lookup"><span data-stu-id="29121-182">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="29121-183">However, for this tutorial, the implementation is located in the same file as the interface definition and the `Main` method.</span><span class="sxs-lookup"><span data-stu-id="29121-183">However, for this tutorial, the implementation is located in the same file as the interface definition and the `Main` method.</span></span>
2. <span data-ttu-id="29121-184">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="29121-184">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the `IEchoContract` interface.</span></span> <span data-ttu-id="29121-185">The attribute specifies the service name and namespace.</span><span class="sxs-lookup"><span data-stu-id="29121-185">The attribute specifies the service name and namespace.</span></span> <span data-ttu-id="29121-186">After doing so, the `EchoService` class appears as follows:</span><span class="sxs-lookup"><span data-stu-id="29121-186">After doing so, the `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="29121-187">Implement the `Echo` method defined in the `IEchoContract` interface in the `EchoService` class.</span><span class="sxs-lookup"><span data-stu-id="29121-187">Implement the `Echo` method defined in the `IEchoContract` interface in the `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="29121-188">Click **Build**, then click **Build Solution** to confirm the accuracy of your work.</span><span class="sxs-lookup"><span data-stu-id="29121-188">Click **Build**, then click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="to-define-the-configuration-for-the-service-host"></a><span data-ttu-id="29121-189">To define the configuration for the service host</span><span class="sxs-lookup"><span data-stu-id="29121-189">To define the configuration for the service host</span></span>
1. <span data-ttu-id="29121-190">The configuration file is very similar to a WCF configuration file.</span><span class="sxs-lookup"><span data-stu-id="29121-190">The configuration file is very similar to a WCF configuration file.</span></span> <span data-ttu-id="29121-191">It includes the service name, endpoint (that is, the location that Azure Relay exposes for clients and hosts to communicate with each other), and the binding (the type of protocol that is used to communicate).</span><span class="sxs-lookup"><span data-stu-id="29121-191">It includes the service name, endpoint (that is, the location that Azure Relay exposes for clients and hosts to communicate with each other), and the binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="29121-192">The main difference is that this configured service endpoint refers to a [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of the .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="29121-192">The main difference is that this configured service endpoint refers to a [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of the .NET Framework.</span></span> <span data-ttu-id="29121-193">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of the bindings defined by the service.</span><span class="sxs-lookup"><span data-stu-id="29121-193">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of the bindings defined by the service.</span></span>
2. <span data-ttu-id="29121-194">In **Solution Explorer**, double-click the App.config file to open it in the Visual Studio editor.</span><span class="sxs-lookup"><span data-stu-id="29121-194">In **Solution Explorer**, double-click the App.config file to open it in the Visual Studio editor.</span></span>
3. <span data-ttu-id="29121-195">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span><span class="sxs-lookup"><span data-stu-id="29121-195">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="29121-196">Within the `<system.serviceModel>` tags, add a `<services>` element.</span><span class="sxs-lookup"><span data-stu-id="29121-196">Within the `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="29121-197">You can define multiple relay applications in a single configuration file.</span><span class="sxs-lookup"><span data-stu-id="29121-197">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="29121-198">However, this tutorial defines only one.</span><span class="sxs-lookup"><span data-stu-id="29121-198">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="29121-199">Within the `<services>` element, add a `<service>` element to define the name of the service.</span><span class="sxs-lookup"><span data-stu-id="29121-199">Within the `<services>` element, add a `<service>` element to define the name of the service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="29121-200">Within the `<service>` element, define the location of the endpoint contract, and also the type of binding for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="29121-200">Within the `<service>` element, define the location of the endpoint contract, and also the type of binding for the endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="29121-201">The endpoint defines where the client will look for the host application.</span><span class="sxs-lookup"><span data-stu-id="29121-201">The endpoint defines where the client will look for the host application.</span></span> <span data-ttu-id="29121-202">Later, the tutorial uses this step to create a URI that fully exposes the host through Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="29121-202">Later, the tutorial uses this step to create a URI that fully exposes the host through Azure Relay.</span></span> <span data-ttu-id="29121-203">The binding declares that we are using TCP as the protocol to communicate with the relay service.</span><span class="sxs-lookup"><span data-stu-id="29121-203">The binding declares that we are using TCP as the protocol to communicate with the relay service.</span></span>
7. <span data-ttu-id="29121-204">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work.</span><span class="sxs-lookup"><span data-stu-id="29121-204">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="29121-205">Example</span><span class="sxs-lookup"><span data-stu-id="29121-205">Example</span></span>
<span data-ttu-id="29121-206">The following code shows the implementation of the service contract.</span><span class="sxs-lookup"><span data-stu-id="29121-206">The following code shows the implementation of the service contract.</span></span>

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

<span data-ttu-id="29121-207">The following code shows the basic format of the App.config file associated with the service host.</span><span class="sxs-lookup"><span data-stu-id="29121-207">The following code shows the basic format of the App.config file associated with the service host.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-to-register-with-the-relay-service"></a><span data-ttu-id="29121-208">Host and run a basic web service to register with the relay service</span><span class="sxs-lookup"><span data-stu-id="29121-208">Host and run a basic web service to register with the relay service</span></span>
<span data-ttu-id="29121-209">This step describes how to run an Azure Relay service.</span><span class="sxs-lookup"><span data-stu-id="29121-209">This step describes how to run an Azure Relay service.</span></span>

### <a name="to-create-the-relay-credentials"></a><span data-ttu-id="29121-210">To create the relay credentials</span><span class="sxs-lookup"><span data-stu-id="29121-210">To create the relay credentials</span></span>
1. <span data-ttu-id="29121-211">In `Main()`, create two variables in which to store the namespace and the SAS key that are read from the console window.</span><span class="sxs-lookup"><span data-stu-id="29121-211">In `Main()`, create two variables in which to store the namespace and the SAS key that are read from the console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="29121-212">The SAS key will be used later to access your project.</span><span class="sxs-lookup"><span data-stu-id="29121-212">The SAS key will be used later to access your project.</span></span> <span data-ttu-id="29121-213">The namespace is passed as a parameter to `CreateServiceUri` to create a service URI.</span><span class="sxs-lookup"><span data-stu-id="29121-213">The namespace is passed as a parameter to `CreateServiceUri` to create a service URI.</span></span>
2. <span data-ttu-id="29121-214">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as the credential type.</span><span class="sxs-lookup"><span data-stu-id="29121-214">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as the credential type.</span></span> <span data-ttu-id="29121-215">Add the following code directly after the code added in the last step.</span><span class="sxs-lookup"><span data-stu-id="29121-215">Add the following code directly after the code added in the last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="29121-216">To create a base address for the service</span><span class="sxs-lookup"><span data-stu-id="29121-216">To create a base address for the service</span></span>
<span data-ttu-id="29121-217">After the code you added in the last step, create a `Uri` instance for the base address of the service.</span><span class="sxs-lookup"><span data-stu-id="29121-217">After the code you added in the last step, create a `Uri` instance for the base address of the service.</span></span> <span data-ttu-id="29121-218">This URI specifies the Service Bus scheme, the namespace, and the path of the service interface.</span><span class="sxs-lookup"><span data-stu-id="29121-218">This URI specifies the Service Bus scheme, the namespace, and the path of the service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="29121-219">"sb" is an abbreviation for the Service Bus scheme, and indicates that we are using TCP as the protocol.</span><span class="sxs-lookup"><span data-stu-id="29121-219">"sb" is an abbreviation for the Service Bus scheme, and indicates that we are using TCP as the protocol.</span></span> <span data-ttu-id="29121-220">This was also previously indicated in the configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as the binding.</span><span class="sxs-lookup"><span data-stu-id="29121-220">This was also previously indicated in the configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as the binding.</span></span>

<span data-ttu-id="29121-221">For this tutorial, the URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="29121-221">For this tutorial, the URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="to-create-and-configure-the-service-host"></a><span data-ttu-id="29121-222">To create and configure the service host</span><span class="sxs-lookup"><span data-stu-id="29121-222">To create and configure the service host</span></span>
1. <span data-ttu-id="29121-223">Set the connectivity mode to `AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="29121-223">Set the connectivity mode to `AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="29121-224">The connectivity mode describes the protocol the service uses to communicate with the relay service; either HTTP or TCP.</span><span class="sxs-lookup"><span data-stu-id="29121-224">The connectivity mode describes the protocol the service uses to communicate with the relay service; either HTTP or TCP.</span></span> <span data-ttu-id="29121-225">Using the default setting `AutoDetect`, the service attempts to connect to Azure Relay over TCP if it is available, and HTTP if TCP is not available.</span><span class="sxs-lookup"><span data-stu-id="29121-225">Using the default setting `AutoDetect`, the service attempts to connect to Azure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="29121-226">Note that this differs from the protocol the service specifies for client communication.</span><span class="sxs-lookup"><span data-stu-id="29121-226">Note that this differs from the protocol the service specifies for client communication.</span></span> <span data-ttu-id="29121-227">That protocol is determined by the binding used.</span><span class="sxs-lookup"><span data-stu-id="29121-227">That protocol is determined by the binding used.</span></span> <span data-ttu-id="29121-228">For example, a service can use the [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span><span class="sxs-lookup"><span data-stu-id="29121-228">For example, a service can use the [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="29121-229">That same service could specify **ConnectivityMode.AutoDetect** so that the service communicates with Azure Relay over TCP.</span><span class="sxs-lookup"><span data-stu-id="29121-229">That same service could specify **ConnectivityMode.AutoDetect** so that the service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="29121-230">Create the service host, using the URI created earlier in this section.</span><span class="sxs-lookup"><span data-stu-id="29121-230">Create the service host, using the URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="29121-231">The service host is the WCF object that instantiates the service.</span><span class="sxs-lookup"><span data-stu-id="29121-231">The service host is the WCF object that instantiates the service.</span></span> <span data-ttu-id="29121-232">Here, you pass it the type of service you want to create (an `EchoService` type), and also to the address at which you want to expose the service.</span><span class="sxs-lookup"><span data-stu-id="29121-232">Here, you pass it the type of service you want to create (an `EchoService` type), and also to the address at which you want to expose the service.</span></span>
3. <span data-ttu-id="29121-233">At the top of the Program.cs file, add references to [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="29121-233">At the top of the Program.cs file, add references to [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="29121-234">Back in `Main()`, configure the endpoint to enable public access.</span><span class="sxs-lookup"><span data-stu-id="29121-234">Back in `Main()`, configure the endpoint to enable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="29121-235">This step informs the relay service that your application can be found publicly by examining the ATOM feed for your project.</span><span class="sxs-lookup"><span data-stu-id="29121-235">This step informs the relay service that your application can be found publicly by examining the ATOM feed for your project.</span></span> <span data-ttu-id="29121-236">If you set **DiscoveryType** to **private**, a client would still be able to access the service.</span><span class="sxs-lookup"><span data-stu-id="29121-236">If you set **DiscoveryType** to **private**, a client would still be able to access the service.</span></span> <span data-ttu-id="29121-237">However, the service would not appear when it searches the Relay namespace.</span><span class="sxs-lookup"><span data-stu-id="29121-237">However, the service would not appear when it searches the Relay namespace.</span></span> <span data-ttu-id="29121-238">Instead, the client would have to know the endpoint path beforehand.</span><span class="sxs-lookup"><span data-stu-id="29121-238">Instead, the client would have to know the endpoint path beforehand.</span></span>
5. <span data-ttu-id="29121-239">Apply the service credentials to the service endpoints defined in the App.config file:</span><span class="sxs-lookup"><span data-stu-id="29121-239">Apply the service credentials to the service endpoints defined in the App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="29121-240">As stated in the previous step, you could have declared multiple services and endpoints in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="29121-240">As stated in the previous step, you could have declared multiple services and endpoints in the configuration file.</span></span> <span data-ttu-id="29121-241">If you had, this code would traverse the configuration file and search for every endpoint to which it should apply your credentials.</span><span class="sxs-lookup"><span data-stu-id="29121-241">If you had, this code would traverse the configuration file and search for every endpoint to which it should apply your credentials.</span></span> <span data-ttu-id="29121-242">However, for this tutorial, the configuration file has only one endpoint.</span><span class="sxs-lookup"><span data-stu-id="29121-242">However, for this tutorial, the configuration file has only one endpoint.</span></span>

### <a name="to-open-the-service-host"></a><span data-ttu-id="29121-243">To open the service host</span><span class="sxs-lookup"><span data-stu-id="29121-243">To open the service host</span></span>
1. <span data-ttu-id="29121-244">Open the service.</span><span class="sxs-lookup"><span data-stu-id="29121-244">Open the service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="29121-245">Inform the user that the service is running, and explain how to shut down the service.</span><span class="sxs-lookup"><span data-stu-id="29121-245">Inform the user that the service is running, and explain how to shut down the service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="29121-246">When finished, close the service host.</span><span class="sxs-lookup"><span data-stu-id="29121-246">When finished, close the service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="29121-247">Press **Ctrl+Shift+B** to build the project.</span><span class="sxs-lookup"><span data-stu-id="29121-247">Press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="example"></a><span data-ttu-id="29121-248">Example</span><span class="sxs-lookup"><span data-stu-id="29121-248">Example</span></span>
<span data-ttu-id="29121-249">The following example includes the service contract and implementation from previous steps in the tutorial, and hosts the service in a console application.</span><span class="sxs-lookup"><span data-stu-id="29121-249">The following example includes the service contract and implementation from previous steps in the tutorial, and hosts the service in a console application.</span></span> <span data-ttu-id="29121-250">Compile the following into an executable named EchoService.exe.</span><span class="sxs-lookup"><span data-stu-id="29121-250">Compile the following into an executable named EchoService.exe.</span></span>

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create the credentials object for the endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create the service URI based on the service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create the service host reading the configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create the ServiceRegistrySettings behavior for the endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add the Relay credentials to all endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open the service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            // Close the service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-the-service-contract"></a><span data-ttu-id="29121-251">Create a WCF client for the service contract</span><span class="sxs-lookup"><span data-stu-id="29121-251">Create a WCF client for the service contract</span></span>
<span data-ttu-id="29121-252">The next step is to create a client application and define the service contract you will implement in later steps.</span><span class="sxs-lookup"><span data-stu-id="29121-252">The next step is to create a client application and define the service contract you will implement in later steps.</span></span> <span data-ttu-id="29121-253">Note that many of these steps resemble the steps used to create a service: defining a contract, editing an App.config file, using credentials to connect to the relay service, and so on.</span><span class="sxs-lookup"><span data-stu-id="29121-253">Note that many of these steps resemble the steps used to create a service: defining a contract, editing an App.config file, using credentials to connect to the relay service, and so on.</span></span> <span data-ttu-id="29121-254">The code used for these tasks is provided in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="29121-254">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="29121-255">Create a new project in the current Visual Studio solution for the client by doing the following:</span><span class="sxs-lookup"><span data-stu-id="29121-255">Create a new project in the current Visual Studio solution for the client by doing the following:</span></span>

   1. <span data-ttu-id="29121-256">In Solution Explorer, in the same solution that contains the service, right-click the current solution (not the project), and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="29121-256">In Solution Explorer, in the same solution that contains the service, right-click the current solution (not the project), and click **Add**.</span></span> <span data-ttu-id="29121-257">Then click **New Project**.</span><span class="sxs-lookup"><span data-stu-id="29121-257">Then click **New Project**.</span></span>
   2. <span data-ttu-id="29121-258">In the **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select the **Console Application** template, and name it **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="29121-258">In the **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select the **Console Application** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="29121-259">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="29121-259">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="29121-260">In Solution Explorer, double-click the Program.cs file in the **EchoClient** project to open it in the editor, if it is not already open.</span><span class="sxs-lookup"><span data-stu-id="29121-260">In Solution Explorer, double-click the Program.cs file in the **EchoClient** project to open it in the editor, if it is not already open.</span></span>
3. <span data-ttu-id="29121-261">Change the namespace name from its default name of `EchoClient` to `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="29121-261">Change the namespace name from its default name of `EchoClient` to `Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="29121-262">Install the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click the **EchoClient** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="29121-262">Install the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click the **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="29121-263">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="29121-263">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="29121-264">Click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="29121-264">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="29121-265">Add a `using` statement for the [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="29121-265">Add a `using` statement for the [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in the Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="29121-266">Add the service contract definition to the namespace, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="29121-266">Add the service contract definition to the namespace, as shown in the following example.</span></span> <span data-ttu-id="29121-267">Note that this definition is identical to the definition used in the **Service** project.</span><span class="sxs-lookup"><span data-stu-id="29121-267">Note that this definition is identical to the definition used in the **Service** project.</span></span> <span data-ttu-id="29121-268">You should add this code at the top of the `Microsoft.ServiceBus.Samples` namespace.</span><span class="sxs-lookup"><span data-stu-id="29121-268">You should add this code at the top of the `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="29121-269">Press **Ctrl+Shift+B** to build the client.</span><span class="sxs-lookup"><span data-stu-id="29121-269">Press **Ctrl+Shift+B** to build the client.</span></span>

### <a name="example"></a><span data-ttu-id="29121-270">Example</span><span class="sxs-lookup"><span data-stu-id="29121-270">Example</span></span>
<span data-ttu-id="29121-271">The following code shows the current status of the Program.cs file in the **EchoClient** project.</span><span class="sxs-lookup"><span data-stu-id="29121-271">The following code shows the current status of the Program.cs file in the **EchoClient** project.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-the-wcf-client"></a><span data-ttu-id="29121-272">Configure the WCF client</span><span class="sxs-lookup"><span data-stu-id="29121-272">Configure the WCF client</span></span>
<span data-ttu-id="29121-273">In this step, you create an App.config file for a basic client application that accesses the service created previously in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="29121-273">In this step, you create an App.config file for a basic client application that accesses the service created previously in this tutorial.</span></span> <span data-ttu-id="29121-274">This App.config file defines the contract, binding, and name of the endpoint.</span><span class="sxs-lookup"><span data-stu-id="29121-274">This App.config file defines the contract, binding, and name of the endpoint.</span></span> <span data-ttu-id="29121-275">The code used for these tasks is provided in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="29121-275">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="29121-276">In Solution Explorer, in the **EchoClient** project, double-click **App.config** to open the file in the Visual Studio editor.</span><span class="sxs-lookup"><span data-stu-id="29121-276">In Solution Explorer, in the **EchoClient** project, double-click **App.config** to open the file in the Visual Studio editor.</span></span>
2. <span data-ttu-id="29121-277">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span><span class="sxs-lookup"><span data-stu-id="29121-277">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="29121-278">Within the system.serviceModel element, add a `<client>` element.</span><span class="sxs-lookup"><span data-stu-id="29121-278">Within the system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="29121-279">This step declares that you are defining a WCF-style client application.</span><span class="sxs-lookup"><span data-stu-id="29121-279">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="29121-280">Within the `client` element, define the name, contract, and binding type for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="29121-280">Within the `client` element, define the name, contract, and binding type for the endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="29121-281">This step defines the name of the endpoint, the contract defined in the service, and the fact that the client application uses TCP to communicate with Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="29121-281">This step defines the name of the endpoint, the contract defined in the service, and the fact that the client application uses TCP to communicate with Azure Relay.</span></span> <span data-ttu-id="29121-282">The endpoint name is used in the next step to link this endpoint configuration with the service URI.</span><span class="sxs-lookup"><span data-stu-id="29121-282">The endpoint name is used in the next step to link this endpoint configuration with the service URI.</span></span>
5. <span data-ttu-id="29121-283">Click **File**, then click **Save All**.</span><span class="sxs-lookup"><span data-stu-id="29121-283">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="29121-284">Example</span><span class="sxs-lookup"><span data-stu-id="29121-284">Example</span></span>
<span data-ttu-id="29121-285">The following code shows the App.config file for the Echo client.</span><span class="sxs-lookup"><span data-stu-id="29121-285">The following code shows the App.config file for the Echo client.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-the-wcf-client"></a><span data-ttu-id="29121-286">Implement the WCF client</span><span class="sxs-lookup"><span data-stu-id="29121-286">Implement the WCF client</span></span>
<span data-ttu-id="29121-287">In this step, you implement a basic client application that accesses the service you created previously in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="29121-287">In this step, you implement a basic client application that accesses the service you created previously in this tutorial.</span></span> <span data-ttu-id="29121-288">Similar to the service, the client performs many of the same operations to access Azure Relay:</span><span class="sxs-lookup"><span data-stu-id="29121-288">Similar to the service, the client performs many of the same operations to access Azure Relay:</span></span>

1. <span data-ttu-id="29121-289">Sets the connectivity mode.</span><span class="sxs-lookup"><span data-stu-id="29121-289">Sets the connectivity mode.</span></span>
2. <span data-ttu-id="29121-290">Creates the URI that locates the host service.</span><span class="sxs-lookup"><span data-stu-id="29121-290">Creates the URI that locates the host service.</span></span>
3. <span data-ttu-id="29121-291">Defines the security credentials.</span><span class="sxs-lookup"><span data-stu-id="29121-291">Defines the security credentials.</span></span>
4. <span data-ttu-id="29121-292">Applies the credentials to the connection.</span><span class="sxs-lookup"><span data-stu-id="29121-292">Applies the credentials to the connection.</span></span>
5. <span data-ttu-id="29121-293">Opens the connection.</span><span class="sxs-lookup"><span data-stu-id="29121-293">Opens the connection.</span></span>
6. <span data-ttu-id="29121-294">Performs the application-specific tasks.</span><span class="sxs-lookup"><span data-stu-id="29121-294">Performs the application-specific tasks.</span></span>
7. <span data-ttu-id="29121-295">Closes the connection.</span><span class="sxs-lookup"><span data-stu-id="29121-295">Closes the connection.</span></span>

<span data-ttu-id="29121-296">However, one of the main differences is that the client application uses a channel to connect to the relay service, whereas the service uses a call to **ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="29121-296">However, one of the main differences is that the client application uses a channel to connect to the relay service, whereas the service uses a call to **ServiceHost**.</span></span> <span data-ttu-id="29121-297">The code used for these tasks is provided in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="29121-297">The code used for these tasks is provided in the example following the procedure.</span></span>

### <a name="to-implement-a-client-application"></a><span data-ttu-id="29121-298">To implement a client application</span><span class="sxs-lookup"><span data-stu-id="29121-298">To implement a client application</span></span>
1. <span data-ttu-id="29121-299">Set the connectivity mode to **AutoDetect**.</span><span class="sxs-lookup"><span data-stu-id="29121-299">Set the connectivity mode to **AutoDetect**.</span></span> <span data-ttu-id="29121-300">Add the following code inside the `Main()` method of the **EchoClient** application.</span><span class="sxs-lookup"><span data-stu-id="29121-300">Add the following code inside the `Main()` method of the **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="29121-301">Define variables to hold the values for the service namespace, and SAS key that are read from the console.</span><span class="sxs-lookup"><span data-stu-id="29121-301">Define variables to hold the values for the service namespace, and SAS key that are read from the console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="29121-302">Create the URI that defines the location of the host in your Relay project.</span><span class="sxs-lookup"><span data-stu-id="29121-302">Create the URI that defines the location of the host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="29121-303">Create the credential object for your service namespace endpoint.</span><span class="sxs-lookup"><span data-stu-id="29121-303">Create the credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="29121-304">Create the channel factory that loads the configuration described in the App.config file.</span><span class="sxs-lookup"><span data-stu-id="29121-304">Create the channel factory that loads the configuration described in the App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="29121-305">A channel factory is a WCF object that creates a channel through which the service and client applications communicate.</span><span class="sxs-lookup"><span data-stu-id="29121-305">A channel factory is a WCF object that creates a channel through which the service and client applications communicate.</span></span>
6. <span data-ttu-id="29121-306">Apply the credentials.</span><span class="sxs-lookup"><span data-stu-id="29121-306">Apply the credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="29121-307">Create and open the channel to the service.</span><span class="sxs-lookup"><span data-stu-id="29121-307">Create and open the channel to the service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="29121-308">Write the basic user interface and functionality for the echo.</span><span class="sxs-lookup"><span data-stu-id="29121-308">Write the basic user interface and functionality for the echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text to echo (or [Enter] to exit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    <span data-ttu-id="29121-309">Note that the code uses the instance of the channel object as a proxy for the service.</span><span class="sxs-lookup"><span data-stu-id="29121-309">Note that the code uses the instance of the channel object as a proxy for the service.</span></span>
9. <span data-ttu-id="29121-310">Close the channel, and close the factory.</span><span class="sxs-lookup"><span data-stu-id="29121-310">Close the channel, and close the factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="to-run-the-applications"></a><span data-ttu-id="29121-311">To run the applications</span><span class="sxs-lookup"><span data-stu-id="29121-311">To run the applications</span></span>
1. <span data-ttu-id="29121-312">Press **Ctrl+Shift+B** to build the solution.</span><span class="sxs-lookup"><span data-stu-id="29121-312">Press **Ctrl+Shift+B** to build the solution.</span></span> <span data-ttu-id="29121-313">This builds both the client project and the service project that you created in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="29121-313">This builds both the client project and the service project that you created in the previous steps.</span></span>
2. <span data-ttu-id="29121-314">Before running the client application, you must make sure that the service application is running.</span><span class="sxs-lookup"><span data-stu-id="29121-314">Before running the client application, you must make sure that the service application is running.</span></span> <span data-ttu-id="29121-315">In Solution Explorer in Visual Studio, right-click the **EchoService** solution, then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="29121-315">In Solution Explorer in Visual Studio, right-click the **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="29121-316">In the solution properties dialog box, click **Startup Project**, then click the **Multiple startup projects** button.</span><span class="sxs-lookup"><span data-stu-id="29121-316">In the solution properties dialog box, click **Startup Project**, then click the **Multiple startup projects** button.</span></span> <span data-ttu-id="29121-317">Make sure **EchoService** appears first in the list.</span><span class="sxs-lookup"><span data-stu-id="29121-317">Make sure **EchoService** appears first in the list.</span></span>
4. <span data-ttu-id="29121-318">Set the **Action** box for both the **EchoService** and **EchoClient** projects to **Start**.</span><span class="sxs-lookup"><span data-stu-id="29121-318">Set the **Action** box for both the **EchoService** and **EchoClient** projects to **Start**.</span></span>

    ![][5]
5. <span data-ttu-id="29121-319">Click **Project Dependencies**.</span><span class="sxs-lookup"><span data-stu-id="29121-319">Click **Project Dependencies**.</span></span> <span data-ttu-id="29121-320">In the **Projects** box, select **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="29121-320">In the **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="29121-321">In the **Depends on** box, make sure **EchoService** is checked.</span><span class="sxs-lookup"><span data-stu-id="29121-321">In the **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="29121-322">Click **OK** to dismiss the **Properties** dialog.</span><span class="sxs-lookup"><span data-stu-id="29121-322">Click **OK** to dismiss the **Properties** dialog.</span></span>
7. <span data-ttu-id="29121-323">Press **F5** to run both projects.</span><span class="sxs-lookup"><span data-stu-id="29121-323">Press **F5** to run both projects.</span></span>
8. <span data-ttu-id="29121-324">Both console windows open and prompt you for the namespace name.</span><span class="sxs-lookup"><span data-stu-id="29121-324">Both console windows open and prompt you for the namespace name.</span></span> <span data-ttu-id="29121-325">The service must run first, so in the **EchoService** console window, enter the namespace and then press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="29121-325">The service must run first, so in the **EchoService** console window, enter the namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="29121-326">Next, you are prompted for your SAS key.</span><span class="sxs-lookup"><span data-stu-id="29121-326">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="29121-327">Enter the SAS key and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="29121-327">Enter the SAS key and press ENTER.</span></span>

    <span data-ttu-id="29121-328">Here is example output from the console window.</span><span class="sxs-lookup"><span data-stu-id="29121-328">Here is example output from the console window.</span></span> <span data-ttu-id="29121-329">Note that the values provided here are for example purposes only.</span><span class="sxs-lookup"><span data-stu-id="29121-329">Note that the values provided here are for example purposes only.</span></span>

    <span data-ttu-id="29121-330">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="29121-330">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="29121-331">The service application prints to the console window the address on which it's listening, as seen in the following example.</span><span class="sxs-lookup"><span data-stu-id="29121-331">The service application prints to the console window the address on which it's listening, as seen in the following example.</span></span>

    <span data-ttu-id="29121-332">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span><span class="sxs-lookup"><span data-stu-id="29121-332">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span></span>
10. <span data-ttu-id="29121-333">In the **EchoClient** console window, enter the same information that you entered previously for the service application.</span><span class="sxs-lookup"><span data-stu-id="29121-333">In the **EchoClient** console window, enter the same information that you entered previously for the service application.</span></span> <span data-ttu-id="29121-334">Follow the previous steps to enter the same service namespace and SAS key values for the client application.</span><span class="sxs-lookup"><span data-stu-id="29121-334">Follow the previous steps to enter the same service namespace and SAS key values for the client application.</span></span>
11. <span data-ttu-id="29121-335">After entering these values, the client opens a channel to the service and prompts you to enter some text as seen in the following console output example.</span><span class="sxs-lookup"><span data-stu-id="29121-335">After entering these values, the client opens a channel to the service and prompts you to enter some text as seen in the following console output example.</span></span>

    `Enter text to echo (or [Enter] to exit):`

    <span data-ttu-id="29121-336">Enter some text to send to the service application and press Enter.</span><span class="sxs-lookup"><span data-stu-id="29121-336">Enter some text to send to the service application and press Enter.</span></span> <span data-ttu-id="29121-337">This text is sent to the service through the Echo service operation and appears in the service console window as in the following example output.</span><span class="sxs-lookup"><span data-stu-id="29121-337">This text is sent to the service through the Echo service operation and appears in the service console window as in the following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="29121-338">The client application receives the return value of the `Echo` operation, which is the original text, and prints it to its console window.</span><span class="sxs-lookup"><span data-stu-id="29121-338">The client application receives the return value of the `Echo` operation, which is the original text, and prints it to its console window.</span></span> <span data-ttu-id="29121-339">The following is example output from the client console window.</span><span class="sxs-lookup"><span data-stu-id="29121-339">The following is example output from the client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="29121-340">You can continue sending text messages from the client to the service in this manner.</span><span class="sxs-lookup"><span data-stu-id="29121-340">You can continue sending text messages from the client to the service in this manner.</span></span> <span data-ttu-id="29121-341">When you are finished, press Enter in the client and service console windows to end both applications.</span><span class="sxs-lookup"><span data-stu-id="29121-341">When you are finished, press Enter in the client and service console windows to end both applications.</span></span>

## <a name="example"></a><span data-ttu-id="29121-342">Example</span><span class="sxs-lookup"><span data-stu-id="29121-342">Example</span></span>
<span data-ttu-id="29121-343">The following example shows how to create a client application, how to call the operations of the service, and how to close the client after the operation call is finished.</span><span class="sxs-lookup"><span data-stu-id="29121-343">The following example shows how to create a client application, how to call the operations of the service, and how to close the client after the operation call is finished.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text to echo (or [Enter] to exit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="29121-344">Next steps</span><span class="sxs-lookup"><span data-stu-id="29121-344">Next steps</span></span>
<span data-ttu-id="29121-345">This tutorial showed how to build an Azure Relay client application and service using the WCF Relay capabilities of Service Bus.</span><span class="sxs-lookup"><span data-stu-id="29121-345">This tutorial showed how to build an Azure Relay client application and service using the WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="29121-346">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="29121-346">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="29121-347">To learn more about Azure Relay, see the following topics.</span><span class="sxs-lookup"><span data-stu-id="29121-347">To learn more about Azure Relay, see the following topics.</span></span>

* [<span data-ttu-id="29121-348">Azure Service Bus architectural overview</span><span class="sxs-lookup"><span data-stu-id="29121-348">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="29121-349">Azure Relay overview</span><span class="sxs-lookup"><span data-stu-id="29121-349">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="29121-350">How to use the WCF relay service with .NET</span><span class="sxs-lookup"><span data-stu-id="29121-350">How to use the WCF relay service with .NET</span></span>](service-bus-dotnet-how-to-use-relay.md)

[Azure classic portal]: http://manage.windowsazure.com

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-relay/media/service-bus-relay-tutorial/service-bus-policies.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-relay/media/service-bus-relay-tutorial/create-console-app.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-relay/media/service-bus-relay-tutorial/install-nuget.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-relay/media/service-bus-relay-tutorial/create-ns.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-relay/media/service-bus-relay-tutorial/set-projects.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-relay/media/service-bus-relay-tutorial/set-depend.png






