---
title: .NET multi-tier application using Azure Service Bus | Microsoft Docs
description: A .NET tutorial that helps you develop a multi-tier app in Azure that uses Service Bus queues to communicate between tiers.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 835741ba84bc989bb9e1dc3b9d009c158a6aa276
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553311"
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="c866f-103">.NET multi-tier application using Azure Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="c866f-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="c866f-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="c866f-104">Introduction</span></span>
<span data-ttu-id="c866f-105">Developing for Microsoft Azure is easy using Visual Studio and the free Azure SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="c866f-105">Developing for Microsoft Azure is easy using Visual Studio and the free Azure SDK for .NET.</span></span> <span data-ttu-id="c866f-106">This tutorial walks you through the steps to create an application that uses multiple Azure resources running in your local environment.</span><span class="sxs-lookup"><span data-stu-id="c866f-106">This tutorial walks you through the steps to create an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="c866f-107">You will learn the following:</span><span class="sxs-lookup"><span data-stu-id="c866f-107">You will learn the following:</span></span>

* <span data-ttu-id="c866f-108">How to enable your computer for Azure development with a single download and install.</span><span class="sxs-lookup"><span data-stu-id="c866f-108">How to enable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="c866f-109">How to use Visual Studio to develop for Azure.</span><span class="sxs-lookup"><span data-stu-id="c866f-109">How to use Visual Studio to develop for Azure.</span></span>
* <span data-ttu-id="c866f-110">How to create a multi-tier application in Azure using web and worker roles.</span><span class="sxs-lookup"><span data-stu-id="c866f-110">How to create a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="c866f-111">How to communicate between tiers using Service Bus queues.</span><span class="sxs-lookup"><span data-stu-id="c866f-111">How to communicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="c866f-112">In this tutorial you'll build and run the multi-tier application in an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="c866f-112">In this tutorial you'll build and run the multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="c866f-113">The front end is an ASP.NET MVC web role and the back end is a worker-role that uses a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-113">The front end is an ASP.NET MVC web role and the back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="c866f-114">You can create the same multi-tier application with the front end as a web project, that is deployed to an Azure website instead of a cloud service.</span><span class="sxs-lookup"><span data-stu-id="c866f-114">You can create the same multi-tier application with the front end as a web project, that is deployed to an Azure website instead of a cloud service.</span></span> <span data-ttu-id="c866f-115">You can also try out the [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="c866f-115">You can also try out the [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="c866f-116">The following screen shot shows the completed application.</span><span class="sxs-lookup"><span data-stu-id="c866f-116">The following screen shot shows the completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="c866f-117">Scenario overview: inter-role communication</span><span class="sxs-lookup"><span data-stu-id="c866f-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="c866f-118">To submit an order for processing, the front-end UI component, running in the web role, must interact with the middle tier logic running in the worker role.</span><span class="sxs-lookup"><span data-stu-id="c866f-118">To submit an order for processing, the front-end UI component, running in the web role, must interact with the middle tier logic running in the worker role.</span></span> <span data-ttu-id="c866f-119">This example uses Service Bus messaging for the communication between the tiers.</span><span class="sxs-lookup"><span data-stu-id="c866f-119">This example uses Service Bus messaging for the communication between the tiers.</span></span>

<span data-ttu-id="c866f-120">Using Service Bus messaging between the web and middle tiers decouples the two components.</span><span class="sxs-lookup"><span data-stu-id="c866f-120">Using Service Bus messaging between the web and middle tiers decouples the two components.</span></span> <span data-ttu-id="c866f-121">In contrast to direct messaging (that is, TCP or HTTP), the web tier does not connect to the middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until the middle tier is ready to consume and process them.</span><span class="sxs-lookup"><span data-stu-id="c866f-121">In contrast to direct messaging (that is, TCP or HTTP), the web tier does not connect to the middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until the middle tier is ready to consume and process them.</span></span>

