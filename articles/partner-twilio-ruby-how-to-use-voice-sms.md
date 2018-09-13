---
title: How to Use Twilio for Voice and SMS (Ruby) | Microsoft Docs
description: Learn how to make a phone call and send a SMS message with the Twilio API service on Azure. Code samples written in Ruby.
services: ''
documentationcenter: ruby
author: devinrader
manager: twilio
editor: ''
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552534"
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="21515-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span><span class="sxs-lookup"><span data-stu-id="21515-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="21515-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span><span class="sxs-lookup"><span data-stu-id="21515-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="21515-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span><span class="sxs-lookup"><span data-stu-id="21515-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="21515-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span><span class="sxs-lookup"><span data-stu-id="21515-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <a id="WhatIs"></a><span data-ttu-id="21515-108">What is Twilio?</span><span class="sxs-lookup"><span data-stu-id="21515-108">What is Twilio?</span></span>
<span data-ttu-id="21515-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span><span class="sxs-lookup"><span data-stu-id="21515-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="21515-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span><span class="sxs-lookup"><span data-stu-id="21515-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="21515-111">**Twilio Voice** allows your applications to make and receive phone calls.</span><span class="sxs-lookup"><span data-stu-id="21515-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="21515-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span><span class="sxs-lookup"><span data-stu-id="21515-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="21515-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span><span class="sxs-lookup"><span data-stu-id="21515-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <a id="Pricing"></a><span data-ttu-id="21515-114">Twilio Pricing and Special Offers</span><span class="sxs-lookup"><span data-stu-id="21515-114">Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="21515-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="21515-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="21515-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span><span class="sxs-lookup"><span data-stu-id="21515-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="21515-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="21515-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <a id="Concepts"></a><span data-ttu-id="21515-118">Concepts</span><span class="sxs-lookup"><span data-stu-id="21515-118">Concepts</span></span>
<span data-ttu-id="21515-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span><span class="sxs-lookup"><span data-stu-id="21515-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="21515-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="21515-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <a id="TwiML"></a><span data-ttu-id="21515-121">TwiML</span><span class="sxs-lookup"><span data-stu-id="21515-121">TwiML</span></span>
<span data-ttu-id="21515-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span><span class="sxs-lookup"><span data-stu-id="21515-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="21515-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span><span class="sxs-lookup"><span data-stu-id="21515-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="21515-124">All TwiML documents have `<Response>` as their root element.</span><span class="sxs-lookup"><span data-stu-id="21515-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="21515-125">From there, you use Twilio Verbs to define the behavior of your application.</span><span class="sxs-lookup"><span data-stu-id="21515-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <a id="Verbs"></a><span data-ttu-id="21515-126">TwiML Verbs</span><span class="sxs-lookup"><span data-stu-id="21515-126">TwiML Verbs</span></span>
<span data-ttu-id="21515-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span><span class="sxs-lookup"><span data-stu-id="21515-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="21515-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span><span class="sxs-lookup"><span data-stu-id="21515-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="21515-129">The following is a list of Twilio verbs.</span><span class="sxs-lookup"><span data-stu-id="21515-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="21515-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span><span class="sxs-lookup"><span data-stu-id="21515-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="21515-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span><span class="sxs-lookup"><span data-stu-id="21515-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="21515-132">**&lt;Hangup&gt;**: Ends a call.</span><span class="sxs-lookup"><span data-stu-id="21515-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="21515-133">**&lt;Play&gt;**: Plays an audio file.</span><span class="sxs-lookup"><span data-stu-id="21515-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="21515-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span><span class="sxs-lookup"><span data-stu-id="21515-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="21515-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span><span class="sxs-lookup"><span data-stu-id="21515-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="21515-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span><span class="sxs-lookup"><span data-stu-id="21515-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="21515-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span><span class="sxs-lookup"><span data-stu-id="21515-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="21515-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span><span class="sxs-lookup"><span data-stu-id="21515-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="21515-139">**&lt;Sms&gt;**: Sends an SMS message.</span><span class="sxs-lookup"><span data-stu-id="21515-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="21515-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="21515-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="21515-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="21515-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <a id="CreateAccount"></a><span data-ttu-id="21515-142">Create a Twilio Account</span><span class="sxs-lookup"><span data-stu-id="21515-142">Create a Twilio Account</span></span>
<span data-ttu-id="21515-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="21515-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="21515-144">You can start with a free account, and upgrade your account later.</span><span class="sxs-lookup"><span data-stu-id="21515-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="21515-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span><span class="sxs-lookup"><span data-stu-id="21515-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="21515-146">You'll also receive an account SID and an auth token.</span><span class="sxs-lookup"><span data-stu-id="21515-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="21515-147">Both will be needed to make Twilio API calls.</span><span class="sxs-lookup"><span data-stu-id="21515-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="21515-148">To prevent unauthorized access to your account, keep your authentication token secure.</span><span class="sxs-lookup"><span data-stu-id="21515-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="21515-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span><span class="sxs-lookup"><span data-stu-id="21515-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <a id="VerifyPhoneNumbers"></a><span data-ttu-id="21515-150">Verify Phone Numbers</span><span class="sxs-lookup"><span data-stu-id="21515-150">Verify Phone Numbers</span></span>
<span data-ttu-id="21515-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span><span class="sxs-lookup"><span data-stu-id="21515-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="21515-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="21515-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <a id="create_app"></a><span data-ttu-id="21515-153">Create a Ruby Application</span><span class="sxs-lookup"><span data-stu-id="21515-153">Create a Ruby Application</span></span>
<span data-ttu-id="21515-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span><span class="sxs-lookup"><span data-stu-id="21515-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="21515-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="21515-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="21515-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span><span class="sxs-lookup"><span data-stu-id="21515-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="21515-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span><span class="sxs-lookup"><span data-stu-id="21515-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="21515-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span><span class="sxs-lookup"><span data-stu-id="21515-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="21515-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span><span class="sxs-lookup"><span data-stu-id="21515-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="21515-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span><span class="sxs-lookup"><span data-stu-id="21515-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="21515-161">SSH into your new VM and create a directory for your new app.</span><span class="sxs-lookup"><span data-stu-id="21515-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="21515-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span><span class="sxs-lookup"><span data-stu-id="21515-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="21515-163">On the command line run `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="21515-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="21515-164">This will install the dependencies above.</span><span class="sxs-lookup"><span data-stu-id="21515-164">This will install the dependencies above.</span></span> <span data-ttu-id="21515-165">Next create a file called `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="21515-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="21515-166">This will be where the code for your web app lives.</span><span class="sxs-lookup"><span data-stu-id="21515-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="21515-167">Paste the following code into it:</span><span class="sxs-lookup"><span data-stu-id="21515-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="21515-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="21515-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="21515-169">This will spin-up a small web server on port 5000.</span><span class="sxs-lookup"><span data-stu-id="21515-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="21515-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span><span class="sxs-lookup"><span data-stu-id="21515-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="21515-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span><span class="sxs-lookup"><span data-stu-id="21515-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <a id="configure_app"></a><span data-ttu-id="21515-172">Configure Your Application to Use Twilio</span><span class="sxs-lookup"><span data-stu-id="21515-172">Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="21515-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span><span class="sxs-lookup"><span data-stu-id="21515-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="21515-174">On the command line, run `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="21515-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="21515-175">Now open `web.rb` and including this line at the top:</span><span class="sxs-lookup"><span data-stu-id="21515-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="21515-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span><span class="sxs-lookup"><span data-stu-id="21515-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <a id="howto_make_call"></a><span data-ttu-id="21515-177">How to: Make an outgoing call</span><span class="sxs-lookup"><span data-stu-id="21515-177">How to: Make an outgoing call</span></span>
<span data-ttu-id="21515-178">The following shows how to make an outgoing call.</span><span class="sxs-lookup"><span data-stu-id="21515-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="21515-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span><span class="sxs-lookup"><span data-stu-id="21515-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="21515-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span><span class="sxs-lookup"><span data-stu-id="21515-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="21515-181">Add this function to `web.md`:</span><span class="sxs-lookup"><span data-stu-id="21515-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="21515-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span><span class="sxs-lookup"><span data-stu-id="21515-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="21515-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span><span class="sxs-lookup"><span data-stu-id="21515-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="21515-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span><span class="sxs-lookup"><span data-stu-id="21515-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="21515-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span><span class="sxs-lookup"><span data-stu-id="21515-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <a id="howto_recieve_sms"></a><span data-ttu-id="21515-186">How to: Recieve an SMS message</span><span class="sxs-lookup"><span data-stu-id="21515-186">How to: Recieve an SMS message</span></span>
<span data-ttu-id="21515-187">In the previous example we initiated an **outgoing** phone call.</span><span class="sxs-lookup"><span data-stu-id="21515-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="21515-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span><span class="sxs-lookup"><span data-stu-id="21515-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="21515-189">First, log-in to your [Twilio dashboard][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="21515-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="21515-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span><span class="sxs-lookup"><span data-stu-id="21515-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="21515-191">You'll see two URLs that you can configure.</span><span class="sxs-lookup"><span data-stu-id="21515-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="21515-192">A Voice Request URL and an SMS Request URL.</span><span class="sxs-lookup"><span data-stu-id="21515-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="21515-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span><span class="sxs-lookup"><span data-stu-id="21515-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="21515-194">The URLs are also known as "web hooks".</span><span class="sxs-lookup"><span data-stu-id="21515-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="21515-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="21515-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="21515-196">Go ahead and click Save Changes at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="21515-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="21515-197">Now, back in `web.rb` let's program our application to handle this:</span><span class="sxs-lookup"><span data-stu-id="21515-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="21515-198">After making the change, make sure to re-start your web app.</span><span class="sxs-lookup"><span data-stu-id="21515-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="21515-199">Now, take out your phone and send an SMS to your Twilio number.</span><span class="sxs-lookup"><span data-stu-id="21515-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="21515-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span><span class="sxs-lookup"><span data-stu-id="21515-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="21515-201">Twilio and Azure rock!".</span><span class="sxs-lookup"><span data-stu-id="21515-201">Twilio and Azure rock!".</span></span>

## <a id="additional_services"></a><span data-ttu-id="21515-202">How to: Use Additional Twilio Services</span><span class="sxs-lookup"><span data-stu-id="21515-202">How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="21515-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span><span class="sxs-lookup"><span data-stu-id="21515-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="21515-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="21515-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <a id="NextSteps"></a><span data-ttu-id="21515-205">Next Steps</span><span class="sxs-lookup"><span data-stu-id="21515-205">Next Steps</span></span>
<span data-ttu-id="21515-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span><span class="sxs-lookup"><span data-stu-id="21515-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="21515-207">[Twilio Security Guidelines][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="21515-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="21515-208">[Twilio HowTos and Example Code][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="21515-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="21515-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="21515-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="21515-210">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="21515-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="21515-211">[Talk to Twilio Support][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="21515-211">[Talk to Twilio Support][twilio_support]</span></span>

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
