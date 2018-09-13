---
title: REST tutorial using Azure Relay | Microsoft Docs
description: Build a simple Azure Service Bus Relay host application that exposes a REST-based interface.
services: service-bus-relay
documentationcenter: na
author: spelluru
manager: timlt
editor: ''
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/06/2017
ms.author: spelluru
ms.openlocfilehash: fa5b4ba02eda75d16243c9aebbf38dfb30afe53d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800571"
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="d0d8d-103">Azure WCF Relay REST tutorial</span><span class="sxs-lookup"><span data-stu-id="d0d8d-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="d0d8d-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="d0d8d-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="d0d8d-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Azure Relay.</span></span> <span data-ttu-id="d0d8d-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="d0d8d-108">Step 1: Create a namespace</span><span class="sxs-lookup"><span data-stu-id="d0d8d-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="d0d8d-109">To begin using the relay features in Azure, you must first create a service namespace.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="d0d8d-110">A namespace provides a scoping container for addressing Azure resources within your application.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="d0d8d-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="d0d8d-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span><span class="sxs-lookup"><span data-stu-id="d0d8d-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>

<span data-ttu-id="d0d8d-113">When you create a WCF REST-style service, you must define the contract.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="d0d8d-114">The contract specifies what operations the host supports.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="d0d8d-115">A service operation can be thought of as a web service method.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="d0d8d-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="d0d8d-117">Each method in the interface corresponds to a specific service operation.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="d0d8d-118">The [ServiceContractAttribute](/dotnet/api/system.servicemodel.servicecontractattribute) attribute must be applied to each interface, and the [OperationContractAttribute](/dotnet/api/system.servicemodel.operationcontractattribute) attribute must be applied to each operation.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-118">The [ServiceContractAttribute](/dotnet/api/system.servicemodel.servicecontractattribute) attribute must be applied to each interface, and the [OperationContractAttribute](/dotnet/api/system.servicemodel.operationcontractattribute) attribute must be applied to each operation.</span></span> <span data-ttu-id="d0d8d-119">If a method in an interface that has the [ServiceContractAttribute](/dotnet/api/system.servicemodel.servicecontractattribute) does not have the [OperationContractAttribute](/dotnet/api/system.servicemodel.operationcontractattribute), that method is not exposed.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-119">If a method in an interface that has the [ServiceContractAttribute](/dotnet/api/system.servicemodel.servicecontractattribute) does not have the [OperationContractAttribute](/dotnet/api/system.servicemodel.operationcontractattribute), that method is not exposed.</span></span> <span data-ttu-id="d0d8d-120">The code used for these tasks is shown in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="d0d8d-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](/dotnet/api/system.servicemodel.operationcontractattribute): [WebGetAttribute](/dotnet/api/system.servicemodel.web.webgetattribute).</span><span class="sxs-lookup"><span data-stu-id="d0d8d-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](/dotnet/api/system.servicemodel.operationcontractattribute): [WebGetAttribute](/dotnet/api/system.servicemodel.web.webgetattribute).</span></span> <span data-ttu-id="d0d8d-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="d0d8d-123">This example uses the [WebGetAttribute](/dotnet/api/system.servicemodel.web.webgetattribute) attribute to link a method to HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-123">This example uses the [WebGetAttribute](/dotnet/api/system.servicemodel.web.webgetattribute) attribute to link a method to HTTP GET.</span></span> <span data-ttu-id="d0d8d-124">This enables Service Bus to accurately retrieve and interpret commands sent to the interface.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-124">This enables Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="d0d8d-125">To create a contract with an interface</span><span class="sxs-lookup"><span data-stu-id="d0d8d-125">To create a contract with an interface</span></span>