<span data-ttu-id="c866f-122">Service Bus provides two entities to support brokered messaging: queues and topics.</span><span class="sxs-lookup"><span data-stu-id="c866f-122">Service Bus provides two entities to support brokered messaging: queues and topics.</span></span> <span data-ttu-id="c866f-123">With queues, each message sent to the queue is consumed by a single receiver.</span><span class="sxs-lookup"><span data-stu-id="c866f-123">With queues, each message sent to the queue is consumed by a single receiver.</span></span> <span data-ttu-id="c866f-124">Topics support the publish/subscribe pattern in which each published message is made available to a subscription registered with the topic.</span><span class="sxs-lookup"><span data-stu-id="c866f-124">Topics support the publish/subscribe pattern in which each published message is made available to a subscription registered with the topic.</span></span> <span data-ttu-id="c866f-125">Each subscription logically maintains its own queue of messages.</span><span class="sxs-lookup"><span data-stu-id="c866f-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="c866f-126">Subscriptions can also be configured with filter rules that restrict the set of messages passed to the subscription queue to those that match the filter.</span><span class="sxs-lookup"><span data-stu-id="c866f-126">Subscriptions can also be configured with filter rules that restrict the set of messages passed to the subscription queue to those that match the filter.</span></span> <span data-ttu-id="c866f-127">The following example uses Service Bus queues.</span><span class="sxs-lookup"><span data-stu-id="c866f-127">The following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="c866f-128">This communication mechanism has several advantages over direct messaging:</span><span class="sxs-lookup"><span data-stu-id="c866f-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="c866f-129">**Temporal decoupling.**</span><span class="sxs-lookup"><span data-stu-id="c866f-129">**Temporal decoupling.**</span></span> <span data-ttu-id="c866f-130">With the asynchronous messaging pattern, producers and consumers need not be online at the same time.</span><span class="sxs-lookup"><span data-stu-id="c866f-130">With the asynchronous messaging pattern, producers and consumers need not be online at the same time.</span></span> <span data-ttu-id="c866f-131">Service Bus reliably stores messages until the consuming party is ready to receive them.</span><span class="sxs-lookup"><span data-stu-id="c866f-131">Service Bus reliably stores messages until the consuming party is ready to receive them.</span></span> <span data-ttu-id="c866f-132">This enables the components of the distributed application to be disconnected, either voluntarily, for example, for maintenance, or due to a component crash, without impacting the system as a whole.</span><span class="sxs-lookup"><span data-stu-id="c866f-132">This enables the components of the distributed application to be disconnected, either voluntarily, for example, for maintenance, or due to a component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="c866f-133">Furthermore, the consuming application might only need to come online during certain times of the day.</span><span class="sxs-lookup"><span data-stu-id="c866f-133">Furthermore, the consuming application might only need to come online during certain times of the day.</span></span>
* <span data-ttu-id="c866f-134">**Load leveling.**</span><span class="sxs-lookup"><span data-stu-id="c866f-134">**Load leveling.**</span></span> <span data-ttu-id="c866f-135">In many applications, system load varies over time, while the processing time required for each unit of work is typically constant.</span><span class="sxs-lookup"><span data-stu-id="c866f-135">In many applications, system load varies over time, while the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="c866f-136">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only needs to be provisioned to accommodate average load rather than peak load.</span><span class="sxs-lookup"><span data-stu-id="c866f-136">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only needs to be provisioned to accommodate average load rather than peak load.</span></span> <span data-ttu-id="c866f-137">The depth of the queue grows and contracts as the incoming load varies.</span><span class="sxs-lookup"><span data-stu-id="c866f-137">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="c866f-138">This directly saves money in terms of the amount of infrastructure required to service the application load.</span><span class="sxs-lookup"><span data-stu-id="c866f-138">This directly saves money in terms of the amount of infrastructure required to service the application load.</span></span>
* <span data-ttu-id="c866f-139">**Load balancing.**</span><span class="sxs-lookup"><span data-stu-id="c866f-139">**Load balancing.**</span></span> <span data-ttu-id="c866f-140">As load increases, more worker processes can be added to read from the queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-140">As load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="c866f-141">Each message is processed by only one of the worker processes.</span><span class="sxs-lookup"><span data-stu-id="c866f-141">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="c866f-142">Furthermore, this pull-based load balancing enables optimal use of the worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span><span class="sxs-lookup"><span data-stu-id="c866f-142">Furthermore, this pull-based load balancing enables optimal use of the worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="c866f-143">This pattern is often termed the *competing consumer* pattern.</span><span class="sxs-lookup"><span data-stu-id="c866f-143">This pattern is often termed the *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="c866f-144">The following sections discuss the code that implements this architecture.</span><span class="sxs-lookup"><span data-stu-id="c866f-144">The following sections discuss the code that implements this architecture.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="c866f-145">Set up the development environment</span><span class="sxs-lookup"><span data-stu-id="c866f-145">Set up the development environment</span></span>
<span data-ttu-id="c866f-146">Before you can begin developing Azure applications, get the tools and set up your development environment.</span><span class="sxs-lookup"><span data-stu-id="c866f-146">Before you can begin developing Azure applications, get the tools and set up your development environment.</span></span>

