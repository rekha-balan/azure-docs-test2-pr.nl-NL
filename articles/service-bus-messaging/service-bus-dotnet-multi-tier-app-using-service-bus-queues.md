---
title: .NET multi-tier application using Azure Service Bus | Microsoft Docs
description: A .NET tutorial that helps you develop a multi-tier app in Azure that uses Service Bus queues to communicate between tiers.
services: service-bus-messaging
documentationcenter: .net
author: spelluru
manager: timlt
ms.service: service-bus-messaging
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2018
ms.author: spelluru
ms.openlocfilehash: cd451f50406c8ee9e20420b02988fd63366f9061
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776093"
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="d6bd2-103">.NET multi-tier application using Azure Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="d6bd2-103">.NET multi-tier application using Azure Service Bus queues</span></span>

<span data-ttu-id="d6bd2-104">Developing for Microsoft Azure is easy using Visual Studio and the free Azure SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-104">Developing for Microsoft Azure is easy using Visual Studio and the free Azure SDK for .NET.</span></span> <span data-ttu-id="d6bd2-105">This tutorial walks you through the steps to create an application that uses multiple Azure resources running in your local environment.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-105">This tutorial walks you through the steps to create an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="d6bd2-106">You will learn the following:</span><span class="sxs-lookup"><span data-stu-id="d6bd2-106">You will learn the following:</span></span>