1. <span data-ttu-id="d0d8d-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="d0d8d-127">Create a new console application project.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-127">Create a new console application project.</span></span> <span data-ttu-id="d0d8d-128">Click the **File** menu and select **New**, then select **Project**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="d0d8d-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="d0d8d-130">Use the default **Location**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-130">Use the default **Location**.</span></span> <span data-ttu-id="d0d8d-131">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="d0d8d-132">For a C# project, Visual Studio creates a `Program.cs` file.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="d0d8d-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="d0d8d-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="d0d8d-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="d0d8d-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="d0d8d-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="d0d8d-138">Click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="d0d8d-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span><span class="sxs-lookup"><span data-stu-id="d0d8d-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="d0d8d-140">a.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-140">a.</span></span> <span data-ttu-id="d0d8d-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="d0d8d-142">b.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-142">b.</span></span> <span data-ttu-id="d0d8d-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="d0d8d-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="d0d8d-145">Add the following `using` statements at the top of the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="d0d8d-146">[System.ServiceModel](/dotnet/api/system.servicemodel) is the namespace that enables programmatic access to basic features of WCF.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-146">[System.ServiceModel](/dotnet/api/system.servicemodel) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="d0d8d-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="d0d8d-148">You use this namespace in most of your relay applications.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-148">You use this namespace in most of your relay applications.</span></span> <span data-ttu-id="d0d8d-149">Similarly, [System.ServiceModel.Channels](/dotnet/api/system.servicemodel.channels) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-149">Similarly, [System.ServiceModel.Channels](/dotnet/api/system.servicemodel.channels) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="d0d8d-150">Finally, [System.ServiceModel.Web](/dotnet/api/system.servicemodel.web) contains the types that enable you to create web-based applications.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-150">Finally, [System.ServiceModel.Web](/dotnet/api/system.servicemodel.web) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="d0d8d-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="d0d8d-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="d0d8d-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="d0d8d-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="d0d8d-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="d0d8d-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="d0d8d-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="d0d8d-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="d0d8d-158">In the **OperationContract** attribute, add the **WebGet** value.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="d0d8d-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="d0d8d-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="d0d8d-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="d0d8d-162">A channel is the WCF object through which the service and client pass information to each other.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="d0d8d-163">Later, you create the channel in your host application.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-163">Later, you create the channel in your host application.</span></span> <span data-ttu-id="d0d8d-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="d0d8d-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="d0d8d-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="d0d8d-167">Example</span><span class="sxs-lookup"><span data-stu-id="d0d8d-167">Example</span></span>
<span data-ttu-id="d0d8d-168">The following code shows a basic interface that defines a WCF Relay contract.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="d0d8d-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span><span class="sxs-lookup"><span data-stu-id="d0d8d-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="d0d8d-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="d0d8d-171">The next step is to implement the interface.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-171">The next step is to implement the interface.</span></span> <span data-ttu-id="d0d8d-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="d0d8d-173">After you implement the contract, you then configure the interface using an App.config file.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="d0d8d-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="d0d8d-175">The code used for these tasks is provided in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="d0d8d-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="d0d8d-177">To implement a REST-style Service Bus contract</span><span class="sxs-lookup"><span data-stu-id="d0d8d-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="d0d8d-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="d0d8d-179">The **ImageService** class implements the **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="d0d8d-180">Similar to other interface implementations, you can implement the definition in a different file.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="d0d8d-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="d0d8d-182">Apply the [ServiceBehaviorAttribute](/dotnet/api/system.servicemodel.servicebehaviorattribute) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-182">Apply the [ServiceBehaviorAttribute](/dotnet/api/system.servicemodel.servicebehaviorattribute) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="d0d8d-183">As mentioned previously, this namespace is not a traditional namespace.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="d0d8d-184">Instead, it is part of the WCF architecture that identifies the contract.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="d0d8d-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) article in the WCF documentation.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) article in the WCF documentation.</span></span>
3. <span data-ttu-id="d0d8d-186">Add a .jpg image to your project.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="d0d8d-187">This is a picture that the service displays in the receiving browser.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="d0d8d-188">Right-click your project, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="d0d8d-189">Then click **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-189">Then click **Existing Item**.</span></span> <span data-ttu-id="d0d8d-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="d0d8d-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="d0d8d-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span><span class="sxs-lookup"><span data-stu-id="d0d8d-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="d0d8d-193">If you have a different file, you must rename the image, or change your code to compensate.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-193">If you have a different file, you must rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="d0d8d-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="d0d8d-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="d0d8d-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="d0d8d-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. <span data-ttu-id="d0d8d-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    <span data-ttu-id="d0d8d-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="d0d8d-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="d0d8d-201">From the **Build** menu, click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="d0d8d-202">To define the configuration for running the web service on Service Bus</span><span class="sxs-lookup"><span data-stu-id="d0d8d-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="d0d8d-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="d0d8d-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span><span class="sxs-lookup"><span data-stu-id="d0d8d-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="d0d8d-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="d0d8d-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="d0d8d-207">Here, it is used to define the service name and endpoint.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="d0d8d-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="d0d8d-209">This defines the bindings used in the application.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="d0d8d-210">You can define multiple bindings, but for this tutorial you are defining only one.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    <span data-ttu-id="d0d8d-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="d0d8d-212">This setting indicates that an endpoint using this binding does not require a client credential.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="d0d8d-213">After the `<bindings>` element, add a `<services>` element.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="d0d8d-214">Similar to the bindings, you can define multiple services in a single configuration file.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="d0d8d-215">However, for this tutorial, you define only one.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-215">However, for this tutorial, you define only one.</span></span>
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    <span data-ttu-id="d0d8d-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="d0d8d-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="d0d8d-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d0d8d-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. <span data-ttu-id="d0d8d-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="d0d8d-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="d0d8d-221">Example</span><span class="sxs-lookup"><span data-stu-id="d0d8d-221">Example</span></span>
<span data-ttu-id="d0d8d-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="d0d8d-223">The following example shows the App.config file associated with the service.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-223">The following example shows the App.config file associated with the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove the ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="d0d8d-224">Step 4: Host the REST-based WCF service to use Azure Relay</span><span class="sxs-lookup"><span data-stu-id="d0d8d-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="d0d8d-225">This step describes how to run a web service using a console application with WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="d0d8d-226">A complete listing of the code written in this step is provided in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="d0d8d-227">To create a base address for the service</span><span class="sxs-lookup"><span data-stu-id="d0d8d-227">To create a base address for the service</span></span>
1. <span data-ttu-id="d0d8d-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="d0d8d-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="d0d8d-230">Service Bus uses the name of your namespace to create a unique URI.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="d0d8d-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="d0d8d-232">To create and configure the web service host</span><span class="sxs-lookup"><span data-stu-id="d0d8d-232">To create and configure the web service host</span></span>
* <span data-ttu-id="d0d8d-233">Create the web service host, using the URI address created earlier in this section.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="d0d8d-234">The service host is the WCF object that instantiates the host application.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="d0d8d-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="d0d8d-236">To run the web service host</span><span class="sxs-lookup"><span data-stu-id="d0d8d-236">To run the web service host</span></span>
1. <span data-ttu-id="d0d8d-237">Open the service.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="d0d8d-238">The service is now running.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-238">The service is now running.</span></span>
2. <span data-ttu-id="d0d8d-239">Display a message indicating that the service is running, and how to stop the service.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="d0d8d-240">When finished, close the service host.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="d0d8d-241">Example</span><span class="sxs-lookup"><span data-stu-id="d0d8d-241">Example</span></span>
<span data-ttu-id="d0d8d-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="d0d8d-243">Compile the following code into an executable named ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-243">Compile the following code into an executable named ImageListener.exe.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy the following address into a browser to see the image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-the-code"></a><span data-ttu-id="d0d8d-244">Compiling the code</span><span class="sxs-lookup"><span data-stu-id="d0d8d-244">Compiling the code</span></span>
<span data-ttu-id="d0d8d-245">After building the solution, do the following to run the application:</span><span class="sxs-lookup"><span data-stu-id="d0d8d-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="d0d8d-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="d0d8d-247">Keep the app running, as it's required to perform the next step.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="d0d8d-248">Copy and paste the address from the command prompt into a browser to see the image.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="d0d8d-249">When you are finished, press **Enter** in the command prompt window to close the app.</span><span class="sxs-lookup"><span data-stu-id="d0d8d-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0d8d-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="d0d8d-250">Next steps</span></span>
<span data-ttu-id="d0d8d-251">Now that you've built an application that uses the Azure Relay service, see the following articles to learn more:</span><span class="sxs-lookup"><span data-stu-id="d0d8d-251">Now that you've built an application that uses the Azure Relay service, see the following articles to learn more:</span></span>

* [<span data-ttu-id="d0d8d-252">Azure Service Bus architectural overview</span><span class="sxs-lookup"><span data-stu-id="d0d8d-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="d0d8d-253">Azure Relay overview</span><span class="sxs-lookup"><span data-stu-id="d0d8d-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="d0d8d-254">How to use the WCF relay service with .NET</span><span class="sxs-lookup"><span data-stu-id="d0d8d-254">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