1. <span data-ttu-id="c866f-147">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c866f-147">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="c866f-148">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span><span class="sxs-lookup"><span data-stu-id="c866f-148">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="c866f-149">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c866f-149">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="c866f-150">When prompted to run or save the installer, click **Run**.</span><span class="sxs-lookup"><span data-stu-id="c866f-150">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="c866f-151">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span><span class="sxs-lookup"><span data-stu-id="c866f-151">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="c866f-152">Once the installation is complete, you will have everything necessary to start to develop the app.</span><span class="sxs-lookup"><span data-stu-id="c866f-152">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="c866f-153">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c866f-153">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="c866f-154">Create a namespace</span><span class="sxs-lookup"><span data-stu-id="c866f-154">Create a namespace</span></span>
<span data-ttu-id="c866f-155">The next step is to create a service namespace, and obtain a Shared Access Signature (SAS) key.</span><span class="sxs-lookup"><span data-stu-id="c866f-155">The next step is to create a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="c866f-156">A namespace provides an application boundary for each application exposed through Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c866f-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="c866f-157">A SAS key is generated by the system when a namespace is created.</span><span class="sxs-lookup"><span data-stu-id="c866f-157">A SAS key is generated by the system when a namespace is created.</span></span> <span data-ttu-id="c866f-158">The combination of namespace and SAS key provides the credentials for Service Bus to authenticate access to an application.</span><span class="sxs-lookup"><span data-stu-id="c866f-158">The combination of namespace and SAS key provides the credentials for Service Bus to authenticate access to an application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="c866f-159">Create a web role</span><span class="sxs-lookup"><span data-stu-id="c866f-159">Create a web role</span></span>
<span data-ttu-id="c866f-160">In this section, you build the front end of your application.</span><span class="sxs-lookup"><span data-stu-id="c866f-160">In this section, you build the front end of your application.</span></span> <span data-ttu-id="c866f-161">First, you create the pages that your application displays.</span><span class="sxs-lookup"><span data-stu-id="c866f-161">First, you create the pages that your application displays.</span></span>
<span data-ttu-id="c866f-162">After that, add code that submits items to a Service Bus queue and displays status information about the queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-162">After that, add code that submits items to a Service Bus queue and displays status information about the queue.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="c866f-163">Create the project</span><span class="sxs-lookup"><span data-stu-id="c866f-163">Create the project</span></span>
1. <span data-ttu-id="c866f-164">Using administrator privileges, start Visual Studio: right-click the **Visual Studio** program icon, and then click **Run as administrator**.</span><span class="sxs-lookup"><span data-stu-id="c866f-164">Using administrator privileges, start Visual Studio: right-click the **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="c866f-165">The Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="c866f-165">The Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="c866f-166">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="c866f-166">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="c866f-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="c866f-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="c866f-168">Name the project **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="c866f-168">Name the project **MultiTierApp**.</span></span> <span data-ttu-id="c866f-169">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c866f-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="c866f-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span><span class="sxs-lookup"><span data-stu-id="c866f-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="c866f-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click the pencil icon, and rename the web role to **FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="c866f-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click the pencil icon, and rename the web role to **FrontendWebRole**.</span></span> <span data-ttu-id="c866f-172">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c866f-172">Then click **OK**.</span></span> <span data-ttu-id="c866f-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span><span class="sxs-lookup"><span data-stu-id="c866f-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="c866f-174">From the **New ASP.NET Project** dialog box, in the **Select a template** list, click **MVC**.</span><span class="sxs-lookup"><span data-stu-id="c866f-174">From the **New ASP.NET Project** dialog box, in the **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="c866f-175">Still in the **New ASP.NET Project** dialog box, click the **Change Authentication** button.</span><span class="sxs-lookup"><span data-stu-id="c866f-175">Still in the **New ASP.NET Project** dialog box, click the **Change Authentication** button.</span></span> <span data-ttu-id="c866f-176">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c866f-176">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="c866f-177">For this tutorial, you're deploying an app that doesn't need a user login.</span><span class="sxs-lookup"><span data-stu-id="c866f-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="c866f-178">Back in the **New ASP.NET Project** dialog box, click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="c866f-178">Back in the **New ASP.NET Project** dialog box, click **OK** to create the project.</span></span>
8. <span data-ttu-id="c866f-179">In **Solution Explorer**, in the **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="c866f-179">In **Solution Explorer**, in the **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="c866f-180">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="c866f-180">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="c866f-181">Select the **WindowsAzure.ServiceBus** package, click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="c866f-181">Select the **WindowsAzure.ServiceBus** package, click **Install**, and accept the terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="c866f-182">Note that the required client assemblies are now referenced and some new code files have been added.</span><span class="sxs-lookup"><span data-stu-id="c866f-182">Note that the required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="c866f-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="c866f-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="c866f-184">In the **Name** box, type the name **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="c866f-184">In the **Name** box, type the name **OnlineOrder.cs**.</span></span> <span data-ttu-id="c866f-185">Then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c866f-185">Then click **Add**.</span></span>

