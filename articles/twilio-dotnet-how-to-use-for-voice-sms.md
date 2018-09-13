---
title: How to Use Twilio for Voice and SMS (.NET) | Microsoft Docs
description: Learn how to make a phone call and send a SMS message with the Twilio API service on Azure. Code samples written in .NET.
services: ''
documentationcenter: .net
author: devinrader
manager: twilio
editor: ''
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1442e3af26ae87e645cf207228ed1197b2afdd4d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555576"
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="93d63-104">How to use Twilio for voice and SMS capabilities from Azure</span><span class="sxs-lookup"><span data-stu-id="93d63-104">How to use Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="93d63-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span><span class="sxs-lookup"><span data-stu-id="93d63-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="93d63-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span><span class="sxs-lookup"><span data-stu-id="93d63-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="93d63-107">For more information on Twilio and using voice and SMS in your applications, see the [Next steps](#NextSteps) section.</span><span class="sxs-lookup"><span data-stu-id="93d63-107">For more information on Twilio and using voice and SMS in your applications, see the [Next steps](#NextSteps) section.</span></span>

## <a id="WhatIs"></a><span data-ttu-id="93d63-108">What is Twilio?</span><span class="sxs-lookup"><span data-stu-id="93d63-108">What is Twilio?</span></span>
<span data-ttu-id="93d63-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span><span class="sxs-lookup"><span data-stu-id="93d63-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="93d63-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span><span class="sxs-lookup"><span data-stu-id="93d63-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="93d63-111">Applications are simple to build and scalable.</span><span class="sxs-lookup"><span data-stu-id="93d63-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="93d63-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span><span class="sxs-lookup"><span data-stu-id="93d63-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="93d63-113">**Twilio Voice** allows your applications to make and receive phone calls.</span><span class="sxs-lookup"><span data-stu-id="93d63-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="93d63-114">**Twilio SMS** enables your applications to send and receive SMS messages.</span><span class="sxs-lookup"><span data-stu-id="93d63-114">**Twilio SMS** enables your applications to send and receive SMS messages.</span></span> <span data-ttu-id="93d63-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span><span class="sxs-lookup"><span data-stu-id="93d63-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <a id="Pricing"></a><span data-ttu-id="93d63-116">Twilio Pricing and Special Offers</span><span class="sxs-lookup"><span data-stu-id="93d63-116">Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="93d63-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span><span class="sxs-lookup"><span data-stu-id="93d63-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="93d63-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span><span class="sxs-lookup"><span data-stu-id="93d63-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="93d63-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="93d63-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="93d63-120">Twilio is a pay-as-you-go service.</span><span class="sxs-lookup"><span data-stu-id="93d63-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="93d63-121">There are no set-up fees, and you can close your account at any time.</span><span class="sxs-lookup"><span data-stu-id="93d63-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="93d63-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="93d63-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <a id="Concepts"></a><span data-ttu-id="93d63-123">Concepts</span><span class="sxs-lookup"><span data-stu-id="93d63-123">Concepts</span></span>
<span data-ttu-id="93d63-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span><span class="sxs-lookup"><span data-stu-id="93d63-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="93d63-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="93d63-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="93d63-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="93d63-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <a id="Verbs"></a><span data-ttu-id="93d63-127">Twilio verbs</span><span class="sxs-lookup"><span data-stu-id="93d63-127">Twilio verbs</span></span>
<span data-ttu-id="93d63-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span><span class="sxs-lookup"><span data-stu-id="93d63-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="93d63-129">The following is a list of Twilio verbs.</span><span class="sxs-lookup"><span data-stu-id="93d63-129">The following is a list of Twilio verbs.</span></span>  <span data-ttu-id="93d63-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="93d63-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="93d63-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span><span class="sxs-lookup"><span data-stu-id="93d63-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="93d63-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span><span class="sxs-lookup"><span data-stu-id="93d63-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="93d63-133">**&lt;Hangup&gt;**: Ends a call.</span><span class="sxs-lookup"><span data-stu-id="93d63-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="93d63-134">**&lt;Play&gt;**: Plays an audio file.</span><span class="sxs-lookup"><span data-stu-id="93d63-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="93d63-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span><span class="sxs-lookup"><span data-stu-id="93d63-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="93d63-136">**&lt;Record&gt;**: Records the caller's voice and returns an URL of a file that contains the recording.</span><span class="sxs-lookup"><span data-stu-id="93d63-136">**&lt;Record&gt;**: Records the caller's voice and returns an URL of a file that contains the recording.</span></span>
* <span data-ttu-id="93d63-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span><span class="sxs-lookup"><span data-stu-id="93d63-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="93d63-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span><span class="sxs-lookup"><span data-stu-id="93d63-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="93d63-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span><span class="sxs-lookup"><span data-stu-id="93d63-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="93d63-140">**&lt;Sms&gt;**: Sends an SMS message.</span><span class="sxs-lookup"><span data-stu-id="93d63-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <a id="TwiML"></a><span data-ttu-id="93d63-141">TwiML</span><span class="sxs-lookup"><span data-stu-id="93d63-141">TwiML</span></span>
<span data-ttu-id="93d63-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span><span class="sxs-lookup"><span data-stu-id="93d63-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="93d63-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span><span class="sxs-lookup"><span data-stu-id="93d63-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="93d63-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span><span class="sxs-lookup"><span data-stu-id="93d63-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="93d63-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span><span class="sxs-lookup"><span data-stu-id="93d63-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="93d63-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span><span class="sxs-lookup"><span data-stu-id="93d63-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="93d63-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="93d63-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="93d63-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="93d63-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <a id="CreateAccount"></a><span data-ttu-id="93d63-149">Create a Twilio Account</span><span class="sxs-lookup"><span data-stu-id="93d63-149">Create a Twilio Account</span></span>
<span data-ttu-id="93d63-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="93d63-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="93d63-151">You can start with a free account, and upgrade your account later.</span><span class="sxs-lookup"><span data-stu-id="93d63-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="93d63-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span><span class="sxs-lookup"><span data-stu-id="93d63-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="93d63-153">Both will be needed to make Twilio API calls.</span><span class="sxs-lookup"><span data-stu-id="93d63-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="93d63-154">To prevent unauthorized access to your account, keep your authentication token secure.</span><span class="sxs-lookup"><span data-stu-id="93d63-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="93d63-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span><span class="sxs-lookup"><span data-stu-id="93d63-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <a id="create_app"></a><span data-ttu-id="93d63-156">Create an Azure Application</span><span class="sxs-lookup"><span data-stu-id="93d63-156">Create an Azure Application</span></span>
<span data-ttu-id="93d63-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span><span class="sxs-lookup"><span data-stu-id="93d63-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="93d63-158">You add the Twilio .NET library and configure the role to use the Twilio .NET libraries.</span><span class="sxs-lookup"><span data-stu-id="93d63-158">You add the Twilio .NET library and configure the role to use the Twilio .NET libraries.</span></span>
<span data-ttu-id="93d63-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span><span class="sxs-lookup"><span data-stu-id="93d63-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <a id="configure_app"></a><span data-ttu-id="93d63-160">Configure Your Application to use Twilio Libraries</span><span class="sxs-lookup"><span data-stu-id="93d63-160">Configure Your Application to use Twilio Libraries</span></span>
<span data-ttu-id="93d63-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio to provide simple and easy ways to interact with the Twilio REST API and Twilio Client to generate TwiML responses.</span><span class="sxs-lookup"><span data-stu-id="93d63-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio to provide simple and easy ways to interact with the Twilio REST API and Twilio Client to generate TwiML responses.</span></span>

<span data-ttu-id="93d63-162">Twilio provides five libraries for .NET developers:</span><span class="sxs-lookup"><span data-stu-id="93d63-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="93d63-163">Library</span><span class="sxs-lookup"><span data-stu-id="93d63-163">Library</span></span>|<span data-ttu-id="93d63-164">Description</span><span class="sxs-lookup"><span data-stu-id="93d63-164">Description</span></span>
---|---
<span data-ttu-id="93d63-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="93d63-165">Twilio.API</span></span>|<span data-ttu-id="93d63-166">The core Twilio library that wraps the Twilio REST API in a friendly .NET library.</span><span class="sxs-lookup"><span data-stu-id="93d63-166">The core Twilio library that wraps the Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="93d63-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="93d63-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="93d63-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="93d63-168">Twilio.TwiML</span></span>|<span data-ttu-id="93d63-169">Provides a .NET friendly way to generate TwiML markup.</span><span class="sxs-lookup"><span data-stu-id="93d63-169">Provides a .NET friendly way to generate TwiML markup.</span></span>
<span data-ttu-id="93d63-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="93d63-170">Twilio.MVC</span></span>|<span data-ttu-id="93d63-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span><span class="sxs-lookup"><span data-stu-id="93d63-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="93d63-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="93d63-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="93d63-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span><span class="sxs-lookup"><span data-stu-id="93d63-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="93d63-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="93d63-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="93d63-175">Contains the Capability token generator for use with the Twilio Client JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="93d63-175">Contains the Capability token generator for use with the Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="93d63-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span><span class="sxs-lookup"><span data-stu-id="93d63-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="93d63-177">The samples provided in this guide use the Twilio.API library.</span><span class="sxs-lookup"><span data-stu-id="93d63-177">The samples provided in this guide use the Twilio.API library.</span></span>

<span data-ttu-id="93d63-178">The libraries can be [installed using the NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up to 2015.</span><span class="sxs-lookup"><span data-stu-id="93d63-178">The libraries can be [installed using the NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up to 2015.</span></span>  <span data-ttu-id="93d63-179">The source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using the libraries.</span><span class="sxs-lookup"><span data-stu-id="93d63-179">The source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using the libraries.</span></span>

<span data-ttu-id="93d63-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span><span class="sxs-lookup"><span data-stu-id="93d63-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="93d63-181">Installing the Twilio libraries requires version 1.6 of NuGet or higher.</span><span class="sxs-lookup"><span data-stu-id="93d63-181">Installing the Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="93d63-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="93d63-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="93d63-183">To install the latest version of NuGet, you must first uninstall the loaded version using the Visual Studio Extension Manager.</span><span class="sxs-lookup"><span data-stu-id="93d63-183">To install the latest version of NuGet, you must first uninstall the loaded version using the Visual Studio Extension Manager.</span></span> <span data-ttu-id="93d63-184">To do so, you must run Visual Studio as administrator.</span><span class="sxs-lookup"><span data-stu-id="93d63-184">To do so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="93d63-185">Otherwise, the Uninstall button is disabled.</span><span class="sxs-lookup"><span data-stu-id="93d63-185">Otherwise, the Uninstall button is disabled.</span></span>
>
>

### <a id="use_nuget"></a><span data-ttu-id="93d63-186">To add the Twilio libraries to your Visual Studio project:</span><span class="sxs-lookup"><span data-stu-id="93d63-186">To add the Twilio libraries to your Visual Studio project:</span></span>
1. <span data-ttu-id="93d63-187">Open your solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93d63-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="93d63-188">Right-click **References**.</span><span class="sxs-lookup"><span data-stu-id="93d63-188">Right-click **References**.</span></span>
3. <span data-ttu-id="93d63-189">Click **Manage NuGet Packages...**</span><span class="sxs-lookup"><span data-stu-id="93d63-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="93d63-190">Click **Online**.</span><span class="sxs-lookup"><span data-stu-id="93d63-190">Click **Online**.</span></span>
5. <span data-ttu-id="93d63-191">In the search online box, type *twilio*.</span><span class="sxs-lookup"><span data-stu-id="93d63-191">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="93d63-192">Click **Install** on the Twilio package.</span><span class="sxs-lookup"><span data-stu-id="93d63-192">Click **Install** on the Twilio package.</span></span>

## <a id="howto_make_call"></a><span data-ttu-id="93d63-193">How to: Make an outgoing call</span><span class="sxs-lookup"><span data-stu-id="93d63-193">How to: Make an outgoing call</span></span>
<span data-ttu-id="93d63-194">The following shows how to make an outgoing call using the **CallResource** class.</span><span class="sxs-lookup"><span data-stu-id="93d63-194">The following shows how to make an outgoing call using the **CallResource** class.</span></span> <span data-ttu-id="93d63-195">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span><span class="sxs-lookup"><span data-stu-id="93d63-195">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="93d63-196">Substitute your values for the **to** and **from** phone numbers, and ensure that you verify the **from** phone number for your Twilio account before running the code.</span><span class="sxs-lookup"><span data-stu-id="93d63-196">Substitute your values for the **to** and **from** phone numbers, and ensure that you verify the **from** phone number for your Twilio account before running the code.</span></span>

    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize the TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set the call From, To, and URL values to use for the call.
    // This sample uses the sandbox number provided by
    // Twilio to make the call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="93d63-197">For more information about the parameters passed in to the **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="93d63-197">For more information about the parameters passed in to the **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="93d63-198">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span><span class="sxs-lookup"><span data-stu-id="93d63-198">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="93d63-199">You could instead use your own site to provide the TwiML response.</span><span class="sxs-lookup"><span data-stu-id="93d63-199">You could instead use your own site to provide the TwiML response.</span></span> <span data-ttu-id="93d63-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="93d63-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <a id="howto_send_sms"></a><span data-ttu-id="93d63-201">How to: Send an SMS message</span><span class="sxs-lookup"><span data-stu-id="93d63-201">How to: Send an SMS message</span></span>
<span data-ttu-id="93d63-202">The following screenshot shows how to send an SMS message using the **MessageResource**  class.</span><span class="sxs-lookup"><span data-stu-id="93d63-202">The following screenshot shows how to send an SMS message using the **MessageResource**  class.</span></span> <span data-ttu-id="93d63-203">The **from** number is provided by Twilio for trial accounts to send SMS messages.</span><span class="sxs-lookup"><span data-stu-id="93d63-203">The **from** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="93d63-204">The **to** number must be verified for your Twilio account before you run the code.</span><span class="sxs-lookup"><span data-stu-id="93d63-204">The **to** number must be verified for your Twilio account before you run the code.</span></span>

    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize the TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making the REST call
        Console.WriteLine(ex.Message);
    }

## <a id="howto_provide_twiml_responses"></a><span data-ttu-id="93d63-205">How to: Provide TwiML Responses from your own website</span><span class="sxs-lookup"><span data-stu-id="93d63-205">How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="93d63-206">When your application initiates a call to the Twilio API - for example, via the **CallResource.Create** method - Twilio sends your request to an URL that is expected to return a TwiML response.</span><span class="sxs-lookup"><span data-stu-id="93d63-206">When your application initiates a call to the Twilio API - for example, via the **CallResource.Create** method - Twilio sends your request to an URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="93d63-207">The example in [How to: Make an outgoing call](#howto_make_call) uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] to return the response.</span><span class="sxs-lookup"><span data-stu-id="93d63-207">The example in [How to: Make an outgoing call](#howto_make_call) uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] to return the response.</span></span>

> [!NOTE]
> <span data-ttu-id="93d63-208">While TwiML is designed for use by web services, you can view the TwiML in your browser.</span><span class="sxs-lookup"><span data-stu-id="93d63-208">While TwiML is designed for use by web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="93d63-209">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) to see a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span><span class="sxs-lookup"><span data-stu-id="93d63-209">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) to see a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="93d63-210">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span><span class="sxs-lookup"><span data-stu-id="93d63-210">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="93d63-211">You can create the site in any language that returns HTTP responses.</span><span class="sxs-lookup"><span data-stu-id="93d63-211">You can create the site in any language that returns HTTP responses.</span></span> <span data-ttu-id="93d63-212">This topic assumes you'll be hosting the URL from an ASP.NET generic handler.</span><span class="sxs-lookup"><span data-stu-id="93d63-212">This topic assumes you'll be hosting the URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="93d63-213">The following ASP.NET Handler crafts a TwiML response that says **Hello World** on the call.</span><span class="sxs-lookup"><span data-stu-id="93d63-213">The following ASP.NET Handler crafts a TwiML response that says **Hello World** on the call.</span></span>

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
<span data-ttu-id="93d63-214">As you can see from the example above, the TwiML response is simply an XML document.</span><span class="sxs-lookup"><span data-stu-id="93d63-214">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="93d63-215">The Twilio.TwiML library contains classes that will generate TwiML for you.</span><span class="sxs-lookup"><span data-stu-id="93d63-215">The Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="93d63-216">The example below produces the equivalent response as shown above, but uses the **VoiceResponse** class.</span><span class="sxs-lookup"><span data-stu-id="93d63-216">The example below produces the equivalent response as shown above, but uses the **VoiceResponse** class.</span></span>

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

<span data-ttu-id="93d63-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="93d63-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="93d63-218">Once you have set up a way to provide TwiML responses, you can pass that URL to the **CallResource.Create** method.</span><span class="sxs-lookup"><span data-stu-id="93d63-218">Once you have set up a way to provide TwiML responses, you can pass that URL to the **CallResource.Create** method.</span></span> <span data-ttu-id="93d63-219">For example, if you have a web application named MyTwiML deployed to an Azure cloud service, and the name of your ASP.NET Handler is mytwiml.ashx, the URL can be passed to **CallResource.Create** as shown in the following code sample:</span><span class="sxs-lookup"><span data-stu-id="93d63-219">For example, if you have a web application named MyTwiML deployed to an Azure cloud service, and the name of your ASP.NET Handler is mytwiml.ashx, the URL can be passed to **CallResource.Create** as shown in the following code sample:</span></span>

    // This sample uses the sandbox number provided by Twilio to make the call.
    // Place the call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="93d63-220">For additional information about using Twilio on Azure with ASP.NET, see [How to make a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="93d63-220">For additional information about using Twilio on Azure with ASP.NET, see [How to make a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