* <span data-ttu-id="d6bd2-107">How to enable your computer for Azure development with a single download and install.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-107">How to enable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="d6bd2-108">How to use Visual Studio to develop for Azure.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-108">How to use Visual Studio to develop for Azure.</span></span>
* <span data-ttu-id="d6bd2-109">How to create a multi-tier application in Azure using web and worker roles.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-109">How to create a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="d6bd2-110">How to communicate between tiers using Service Bus queues.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-110">How to communicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="d6bd2-111">In this tutorial you'll build and run the multi-tier application in an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-111">In this tutorial you'll build and run the multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="d6bd2-112">The front end is an ASP.NET MVC web role and the back end is a worker-role that uses a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-112">The front end is an ASP.NET MVC web role and the back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="d6bd2-113">You can create the same multi-tier application with the front end as a web project, that is deployed to an Azure website instead of a cloud service.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-113">You can create the same multi-tier application with the front end as a web project, that is deployed to an Azure website instead of a cloud service.</span></span> <span data-ttu-id="d6bd2-114">You can also try out the [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-114">You can also try out the [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="d6bd2-115">The following screen shot shows the completed application.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-115">The following screen shot shows the completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="d6bd2-116">Scenario overview: inter-role communication</span><span class="sxs-lookup"><span data-stu-id="d6bd2-116">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="d6bd2-117">To submit an order for processing, the front-end UI component, running in the web role, must interact with the middle tier logic running in the worker role.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-117">To submit an order for processing, the front-end UI component, running in the web role, must interact with the middle tier logic running in the worker role.</span></span> <span data-ttu-id="d6bd2-118">This example uses Service Bus messaging for the communication between the tiers.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-118">This example uses Service Bus messaging for the communication between the tiers.</span></span>

<span data-ttu-id="d6bd2-119">Using Service Bus messaging between the web and middle tiers decouples the two components.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-119">Using Service Bus messaging between the web and middle tiers decouples the two components.</span></span> <span data-ttu-id="d6bd2-120">In contrast to direct messaging (that is, TCP or HTTP), the web tier does not connect to the middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until the middle tier is ready to consume and process them.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-120">In contrast to direct messaging (that is, TCP or HTTP), the web tier does not connect to the middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until the middle tier is ready to consume and process them.</span></span>

<span data-ttu-id="d6bd2-121">Service Bus provides two entities to support brokered messaging: queues and topics.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-121">Service Bus provides two entities to support brokered messaging: queues and topics.</span></span> <span data-ttu-id="d6bd2-122">With queues, each message sent to the queue is consumed by a single receiver.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-122">With queues, each message sent to the queue is consumed by a single receiver.</span></span> <span data-ttu-id="d6bd2-123">Topics support the publish/subscribe pattern in which each published message is made available to a subscription registered with the topic.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-123">Topics support the publish/subscribe pattern in which each published message is made available to a subscription registered with the topic.</span></span> <span data-ttu-id="d6bd2-124">Each subscription logically maintains its own queue of messages.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-124">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="d6bd2-125">Subscriptions can also be configured with filter rules that restrict the set of messages passed to the subscription queue to those that match the filter.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-125">Subscriptions can also be configured with filter rules that restrict the set of messages passed to the subscription queue to those that match the filter.</span></span> <span data-ttu-id="d6bd2-126">The following example uses Service Bus queues.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-126">The following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="d6bd2-127">This communication mechanism has several advantages over direct messaging:</span><span class="sxs-lookup"><span data-stu-id="d6bd2-127">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="d6bd2-128">**Temporal decoupling.**</span><span class="sxs-lookup"><span data-stu-id="d6bd2-128">**Temporal decoupling.**</span></span> <span data-ttu-id="d6bd2-129">With the asynchronous messaging pattern, producers and consumers need not be online at the same time.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-129">With the asynchronous messaging pattern, producers and consumers need not be online at the same time.</span></span> <span data-ttu-id="d6bd2-130">Service Bus reliably stores messages until the consuming party is ready to receive them.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-130">Service Bus reliably stores messages until the consuming party is ready to receive them.</span></span> <span data-ttu-id="d6bd2-131">This enables the components of the distributed application to be disconnected, either voluntarily, for example, for maintenance, or due to a component crash, without impacting the system as a whole.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-131">This enables the components of the distributed application to be disconnected, either voluntarily, for example, for maintenance, or due to a component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="d6bd2-132">Furthermore, the consuming application might only need to come online during certain times of the day.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-132">Furthermore, the consuming application might only need to come online during certain times of the day.</span></span>
* <span data-ttu-id="d6bd2-133">**Load leveling.**</span><span class="sxs-lookup"><span data-stu-id="d6bd2-133">**Load leveling.**</span></span> <span data-ttu-id="d6bd2-134">In many applications, system load varies over time, while the processing time required for each unit of work is typically constant.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-134">In many applications, system load varies over time, while the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="d6bd2-135">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only needs to be provisioned to accommodate average load rather than peak load.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-135">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only needs to be provisioned to accommodate average load rather than peak load.</span></span> <span data-ttu-id="d6bd2-136">The depth of the queue grows and contracts as the incoming load varies.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-136">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="d6bd2-137">This directly saves money in terms of the amount of infrastructure required to service the application load.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-137">This directly saves money in terms of the amount of infrastructure required to service the application load.</span></span>
* <span data-ttu-id="d6bd2-138">**Load balancing.**</span><span class="sxs-lookup"><span data-stu-id="d6bd2-138">**Load balancing.**</span></span> <span data-ttu-id="d6bd2-139">As load increases, more worker processes can be added to read from the queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-139">As load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="d6bd2-140">Each message is processed by only one of the worker processes.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-140">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="d6bd2-141">Furthermore, this pull-based load balancing enables optimal use of the worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-141">Furthermore, this pull-based load balancing enables optimal use of the worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="d6bd2-142">This pattern is often termed the *competing consumer* pattern.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-142">This pattern is often termed the *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="d6bd2-143">The following sections discuss the code that implements this architecture.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-143">The following sections discuss the code that implements this architecture.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="d6bd2-144">Create a namespace</span><span class="sxs-lookup"><span data-stu-id="d6bd2-144">Create a namespace</span></span>

<span data-ttu-id="d6bd2-145">The first step is to create a *namespace*, and obtain a [Shared Access Signature (SAS)](service-bus-sas.md) key for that namespace.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-145">The first step is to create a *namespace*, and obtain a [Shared Access Signature (SAS)](service-bus-sas.md) key for that namespace.</span></span> <span data-ttu-id="d6bd2-146">A namespace provides an application boundary for each application exposed through Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-146">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="d6bd2-147">A SAS key is generated by the system when a namespace is created.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-147">A SAS key is generated by the system when a namespace is created.</span></span> <span data-ttu-id="d6bd2-148">The combination of namespace name and SAS key provides the credentials for Service Bus to authenticate access to an application.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-148">The combination of namespace name and SAS key provides the credentials for Service Bus to authenticate access to an application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="d6bd2-149">Create a web role</span><span class="sxs-lookup"><span data-stu-id="d6bd2-149">Create a web role</span></span>

<span data-ttu-id="d6bd2-150">In this section, you build the front end of your application.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-150">In this section, you build the front end of your application.</span></span> <span data-ttu-id="d6bd2-151">First, you create the pages that your application displays.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-151">First, you create the pages that your application displays.</span></span>
<span data-ttu-id="d6bd2-152">After that, add code that submits items to a Service Bus queue and displays status information about the queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-152">After that, add code that submits items to a Service Bus queue and displays status information about the queue.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="d6bd2-153">Create the project</span><span class="sxs-lookup"><span data-stu-id="d6bd2-153">Create the project</span></span>

1. <span data-ttu-id="d6bd2-154">Using administrator privileges, start Visual Studio: right-click the **Visual Studio** program icon, and then click **Run as administrator**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-154">Using administrator privileges, start Visual Studio: right-click the **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="d6bd2-155">The Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-155">The Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="d6bd2-156">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-156">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="d6bd2-157">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-157">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="d6bd2-158">Name the project **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-158">Name the project **MultiTierApp**.</span></span> <span data-ttu-id="d6bd2-159">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-159">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="d6bd2-160">From the **Roles** pane, double-click **ASP.NET Web Role**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-160">From the **Roles** pane, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="d6bd2-161">Hover over **WebRole1** under **Azure Cloud Service solution**, click the pencil icon, and rename the web role to **FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-161">Hover over **WebRole1** under **Azure Cloud Service solution**, click the pencil icon, and rename the web role to **FrontendWebRole**.</span></span> <span data-ttu-id="d6bd2-162">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-162">Then click **OK**.</span></span> <span data-ttu-id="d6bd2-163">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span><span class="sxs-lookup"><span data-stu-id="d6bd2-163">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="d6bd2-164">From the **New ASP.NET Project** dialog box, in the **Select a template** list, click **MVC**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-164">From the **New ASP.NET Project** dialog box, in the **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="d6bd2-165">Still in the **New ASP.NET Project** dialog box, click the **Change Authentication** button.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-165">Still in the **New ASP.NET Project** dialog box, click the **Change Authentication** button.</span></span> <span data-ttu-id="d6bd2-166">In the **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-166">In the **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="d6bd2-167">For this tutorial, you're deploying an app that doesn't need a user login.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-167">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="d6bd2-168">Back in the **New ASP.NET Project** dialog box, click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-168">Back in the **New ASP.NET Project** dialog box, click **OK** to create the project.</span></span>
8. <span data-ttu-id="d6bd2-169">In **Solution Explorer**, in the **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-169">In **Solution Explorer**, in the **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="d6bd2-170">Click the **Browse** tab, then search for **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-170">Click the **Browse** tab, then search for **WindowsAzure.ServiceBus**.</span></span> <span data-ttu-id="d6bd2-171">Select the **WindowsAzure.ServiceBus** package, click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-171">Select the **WindowsAzure.ServiceBus** package, click **Install**, and accept the terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="d6bd2-172">Note that the required client assemblies are now referenced and some new code files have been added.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-172">Note that the required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="d6bd2-173">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-173">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="d6bd2-174">In the **Name** box, type the name **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-174">In the **Name** box, type the name **OnlineOrder.cs**.</span></span> <span data-ttu-id="d6bd2-175">Then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-175">Then click **Add**.</span></span>

### <a name="write-the-code-for-your-web-role"></a><span data-ttu-id="d6bd2-176">Write the code for your web role</span><span class="sxs-lookup"><span data-stu-id="d6bd2-176">Write the code for your web role</span></span>
<span data-ttu-id="d6bd2-177">In this section, you create the various pages that your application displays.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-177">In this section, you create the various pages that your application displays.</span></span>

1. <span data-ttu-id="d6bd2-178">In the OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with the following code:</span><span class="sxs-lookup"><span data-stu-id="d6bd2-178">In the OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with the following code:</span></span>
   
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
2. <span data-ttu-id="d6bd2-179">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-179">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="d6bd2-180">Add the following **using** statements at the top of the file to include the namespaces for the model you just created, as well as Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-180">Add the following **using** statements at the top of the file to include the namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="d6bd2-181">Also in the HomeController.cs file in Visual Studio, replace the existing namespace definition with the following code.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-181">Also in the HomeController.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span> <span data-ttu-id="d6bd2-182">This code contains methods for handling the submission of items to the queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-182">This code contains methods for handling the submission of items to the queue.</span></span>
   
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
4. <span data-ttu-id="d6bd2-183">From the **Build** menu, click **Build Solution** to test the accuracy of your work so far.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-183">From the **Build** menu, click **Build Solution** to test the accuracy of your work so far.</span></span>
5. <span data-ttu-id="d6bd2-184">Now, create the view for the `Submit()` method you created earlier.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-184">Now, create the view for the `Submit()` method you created earlier.</span></span> <span data-ttu-id="d6bd2-185">Right-click within the `Submit()` method (the overload of `Submit()` that takes no parameters), and then choose **Add View**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-185">Right-click within the `Submit()` method (the overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="d6bd2-186">A dialog box appears for creating the view.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-186">A dialog box appears for creating the view.</span></span> <span data-ttu-id="d6bd2-187">In the **Template** list, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-187">In the **Template** list, choose **Create**.</span></span> <span data-ttu-id="d6bd2-188">In the **Model class** list, select the **OnlineOrder** class.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-188">In the **Model class** list, select the **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="d6bd2-189">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-189">Click **Add**.</span></span>
8. <span data-ttu-id="d6bd2-190">Now, change the displayed name of your application.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-190">Now, change the displayed name of your application.</span></span> <span data-ttu-id="d6bd2-191">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file to open it in the Visual Studio editor.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-191">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="d6bd2-192">Replace all occurrences of **My ASP.NET Application** with **Northwind Traders Products**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-192">Replace all occurrences of **My ASP.NET Application** with **Northwind Traders Products**.</span></span>
10. <span data-ttu-id="d6bd2-193">Remove the **Home**, **About**, and **Contact** links.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-193">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="d6bd2-194">Delete the highlighted code:</span><span class="sxs-lookup"><span data-stu-id="d6bd2-194">Delete the highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="d6bd2-195">Finally, modify the submission page to include some information about the queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-195">Finally, modify the submission page to include some information about the queue.</span></span> <span data-ttu-id="d6bd2-196">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file to open it in the Visual Studio editor.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-196">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="d6bd2-197">Add the following line after `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-197">Add the following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="d6bd2-198">For now, the `ViewBag.MessageCount` is empty.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-198">For now, the `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="d6bd2-199">You will populate it later.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-199">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting to be processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="d6bd2-200">You now have implemented your UI.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-200">You now have implemented your UI.</span></span> <span data-ttu-id="d6bd2-201">You can press **F5** to run your application and confirm that it looks as expected.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-201">You can press **F5** to run your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-the-code-for-submitting-items-to-a-service-bus-queue"></a><span data-ttu-id="d6bd2-202">Write the code for submitting items to a Service Bus queue</span><span class="sxs-lookup"><span data-stu-id="d6bd2-202">Write the code for submitting items to a Service Bus queue</span></span>
<span data-ttu-id="d6bd2-203">Now, add code for submitting items to a queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-203">Now, add code for submitting items to a queue.</span></span> <span data-ttu-id="d6bd2-204">First, you create a class that contains your Service Bus queue connection information.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-204">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="d6bd2-205">Then, initialize your connection from Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-205">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="d6bd2-206">Finally, update the submission code you created earlier in HomeController.cs to actually submit items to a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-206">Finally, update the submission code you created earlier in HomeController.cs to actually submit items to a Service Bus queue.</span></span>

1. <span data-ttu-id="d6bd2-207">In **Solution Explorer**, right-click **FrontendWebRole** (right-click the project, not the role).</span><span class="sxs-lookup"><span data-stu-id="d6bd2-207">In **Solution Explorer**, right-click **FrontendWebRole** (right-click the project, not the role).</span></span> <span data-ttu-id="d6bd2-208">Click **Add**, and then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-208">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="d6bd2-209">Name the class **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-209">Name the class **QueueConnector.cs**.</span></span> <span data-ttu-id="d6bd2-210">Click **Add** to create the class.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-210">Click **Add** to create the class.</span></span>
3. <span data-ttu-id="d6bd2-211">Now, add code that encapsulates the connection information and initializes the connection to a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-211">Now, add code that encapsulates the connection information and initializes the connection to a Service Bus queue.</span></span> <span data-ttu-id="d6bd2-212">Replace the entire contents of QueueConnector.cs with the following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is the **primary key** you previously obtained from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-212">Replace the entire contents of QueueConnector.cs with the following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is the **primary key** you previously obtained from the Azure portal.</span></span>
   
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
4. <span data-ttu-id="d6bd2-213">Now, ensure that your **Initialize** method gets called.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-213">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="d6bd2-214">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-214">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="d6bd2-215">Add the following line of code at the end of the **Application_Start** method.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-215">Add the following line of code at the end of the **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="d6bd2-216">Finally, update the web code you created earlier, to submit items to the queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-216">Finally, update the web code you created earlier, to submit items to the queue.</span></span> <span data-ttu-id="d6bd2-217">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-217">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="d6bd2-218">Update the `Submit()` method (the overload that takes no parameters) as follows to get the message count for the queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-218">Update the `Submit()` method (the overload that takes no parameters) as follows to get the message count for the queue.</span></span>
   
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
8. <span data-ttu-id="d6bd2-219">Update the `Submit(OnlineOrder order)` method (the overload that takes one parameter) as follows to submit order information to the queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-219">Update the `Submit(OnlineOrder order)` method (the overload that takes one parameter) as follows to submit order information to the queue.</span></span>
   
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
9. <span data-ttu-id="d6bd2-220">You can now run the application again.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-220">You can now run the application again.</span></span> <span data-ttu-id="d6bd2-221">Each time you submit an order, the message count increases.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-221">Each time you submit an order, the message count increases.</span></span>
   
   ![][18]

## <a name="create-the-worker-role"></a><span data-ttu-id="d6bd2-222">Create the worker role</span><span class="sxs-lookup"><span data-stu-id="d6bd2-222">Create the worker role</span></span>
<span data-ttu-id="d6bd2-223">You will now create the worker role that processes the order submissions.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-223">You will now create the worker role that processes the order submissions.</span></span> <span data-ttu-id="d6bd2-224">This example uses the **Worker Role with Service Bus Queue** Visual Studio project template.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-224">This example uses the **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="d6bd2-225">You already obtained the required credentials from the portal.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-225">You already obtained the required credentials from the portal.</span></span>

1. <span data-ttu-id="d6bd2-226">Make sure you have connected Visual Studio to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-226">Make sure you have connected Visual Studio to your Azure account.</span></span>
2. <span data-ttu-id="d6bd2-227">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under the **MultiTierApp** project.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-227">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under the **MultiTierApp** project.</span></span>
3. <span data-ttu-id="d6bd2-228">Click **Add**, and then click **New Worker Role Project**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-228">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="d6bd2-229">The **Add New Role Project** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-229">The **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="d6bd2-230">In the **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-230">In the **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="d6bd2-231">In the **Name** box, name the project **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-231">In the **Name** box, name the project **OrderProcessingRole**.</span></span> <span data-ttu-id="d6bd2-232">Then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-232">Then click **Add**.</span></span>
6. <span data-ttu-id="d6bd2-233">Copy the connection string that you obtained in step 9 of the "Create a Service Bus namespace" section to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-233">Copy the connection string that you obtained in step 9 of the "Create a Service Bus namespace" section to the clipboard.</span></span>
7. <span data-ttu-id="d6bd2-234">In **Solution Explorer**, right-click the **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not the class).</span><span class="sxs-lookup"><span data-stu-id="d6bd2-234">In **Solution Explorer**, right-click the **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not the class).</span></span> <span data-ttu-id="d6bd2-235">Then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-235">Then click **Properties**.</span></span>
8. <span data-ttu-id="d6bd2-236">On the **Settings** tab of the **Properties** dialog box, click inside the **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste the endpoint value you copied in step 6.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-236">On the **Settings** tab of the **Properties** dialog box, click inside the **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste the endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="d6bd2-237">Create an **OnlineOrder** class to represent the orders as you process them from the queue.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-237">Create an **OnlineOrder** class to represent the orders as you process them from the queue.</span></span> <span data-ttu-id="d6bd2-238">You can reuse a class you have already created.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-238">You can reuse a class you have already created.</span></span> <span data-ttu-id="d6bd2-239">In **Solution Explorer**, right-click the **OrderProcessingRole** class (right-click the class icon, not the role).</span><span class="sxs-lookup"><span data-stu-id="d6bd2-239">In **Solution Explorer**, right-click the **OrderProcessingRole** class (right-click the class icon, not the role).</span></span> <span data-ttu-id="d6bd2-240">Click **Add**, then click **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-240">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="d6bd2-241">Browse to the subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** to add it to this project.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-241">Browse to the subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** to add it to this project.</span></span>
11. <span data-ttu-id="d6bd2-242">In **WorkerRole.cs**, change the value of the **QueueName** variable from `"ProcessingQueue"` to `"OrdersQueue"` as shown in the following code.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-242">In **WorkerRole.cs**, change the value of the **QueueName** variable from `"ProcessingQueue"` to `"OrdersQueue"` as shown in the following code.</span></span>
    
    ```csharp
    // The name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="d6bd2-243">Add the following using statement at the top of the WorkerRole.cs file.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-243">Add the following using statement at the top of the WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="d6bd2-244">In the `Run()` function, inside the `OnMessage()` call, replace the contents of the `try` clause with the following code.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-244">In the `Run()` function, inside the `OnMessage()` call, replace the contents of the `try` clause with the following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View the message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="d6bd2-245">You have completed the application.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-245">You have completed the application.</span></span> <span data-ttu-id="d6bd2-246">You can test the full application by right-clicking the MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-246">You can test the full application by right-clicking the MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="d6bd2-247">Note that the message count does not increment, because the worker role processes items from the queue and marks them as complete.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-247">Note that the message count does not increment, because the worker role processes items from the queue and marks them as complete.</span></span> <span data-ttu-id="d6bd2-248">You can see the trace output of your worker role by viewing the Azure Compute Emulator UI.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-248">You can see the trace output of your worker role by viewing the Azure Compute Emulator UI.</span></span> <span data-ttu-id="d6bd2-249">You can do this by right-clicking the emulator icon in the notification area of your taskbar and selecting **Show Compute Emulator UI**.</span><span class="sxs-lookup"><span data-stu-id="d6bd2-249">You can do this by right-clicking the emulator icon in the notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="d6bd2-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6bd2-250">Next steps</span></span>
<span data-ttu-id="d6bd2-251">To learn more about Service Bus, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="d6bd2-251">To learn more about Service Bus, see the following resources:</span></span>  

* [<span data-ttu-id="d6bd2-252">Service Bus fundamentals</span><span class="sxs-lookup"><span data-stu-id="d6bd2-252">Service Bus fundamentals</span></span>](service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="d6bd2-253">[Get started using Service Bus queues][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="d6bd2-253">[Get started using Service Bus queues][sbacomqhowto]</span></span>
* <span data-ttu-id="d6bd2-254">[Service Bus service page][sbacom]</span><span class="sxs-lookup"><span data-stu-id="d6bd2-254">[Service Bus service page][sbacom]</span></span>  

<span data-ttu-id="d6bd2-255">To learn more about multi-tier scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="d6bd2-255">To learn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="d6bd2-256">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="d6bd2-256">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