### <a name="write-the-code-for-your-web-role"></a><span data-ttu-id="c866f-186">Write the code for your web role</span><span class="sxs-lookup"><span data-stu-id="c866f-186">Write the code for your web role</span></span>
<span data-ttu-id="c866f-187">In this section, you create the various pages that your application displays.</span><span class="sxs-lookup"><span data-stu-id="c866f-187">In this section, you create the various pages that your application displays.</span></span>

1. <span data-ttu-id="c866f-188">In the OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with the following code:</span><span class="sxs-lookup"><span data-stu-id="c866f-188">In the OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with the following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="c866f-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c866f-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="c866f-190">Add the following **using** statements at the top of the file to include the namespaces for the model you just created, as well as Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c866f-190">Add the following **using** statements at the top of the file to include the namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="c866f-191">Also in the HomeController.cs file in Visual Studio, replace the existing namespace definition with the following code.</span><span class="sxs-lookup"><span data-stu-id="c866f-191">Also in the HomeController.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span> <span data-ttu-id="c866f-192">This code contains methods for handling the submission of items to the queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-192">This code contains methods for handling the submission of items to the queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect to Submit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for the submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from the submission
           // form.
           [HttpPost]
           // Attribute to help prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting to queue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="c866f-193">From the **Build** menu, click **Build Solution** to test the accuracy of your work so far.</span><span class="sxs-lookup"><span data-stu-id="c866f-193">From the **Build** menu, click **Build Solution** to test the accuracy of your work so far.</span></span>
