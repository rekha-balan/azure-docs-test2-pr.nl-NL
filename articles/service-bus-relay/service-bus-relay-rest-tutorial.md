---
title: Service Bus REST tutorial using Azure Relay | Microsoft Docs
description: Build a simple Azure Service Bus relay host application that exposes a REST-based interface.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/17/2017
ms.author: sethm
ms.openlocfilehash: 41bba4608fd7e3d0b16cbf0d846f5f65a071ad20
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551847"
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="666f2-103">Azure WCF Relay REST tutorial</span><span class="sxs-lookup"><span data-stu-id="666f2-103">Azure WCF Relay REST tutorial</span></span>
<span data-ttu-id="666f2-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span><span class="sxs-lookup"><span data-stu-id="666f2-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="666f2-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="666f2-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="666f2-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span><span class="sxs-lookup"><span data-stu-id="666f2-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span></span> <span data-ttu-id="666f2-107">For more information, see [WCF REST Programming Model](https://msdn.microsoft.com/library/bb412169.aspx) and [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span><span class="sxs-lookup"><span data-stu-id="666f2-107">For more information, see [WCF REST Programming Model](https://msdn.microsoft.com/library/bb412169.aspx) and [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span></span>

## <a name="step-1-create-a-service-namespace"></a><span data-ttu-id="666f2-108">Step 1: Create a service namespace</span><span class="sxs-lookup"><span data-stu-id="666f2-108">Step 1: Create a service namespace</span></span>

<span data-ttu-id="666f2-109">To begin using the relay features in Azure, you must first create a service namespace.</span><span class="sxs-lookup"><span data-stu-id="666f2-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="666f2-110">A namespace provides a scoping container for addressing Azure resources within your application.</span><span class="sxs-lookup"><span data-stu-id="666f2-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="666f2-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span><span class="sxs-lookup"><span data-stu-id="666f2-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="666f2-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span><span class="sxs-lookup"><span data-stu-id="666f2-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>
<span data-ttu-id="666f2-113">When you create a WCF REST-style service, you must define the contract.</span><span class="sxs-lookup"><span data-stu-id="666f2-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="666f2-114">The contract specifies what operations the host supports.</span><span class="sxs-lookup"><span data-stu-id="666f2-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="666f2-115">A service operation can be thought of as a web service method.</span><span class="sxs-lookup"><span data-stu-id="666f2-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="666f2-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span><span class="sxs-lookup"><span data-stu-id="666f2-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="666f2-117">Each method in the interface corresponds to a specific service operation.</span><span class="sxs-lookup"><span data-stu-id="666f2-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="666f2-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span><span class="sxs-lookup"><span data-stu-id="666f2-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span></span> <span data-ttu-id="666f2-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span><span class="sxs-lookup"><span data-stu-id="666f2-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="666f2-120">The code used for these tasks is shown in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="666f2-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="666f2-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="666f2-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="666f2-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span><span class="sxs-lookup"><span data-stu-id="666f2-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="666f2-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="666f2-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span></span> <span data-ttu-id="666f2-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span><span class="sxs-lookup"><span data-stu-id="666f2-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="666f2-125">To create a contract with an interface</span><span class="sxs-lookup"><span data-stu-id="666f2-125">To create a contract with an interface</span></span>
1. <span data-ttu-id="666f2-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span><span class="sxs-lookup"><span data-stu-id="666f2-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="666f2-127">Create a new console application project.</span><span class="sxs-lookup"><span data-stu-id="666f2-127">Create a new console application project.</span></span> <span data-ttu-id="666f2-128">Click the **File** menu and select **New**, then select **Project**.</span><span class="sxs-lookup"><span data-stu-id="666f2-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="666f2-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="666f2-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="666f2-130">Use the default **Location**.</span><span class="sxs-lookup"><span data-stu-id="666f2-130">Use the default **Location**.</span></span> <span data-ttu-id="666f2-131">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="666f2-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="666f2-132">For a C# project, Visual Studio creates a `Program.cs` file.</span><span class="sxs-lookup"><span data-stu-id="666f2-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="666f2-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span><span class="sxs-lookup"><span data-stu-id="666f2-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="666f2-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span><span class="sxs-lookup"><span data-stu-id="666f2-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="666f2-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="666f2-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="666f2-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="666f2-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="666f2-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="666f2-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="666f2-138">Click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="666f2-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="666f2-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span><span class="sxs-lookup"><span data-stu-id="666f2-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="666f2-140">a.</span><span class="sxs-lookup"><span data-stu-id="666f2-140">a.</span></span> <span data-ttu-id="666f2-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="666f2-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="666f2-142">b.</span><span class="sxs-lookup"><span data-stu-id="666f2-142">b.</span></span> <span data-ttu-id="666f2-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span><span class="sxs-lookup"><span data-stu-id="666f2-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="666f2-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="666f2-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="666f2-145">Add the following `using` statements at the top of the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="666f2-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="666f2-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span><span class="sxs-lookup"><span data-stu-id="666f2-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="666f2-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span><span class="sxs-lookup"><span data-stu-id="666f2-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="666f2-148">You will use this namespace in most of your relay applications.</span><span class="sxs-lookup"><span data-stu-id="666f2-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="666f2-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span><span class="sxs-lookup"><span data-stu-id="666f2-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="666f2-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span><span class="sxs-lookup"><span data-stu-id="666f2-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="666f2-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="666f2-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="666f2-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="666f2-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="666f2-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span><span class="sxs-lookup"><span data-stu-id="666f2-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="666f2-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span><span class="sxs-lookup"><span data-stu-id="666f2-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="666f2-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="666f2-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="666f2-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span><span class="sxs-lookup"><span data-stu-id="666f2-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="666f2-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span><span class="sxs-lookup"><span data-stu-id="666f2-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="666f2-158">In the **OperationContract** attribute, add the **WebGet** value.</span><span class="sxs-lookup"><span data-stu-id="666f2-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="666f2-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span><span class="sxs-lookup"><span data-stu-id="666f2-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="666f2-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span><span class="sxs-lookup"><span data-stu-id="666f2-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="666f2-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span><span class="sxs-lookup"><span data-stu-id="666f2-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="666f2-162">A channel is the WCF object through which the service and client pass information to each other.</span><span class="sxs-lookup"><span data-stu-id="666f2-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="666f2-163">Later, you will create the channel in your host application.</span><span class="sxs-lookup"><span data-stu-id="666f2-163">Later, you will create the channel in your host application.</span></span> <span data-ttu-id="666f2-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span><span class="sxs-lookup"><span data-stu-id="666f2-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="666f2-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span><span class="sxs-lookup"><span data-stu-id="666f2-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="666f2-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span><span class="sxs-lookup"><span data-stu-id="666f2-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="666f2-167">Example</span><span class="sxs-lookup"><span data-stu-id="666f2-167">Example</span></span>
<span data-ttu-id="666f2-168">The following code shows a basic interface that defines a WCF Relay contract.</span><span class="sxs-lookup"><span data-stu-id="666f2-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="666f2-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span><span class="sxs-lookup"><span data-stu-id="666f2-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="666f2-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span><span class="sxs-lookup"><span data-stu-id="666f2-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="666f2-171">The next step is to implement the interface.</span><span class="sxs-lookup"><span data-stu-id="666f2-171">The next step is to implement the interface.</span></span> <span data-ttu-id="666f2-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="666f2-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="666f2-173">After you implement the contract, you then configure the interface using an App.config file.</span><span class="sxs-lookup"><span data-stu-id="666f2-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="666f2-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span><span class="sxs-lookup"><span data-stu-id="666f2-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="666f2-175">The code used for these tasks is provided in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="666f2-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="666f2-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span><span class="sxs-lookup"><span data-stu-id="666f2-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="666f2-177">To implement a REST-style Service Bus contract</span><span class="sxs-lookup"><span data-stu-id="666f2-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="666f2-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="666f2-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="666f2-179">The **ImageService** class implements the **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="666f2-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="666f2-180">Similar to other interface implementations, you can implement the definition in a different file.</span><span class="sxs-lookup"><span data-stu-id="666f2-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="666f2-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span><span class="sxs-lookup"><span data-stu-id="666f2-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="666f2-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span><span class="sxs-lookup"><span data-stu-id="666f2-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="666f2-183">As mentioned previously, this namespace is not a traditional namespace.</span><span class="sxs-lookup"><span data-stu-id="666f2-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="666f2-184">Instead, it is part of the WCF architecture that identifies the contract.</span><span class="sxs-lookup"><span data-stu-id="666f2-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="666f2-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span><span class="sxs-lookup"><span data-stu-id="666f2-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span></span>
3. <span data-ttu-id="666f2-186">Add a .jpg image to your project.</span><span class="sxs-lookup"><span data-stu-id="666f2-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="666f2-187">This is a picture that the service displays in the receiving browser.</span><span class="sxs-lookup"><span data-stu-id="666f2-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="666f2-188">Right-click your project, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="666f2-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="666f2-189">Then click **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="666f2-189">Then click **Existing Item**.</span></span> <span data-ttu-id="666f2-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="666f2-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="666f2-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span><span class="sxs-lookup"><span data-stu-id="666f2-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="666f2-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span><span class="sxs-lookup"><span data-stu-id="666f2-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="666f2-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span><span class="sxs-lookup"><span data-stu-id="666f2-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="666f2-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="666f2-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="666f2-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span><span class="sxs-lookup"><span data-stu-id="666f2-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="666f2-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span><span class="sxs-lookup"><span data-stu-id="666f2-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="666f2-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span><span class="sxs-lookup"><span data-stu-id="666f2-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
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
7. <span data-ttu-id="666f2-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span><span class="sxs-lookup"><span data-stu-id="666f2-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
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
   
    <span data-ttu-id="666f2-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span><span class="sxs-lookup"><span data-stu-id="666f2-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="666f2-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span><span class="sxs-lookup"><span data-stu-id="666f2-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="666f2-201">From the **Build** menu, click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="666f2-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="666f2-202">To define the configuration for running the web service on Service Bus</span><span class="sxs-lookup"><span data-stu-id="666f2-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="666f2-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span><span class="sxs-lookup"><span data-stu-id="666f2-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="666f2-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span><span class="sxs-lookup"><span data-stu-id="666f2-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="666f2-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span><span class="sxs-lookup"><span data-stu-id="666f2-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="666f2-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span><span class="sxs-lookup"><span data-stu-id="666f2-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="666f2-207">Here, it is used to define the service name and endpoint.</span><span class="sxs-lookup"><span data-stu-id="666f2-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="666f2-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span><span class="sxs-lookup"><span data-stu-id="666f2-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="666f2-209">This defines the bindings used in the application.</span><span class="sxs-lookup"><span data-stu-id="666f2-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="666f2-210">You can define multiple bindings, but for this tutorial you are defining only one.</span><span class="sxs-lookup"><span data-stu-id="666f2-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
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
   
    <span data-ttu-id="666f2-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span><span class="sxs-lookup"><span data-stu-id="666f2-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="666f2-212">This setting indicates that an endpoint using this binding does not require a client credential.</span><span class="sxs-lookup"><span data-stu-id="666f2-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="666f2-213">After the `<bindings>` element, add a `<services>` element.</span><span class="sxs-lookup"><span data-stu-id="666f2-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="666f2-214">Similar to the bindings, you can define multiple services in a single configuration file.</span><span class="sxs-lookup"><span data-stu-id="666f2-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="666f2-215">However, for this tutorial, you define only one.</span><span class="sxs-lookup"><span data-stu-id="666f2-215">However, for this tutorial, you define only one.</span></span>
   
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
   
    <span data-ttu-id="666f2-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="666f2-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="666f2-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span><span class="sxs-lookup"><span data-stu-id="666f2-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="666f2-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="666f2-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
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
5. <span data-ttu-id="666f2-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span><span class="sxs-lookup"><span data-stu-id="666f2-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="666f2-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span><span class="sxs-lookup"><span data-stu-id="666f2-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="666f2-221">Example</span><span class="sxs-lookup"><span data-stu-id="666f2-221">Example</span></span>
<span data-ttu-id="666f2-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span><span class="sxs-lookup"><span data-stu-id="666f2-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

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

<span data-ttu-id="666f2-223">The following example shows the App.config file associated with the service.</span><span class="sxs-lookup"><span data-stu-id="666f2-223">The following example shows the App.config file associated with the service.</span></span>

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

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="666f2-224">Step 4: Host the REST-based WCF service to use Azure Relay</span><span class="sxs-lookup"><span data-stu-id="666f2-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="666f2-225">This step describes how to run a web service using a console application with WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="666f2-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="666f2-226">A complete listing of the code written in this step is provided in the example following the procedure.</span><span class="sxs-lookup"><span data-stu-id="666f2-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="666f2-227">To create a base address for the service</span><span class="sxs-lookup"><span data-stu-id="666f2-227">To create a base address for the service</span></span>
1. <span data-ttu-id="666f2-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span><span class="sxs-lookup"><span data-stu-id="666f2-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="666f2-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span><span class="sxs-lookup"><span data-stu-id="666f2-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="666f2-230">Service Bus uses the name of your namespace to create a unique URI.</span><span class="sxs-lookup"><span data-stu-id="666f2-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="666f2-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span><span class="sxs-lookup"><span data-stu-id="666f2-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="666f2-232">To create and configure the web service host</span><span class="sxs-lookup"><span data-stu-id="666f2-232">To create and configure the web service host</span></span>
* <span data-ttu-id="666f2-233">Create the web service host, using the URI address created earlier in this section.</span><span class="sxs-lookup"><span data-stu-id="666f2-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="666f2-234">The service host is the WCF object that instantiates the host application.</span><span class="sxs-lookup"><span data-stu-id="666f2-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="666f2-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span><span class="sxs-lookup"><span data-stu-id="666f2-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="666f2-236">To run the web service host</span><span class="sxs-lookup"><span data-stu-id="666f2-236">To run the web service host</span></span>
1. <span data-ttu-id="666f2-237">Open the service.</span><span class="sxs-lookup"><span data-stu-id="666f2-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="666f2-238">The service is now running.</span><span class="sxs-lookup"><span data-stu-id="666f2-238">The service is now running.</span></span>
2. <span data-ttu-id="666f2-239">Display a message indicating that the service is running, and how to stop the service.</span><span class="sxs-lookup"><span data-stu-id="666f2-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="666f2-240">When finished, close the service host.</span><span class="sxs-lookup"><span data-stu-id="666f2-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="666f2-241">Example</span><span class="sxs-lookup"><span data-stu-id="666f2-241">Example</span></span>
<span data-ttu-id="666f2-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span><span class="sxs-lookup"><span data-stu-id="666f2-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="666f2-243">Compile the following code into an executable named ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="666f2-243">Compile the following code into an executable named ImageListener.exe.</span></span>

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

### <a name="compiling-the-code"></a><span data-ttu-id="666f2-244">Compiling the code</span><span class="sxs-lookup"><span data-stu-id="666f2-244">Compiling the code</span></span>
<span data-ttu-id="666f2-245">After building the solution, do the following to run the application:</span><span class="sxs-lookup"><span data-stu-id="666f2-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="666f2-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span><span class="sxs-lookup"><span data-stu-id="666f2-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="666f2-247">Keep the app running, as it's required to perform the next step.</span><span class="sxs-lookup"><span data-stu-id="666f2-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="666f2-248">Copy and paste the address from the command prompt into a browser to see the image.</span><span class="sxs-lookup"><span data-stu-id="666f2-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="666f2-249">When you are finished, press **Enter** in the command prompt window to close the app.</span><span class="sxs-lookup"><span data-stu-id="666f2-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="666f2-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="666f2-250">Next steps</span></span>
<span data-ttu-id="666f2-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span><span class="sxs-lookup"><span data-stu-id="666f2-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span></span>

* [<span data-ttu-id="666f2-252">Azure Service Bus architectural overview</span><span class="sxs-lookup"><span data-stu-id="666f2-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="666f2-253">Azure Relay overview</span><span class="sxs-lookup"><span data-stu-id="666f2-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="666f2-254">How to use the WCF relay service with .NET</span><span class="sxs-lookup"><span data-stu-id="666f2-254">How to use the WCF relay service with .NET</span></span>](service-bus-dotnet-how-to-use-relay.md)

[Azure portal]: https://portal.azure.com