5. <span data-ttu-id="c866f-194">Now, create the view for the `Submit()` method you created earlier.</span><span class="sxs-lookup"><span data-stu-id="c866f-194">Now, create the view for the `Submit()` method you created earlier.</span></span> <span data-ttu-id="c866f-195">Right-click within the `Submit()` method (the overload of `Submit()` that takes no parameters), and then choose **Add View**.</span><span class="sxs-lookup"><span data-stu-id="c866f-195">Right-click within the `Submit()` method (the overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="c866f-196">A dialog box appears for creating the view.</span><span class="sxs-lookup"><span data-stu-id="c866f-196">A dialog box appears for creating the view.</span></span> <span data-ttu-id="c866f-197">In the **Template** list, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="c866f-197">In the **Template** list, choose **Create**.</span></span> <span data-ttu-id="c866f-198">In the **Model class** list, click the **OnlineOrder** class.</span><span class="sxs-lookup"><span data-stu-id="c866f-198">In the **Model class** list, click the **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="c866f-199">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c866f-199">Click **Add**.</span></span>
8. <span data-ttu-id="c866f-200">Now, change the displayed name of your application.</span><span class="sxs-lookup"><span data-stu-id="c866f-200">Now, change the displayed name of your application.</span></span> <span data-ttu-id="c866f-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file to open it in the Visual Studio editor.</span><span class="sxs-lookup"><span data-stu-id="c866f-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="c866f-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span><span class="sxs-lookup"><span data-stu-id="c866f-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="c866f-203">Remove the **Home**, **About**, and **Contact** links.</span><span class="sxs-lookup"><span data-stu-id="c866f-203">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="c866f-204">Delete the highlighted code:</span><span class="sxs-lookup"><span data-stu-id="c866f-204">Delete the highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="c866f-205">Finally, modify the submission page to include some information about the queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-205">Finally, modify the submission page to include some information about the queue.</span></span> <span data-ttu-id="c866f-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file to open it in the Visual Studio editor.</span><span class="sxs-lookup"><span data-stu-id="c866f-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="c866f-207">Add the following line after `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="c866f-207">Add the following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="c866f-208">For now, the `ViewBag.MessageCount` is empty.</span><span class="sxs-lookup"><span data-stu-id="c866f-208">For now, the `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="c866f-209">You will populate it later.</span><span class="sxs-lookup"><span data-stu-id="c866f-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting to be processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="c866f-210">You now have implemented your UI.</span><span class="sxs-lookup"><span data-stu-id="c866f-210">You now have implemented your UI.</span></span> <span data-ttu-id="c866f-211">You can press **F5** to run your application and confirm that it looks as expected.</span><span class="sxs-lookup"><span data-stu-id="c866f-211">You can press **F5** to run your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-the-code-for-submitting-items-to-a-service-bus-queue"></a><span data-ttu-id="c866f-212">Write the code for submitting items to a Service Bus queue</span><span class="sxs-lookup"><span data-stu-id="c866f-212">Write the code for submitting items to a Service Bus queue</span></span>
<span data-ttu-id="c866f-213">Now, add code for submitting items to a queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-213">Now, add code for submitting items to a queue.</span></span> <span data-ttu-id="c866f-214">First, you create a class that contains your Service Bus queue connection information.</span><span class="sxs-lookup"><span data-stu-id="c866f-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="c866f-215">Then, initialize your connection from Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="c866f-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="c866f-216">Finally, update the submission code you created earlier in HomeController.cs to actually submit items to a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-216">Finally, update the submission code you created earlier in HomeController.cs to actually submit items to a Service Bus queue.</span></span>

1. <span data-ttu-id="c866f-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click the project, not the role).</span><span class="sxs-lookup"><span data-stu-id="c866f-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click the project, not the role).</span></span> <span data-ttu-id="c866f-218">Click **Add**, and then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="c866f-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="c866f-219">Name the class **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="c866f-219">Name the class **QueueConnector.cs**.</span></span> <span data-ttu-id="c866f-220">Click **Add** to create the class.</span><span class="sxs-lookup"><span data-stu-id="c866f-220">Click **Add** to create the class.</span></span>
3. <span data-ttu-id="c866f-221">Now, add code that encapsulates the connection information and initializes the connection to a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-221">Now, add code that encapsulates the connection information and initializes the connection to a Service Bus queue.</span></span> <span data-ttu-id="c866f-222">Replace the entire contents of QueueConnector.cs with the following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is the **primary key** you previously obtained from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c866f-222">Replace the entire contents of QueueConnector.cs with the following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is the **primary key** you previously obtained from the Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from the portal.
           public const string Namespace = "your Service Bus namespace";
   
           // The name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create the namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http to be friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create the namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create the queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client to the queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="c866f-223">Now, ensure that your **Initialize** method gets called.</span><span class="sxs-lookup"><span data-stu-id="c866f-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="c866f-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="c866f-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="c866f-225">Add the following line of code at the end of the **Application_Start** method.</span><span class="sxs-lookup"><span data-stu-id="c866f-225">Add the following line of code at the end of the **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="c866f-226">Finally, update the web code you created earlier, to submit items to the queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-226">Finally, update the web code you created earlier, to submit items to the queue.</span></span> <span data-ttu-id="c866f-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c866f-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="c866f-228">Update the `Submit()` method (the overload that takes no parameters) as follows to get the message count for the queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-228">Update the `Submit()` method (the overload that takes no parameters) as follows to get the message count for the queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you to perform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get the queue, and obtain the message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="c866f-229">Update the `Submit(OnlineOrder order)` method (the overload that takes one parameter) as follows to submit order information to the queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-229">Update the `Submit(OnlineOrder order)` method (the overload that takes one parameter) as follows to submit order information to the queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from the order.
           var message = new BrokeredMessage(order);
   
           // Submit the order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="c866f-230">You can now run the application again.</span><span class="sxs-lookup"><span data-stu-id="c866f-230">You can now run the application again.</span></span> <span data-ttu-id="c866f-231">Each time you submit an order, the message count increases.</span><span class="sxs-lookup"><span data-stu-id="c866f-231">Each time you submit an order, the message count increases.</span></span>
   
   ![][18]

## <a name="create-the-worker-role"></a><span data-ttu-id="c866f-232">Create the worker role</span><span class="sxs-lookup"><span data-stu-id="c866f-232">Create the worker role</span></span>
<span data-ttu-id="c866f-233">You will now create the worker role that processes the order submissions.</span><span class="sxs-lookup"><span data-stu-id="c866f-233">You will now create the worker role that processes the order submissions.</span></span> <span data-ttu-id="c866f-234">This example uses the **Worker Role with Service Bus Queue** Visual Studio project template.</span><span class="sxs-lookup"><span data-stu-id="c866f-234">This example uses the **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="c866f-235">You already obtained the required credentials from the portal.</span><span class="sxs-lookup"><span data-stu-id="c866f-235">You already obtained the required credentials from the portal.</span></span>

1. <span data-ttu-id="c866f-236">Make sure you have connected Visual Studio to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="c866f-236">Make sure you have connected Visual Studio to your Azure account.</span></span>
2. <span data-ttu-id="c866f-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under the **MultiTierApp** project.</span><span class="sxs-lookup"><span data-stu-id="c866f-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under the **MultiTierApp** project.</span></span>
3. <span data-ttu-id="c866f-238">Click **Add**, and then click **New Worker Role Project**.</span><span class="sxs-lookup"><span data-stu-id="c866f-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="c866f-239">The **Add New Role Project** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="c866f-239">The **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="c866f-240">In the **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span><span class="sxs-lookup"><span data-stu-id="c866f-240">In the **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="c866f-241">In the **Name** box, name the project **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="c866f-241">In the **Name** box, name the project **OrderProcessingRole**.</span></span> <span data-ttu-id="c866f-242">Then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c866f-242">Then click **Add**.</span></span>
6. <span data-ttu-id="c866f-243">Copy the connection string that you obtained in step 9 of the "Create a Service Bus namespace" section to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="c866f-243">Copy the connection string that you obtained in step 9 of the "Create a Service Bus namespace" section to the clipboard.</span></span>
7. <span data-ttu-id="c866f-244">In **Solution Explorer**, right-click the **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not the class).</span><span class="sxs-lookup"><span data-stu-id="c866f-244">In **Solution Explorer**, right-click the **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not the class).</span></span> <span data-ttu-id="c866f-245">Then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="c866f-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="c866f-246">On the **Settings** tab of the **Properties** dialog box, click inside the **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste the endpoint value you copied in step 6.</span><span class="sxs-lookup"><span data-stu-id="c866f-246">On the **Settings** tab of the **Properties** dialog box, click inside the **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste the endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="c866f-247">Create an **OnlineOrder** class to represent the orders as you process them from the queue.</span><span class="sxs-lookup"><span data-stu-id="c866f-247">Create an **OnlineOrder** class to represent the orders as you process them from the queue.</span></span> <span data-ttu-id="c866f-248">You can reuse a class you have already created.</span><span class="sxs-lookup"><span data-stu-id="c866f-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="c866f-249">In **Solution Explorer**, right-click the **OrderProcessingRole** class (right-click the class icon, not the role).</span><span class="sxs-lookup"><span data-stu-id="c866f-249">In **Solution Explorer**, right-click the **OrderProcessingRole** class (right-click the class icon, not the role).</span></span> <span data-ttu-id="c866f-250">Click **Add**, then click **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="c866f-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="c866f-251">Browse to the subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** to add it to this project.</span><span class="sxs-lookup"><span data-stu-id="c866f-251">Browse to the subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** to add it to this project.</span></span>
11. <span data-ttu-id="c866f-252">In **WorkerRole.cs**, change the value of the **QueueName** variable from `"ProcessingQueue"` to `"OrdersQueue"` as shown in the following code.</span><span class="sxs-lookup"><span data-stu-id="c866f-252">In **WorkerRole.cs**, change the value of the **QueueName** variable from `"ProcessingQueue"` to `"OrdersQueue"` as shown in the following code.</span></span>
    
    ```csharp
    // The name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="c866f-253">Add the following using statement at the top of the WorkerRole.cs file.</span><span class="sxs-lookup"><span data-stu-id="c866f-253">Add the following using statement at the top of the WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="c866f-254">In the `Run()` function, inside the `OnMessage()` call, replace the contents of the `try` clause with the following code.</span><span class="sxs-lookup"><span data-stu-id="c866f-254">In the `Run()` function, inside the `OnMessage()` call, replace the contents of the `try` clause with the following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View the message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="c866f-255">You have completed the application.</span><span class="sxs-lookup"><span data-stu-id="c866f-255">You have completed the application.</span></span> <span data-ttu-id="c866f-256">You can test the full application by right-clicking the MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span><span class="sxs-lookup"><span data-stu-id="c866f-256">You can test the full application by right-clicking the MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="c866f-257">Note that the message count does not increment, because the worker role processes items from the queue and marks them as complete.</span><span class="sxs-lookup"><span data-stu-id="c866f-257">Note that the message count does not increment, because the worker role processes items from the queue and marks them as complete.</span></span> <span data-ttu-id="c866f-258">You can see the trace output of your worker role by viewing the Azure Compute Emulator UI.</span><span class="sxs-lookup"><span data-stu-id="c866f-258">You can see the trace output of your worker role by viewing the Azure Compute Emulator UI.</span></span> <span data-ttu-id="c866f-259">You can do this by right-clicking the emulator icon in the notification area of your taskbar and selecting **Show Compute Emulator UI**.</span><span class="sxs-lookup"><span data-stu-id="c866f-259">You can do this by right-clicking the emulator icon in the notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="c866f-260">Next steps</span><span class="sxs-lookup"><span data-stu-id="c866f-260">Next steps</span></span>
<span data-ttu-id="c866f-261">To learn more about Service Bus, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="c866f-261">To learn more about Service Bus, see the following resources:</span></span>  

* <span data-ttu-id="c866f-262">[Azure Service Bus documentation][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="c866f-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="c866f-263">[Service Bus service page][sbacom]</span><span class="sxs-lookup"><span data-stu-id="c866f-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="c866f-264">[How to Use Service Bus Queues][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="c866f-264">[How to Use Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="c866f-265">To learn more about multi-tier scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="c866f-265">To learn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="c866f-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="c866f-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36



















