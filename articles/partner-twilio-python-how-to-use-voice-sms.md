---
title: How to Use Twilio for Voice and SMS (Python) | Microsoft Docs
description: Learn how to make a phone call and send a SMS message with the Twilio API service on Azure. Code samples written in Python.
services: ''
documentationcenter: python
author: devinrader
manager: twilio
editor: ''
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f4a02bb7a7c46e7a0e3c75b870c522eae8294339
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553084"
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="3b892-104">How to Use Twilio for Voice and SMS Capabilities in Python</span><span class="sxs-lookup"><span data-stu-id="3b892-104">How to Use Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="3b892-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span><span class="sxs-lookup"><span data-stu-id="3b892-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="3b892-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span><span class="sxs-lookup"><span data-stu-id="3b892-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="3b892-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span><span class="sxs-lookup"><span data-stu-id="3b892-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <a id="WhatIs"></a><span data-ttu-id="3b892-108">What is Twilio?</span><span class="sxs-lookup"><span data-stu-id="3b892-108">What is Twilio?</span></span>
<span data-ttu-id="3b892-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span><span class="sxs-lookup"><span data-stu-id="3b892-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="3b892-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span><span class="sxs-lookup"><span data-stu-id="3b892-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="3b892-111">Applications are simple to build and scalable.</span><span class="sxs-lookup"><span data-stu-id="3b892-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="3b892-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span><span class="sxs-lookup"><span data-stu-id="3b892-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="3b892-113">**Twilio Voice** allows your applications to make and receive phone calls.</span><span class="sxs-lookup"><span data-stu-id="3b892-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span>
<span data-ttu-id="3b892-114">**Twilio SMS** enables your application to send and receive text messages.</span><span class="sxs-lookup"><span data-stu-id="3b892-114">**Twilio SMS** enables your application to send and receive text messages.</span></span>
<span data-ttu-id="3b892-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span><span class="sxs-lookup"><span data-stu-id="3b892-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <a id="Pricing"></a><span data-ttu-id="3b892-116">Twilio Pricing and Special Offers</span><span class="sxs-lookup"><span data-stu-id="3b892-116">Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="3b892-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span><span class="sxs-lookup"><span data-stu-id="3b892-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="3b892-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span><span class="sxs-lookup"><span data-stu-id="3b892-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="3b892-119">Redeem this [Twilio credit][special_offer] and get started.</span><span class="sxs-lookup"><span data-stu-id="3b892-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="3b892-120">Twilio is a pay-as-you-go service.</span><span class="sxs-lookup"><span data-stu-id="3b892-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="3b892-121">There are no set-up fees and you can close your account at any time.</span><span class="sxs-lookup"><span data-stu-id="3b892-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="3b892-122">You can find more details at [Twilio Pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="3b892-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <a id="Concepts"></a><span data-ttu-id="3b892-123">Concepts</span><span class="sxs-lookup"><span data-stu-id="3b892-123">Concepts</span></span>
<span data-ttu-id="3b892-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span><span class="sxs-lookup"><span data-stu-id="3b892-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="3b892-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="3b892-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="3b892-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="3b892-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <a id="Verbs"></a><span data-ttu-id="3b892-127">Twilio Verbs</span><span class="sxs-lookup"><span data-stu-id="3b892-127">Twilio Verbs</span></span>
<span data-ttu-id="3b892-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span><span class="sxs-lookup"><span data-stu-id="3b892-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="3b892-129">The following is a list of Twilio verbs.</span><span class="sxs-lookup"><span data-stu-id="3b892-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="3b892-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span><span class="sxs-lookup"><span data-stu-id="3b892-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="3b892-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span><span class="sxs-lookup"><span data-stu-id="3b892-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="3b892-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span><span class="sxs-lookup"><span data-stu-id="3b892-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="3b892-133">**&lt;Hangup&gt;**: Ends a call.</span><span class="sxs-lookup"><span data-stu-id="3b892-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="3b892-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span><span class="sxs-lookup"><span data-stu-id="3b892-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="3b892-135">**&lt;Play&gt;**: Plays an audio file.</span><span class="sxs-lookup"><span data-stu-id="3b892-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="3b892-136">**&lt;Queue&gt;**: Add the to a queue of callers.</span><span class="sxs-lookup"><span data-stu-id="3b892-136">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="3b892-137">**&lt;Record&gt;**: Records the voice of the caller and returns a URL of a file that contains the recording.</span><span class="sxs-lookup"><span data-stu-id="3b892-137">**&lt;Record&gt;**: Records the voice of the caller and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="3b892-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span><span class="sxs-lookup"><span data-stu-id="3b892-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="3b892-139">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span><span class="sxs-lookup"><span data-stu-id="3b892-139">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="3b892-140">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span><span class="sxs-lookup"><span data-stu-id="3b892-140">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="3b892-141">**&lt;Sms&gt;**: Sends an SMS message.</span><span class="sxs-lookup"><span data-stu-id="3b892-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <a id="TwiML"></a><span data-ttu-id="3b892-142">TwiML</span><span class="sxs-lookup"><span data-stu-id="3b892-142">TwiML</span></span>
<span data-ttu-id="3b892-143">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span><span class="sxs-lookup"><span data-stu-id="3b892-143">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="3b892-144">As an example, the following TwiML would convert the text **Hello World** to speech.</span><span class="sxs-lookup"><span data-stu-id="3b892-144">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="3b892-145">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span><span class="sxs-lookup"><span data-stu-id="3b892-145">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="3b892-146">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span><span class="sxs-lookup"><span data-stu-id="3b892-146">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="3b892-147">You could also host your own URLs to produce the TwiML responses, and another option is to use the `TwiMLResponse` object.</span><span class="sxs-lookup"><span data-stu-id="3b892-147">You could also host your own URLs to produce the TwiML responses, and another option is to use the `TwiMLResponse` object.</span></span>

<span data-ttu-id="3b892-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="3b892-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="3b892-149">For additional information about the Twilio API, see [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="3b892-149">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <a id="CreateAccount"></a><span data-ttu-id="3b892-150">Create a Twilio Account</span><span class="sxs-lookup"><span data-stu-id="3b892-150">Create a Twilio Account</span></span>
<span data-ttu-id="3b892-151">When you are ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="3b892-151">When you are ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="3b892-152">You can start with a free account, and upgrade your account later.</span><span class="sxs-lookup"><span data-stu-id="3b892-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="3b892-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span><span class="sxs-lookup"><span data-stu-id="3b892-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="3b892-154">Both will be needed to make Twilio API calls.</span><span class="sxs-lookup"><span data-stu-id="3b892-154">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="3b892-155">To prevent unauthorized access to your account, keep your authentication token secure.</span><span class="sxs-lookup"><span data-stu-id="3b892-155">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="3b892-156">Your account SID and authentication token are viewable in the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span><span class="sxs-lookup"><span data-stu-id="3b892-156">Your account SID and authentication token are viewable in the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <a id="create_app"></a><span data-ttu-id="3b892-157">Create a Python Application</span><span class="sxs-lookup"><span data-stu-id="3b892-157">Create a Python Application</span></span>
<span data-ttu-id="3b892-158">A Python application that uses the Twilio service and is running in Azure is no different than any other Python application that uses the Twilio service.</span><span class="sxs-lookup"><span data-stu-id="3b892-158">A Python application that uses the Twilio service and is running in Azure is no different than any other Python application that uses the Twilio service.</span></span> <span data-ttu-id="3b892-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how to use Twilio services with [Twilio library for Python from GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="3b892-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how to use Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="3b892-160">For more information about using the Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="3b892-160">For more information about using the Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="3b892-161">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Python web application.</span><span class="sxs-lookup"><span data-stu-id="3b892-161">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Python web application.</span></span> <span data-ttu-id="3b892-162">Once the Virtual Machine is running, you will need to expose your application on a public port as described below.</span><span class="sxs-lookup"><span data-stu-id="3b892-162">Once the Virtual Machine is running, you will need to expose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="3b892-163">Add An Incoming Rule</span><span class="sxs-lookup"><span data-stu-id="3b892-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="3b892-164">Go to the [Network Security Group][azure_nsg] page.</span><span class="sxs-lookup"><span data-stu-id="3b892-164">Go to the [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="3b892-165">Select the Network Security Group that corresponds with your Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="3b892-165">Select the Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="3b892-166">Add and **Outgoing Rule** for **port 80**.</span><span class="sxs-lookup"><span data-stu-id="3b892-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="3b892-167">Be sure to allow incoming from any address.</span><span class="sxs-lookup"><span data-stu-id="3b892-167">Be sure to allow incoming from any address.</span></span>

### <a name="set-the-dns-name-label"></a><span data-ttu-id="3b892-168">Set the DNS Name Label</span><span class="sxs-lookup"><span data-stu-id="3b892-168">Set the DNS Name Label</span></span>
  1. <span data-ttu-id="3b892-169">Go to the [The Public IP Adresses][azure_ips] page.</span><span class="sxs-lookup"><span data-stu-id="3b892-169">Go to the [The Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="3b892-170">Select the Public IP that correspends with your Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="3b892-170">Select the Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="3b892-171">Set the **DNS Name Label** in the **Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="3b892-171">Set the **DNS Name Label** in the **Configuration** section.</span></span> <span data-ttu-id="3b892-172">In the case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="3b892-172">In the case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="3b892-173">Once you are able to connect through SSH to the Virtual Machine you can install the Web Framework of your choice (the two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="3b892-173">Once you are able to connect through SSH to the Virtual Machine you can install the Web Framework of your choice (the two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="3b892-174">You can install either of them just by running the `pip install` command.</span><span class="sxs-lookup"><span data-stu-id="3b892-174">You can install either of them just by running the `pip install` command.</span></span>

<span data-ttu-id="3b892-175">Keep in mind that we configured the Virtual Machine to allow traffic only on port 80.</span><span class="sxs-lookup"><span data-stu-id="3b892-175">Keep in mind that we configured the Virtual Machine to allow traffic only on port 80.</span></span> <span data-ttu-id="3b892-176">So make sure to configure the application to use this port.</span><span class="sxs-lookup"><span data-stu-id="3b892-176">So make sure to configure the application to use this port.</span></span>

## <a id="configure_app"></a><span data-ttu-id="3b892-177">Configure Your Application to Use Twilio Libraries</span><span class="sxs-lookup"><span data-stu-id="3b892-177">Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="3b892-178">You can configure your application to use the Twilio library for Python in two ways:</span><span class="sxs-lookup"><span data-stu-id="3b892-178">You can configure your application to use the Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="3b892-179">Install the Twilio library for Python as a Pip package.</span><span class="sxs-lookup"><span data-stu-id="3b892-179">Install the Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="3b892-180">It can be installed with the following commands:</span><span class="sxs-lookup"><span data-stu-id="3b892-180">It can be installed with the following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="3b892-181">-OR-</span><span class="sxs-lookup"><span data-stu-id="3b892-181">-OR-</span></span>

* <span data-ttu-id="3b892-182">Download the Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span><span class="sxs-lookup"><span data-stu-id="3b892-182">Download the Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="3b892-183">Once you have installed the Twilio library for Python, you can then `import` it in your Python files:</span><span class="sxs-lookup"><span data-stu-id="3b892-183">Once you have installed the Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="3b892-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="3b892-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <a id="howto_make_call"></a><span data-ttu-id="3b892-185">How to: Make an outgoing call</span><span class="sxs-lookup"><span data-stu-id="3b892-185">How to: Make an outgoing call</span></span>
<span data-ttu-id="3b892-186">The following shows how to make an outgoing call.</span><span class="sxs-lookup"><span data-stu-id="3b892-186">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="3b892-187">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span><span class="sxs-lookup"><span data-stu-id="3b892-187">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="3b892-188">Substitute your values for the **from_number** and **to_number** phone numbers, and ensure that you've verified the **from_number** phone number for your Twilio account before running the code.</span><span class="sxs-lookup"><span data-stu-id="3b892-188">Substitute your values for the **from_number** and **to_number** phone numbers, and ensure that you've verified the **from_number** phone number for your Twilio account before running the code.</span></span>

    from urllib.parse import urlencode

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # The number of the phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use the Twilio-provided site for the TwiML response.
    url = "http://twimlets.com/message?"

    # The phone message text.
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="3b892-189">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span><span class="sxs-lookup"><span data-stu-id="3b892-189">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="3b892-190">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="3b892-190">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <a id="howto_send_sms"></a><span data-ttu-id="3b892-191">How to: Send an SMS message</span><span class="sxs-lookup"><span data-stu-id="3b892-191">How to: Send an SMS message</span></span>
<span data-ttu-id="3b892-192">The following shows how to send an SMS message using the `TwilioRestClient` class.</span><span class="sxs-lookup"><span data-stu-id="3b892-192">The following shows how to send an SMS message using the `TwilioRestClient` class.</span></span> <span data-ttu-id="3b892-193">The **from_number** number is provided by Twilio for trial accounts to send SMS messages.</span><span class="sxs-lookup"><span data-stu-id="3b892-193">The **from_number** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="3b892-194">The **to_number** number must be verified for your Twilio account before running the code.</span><span class="sxs-lookup"><span data-stu-id="3b892-194">The **to_number** number must be verified for your Twilio account before running the code.</span></span>

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send the SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <a id="howto_provide_twiml_responses"></a><span data-ttu-id="3b892-195">How to: Provide TwiML Responses from your own Website</span><span class="sxs-lookup"><span data-stu-id="3b892-195">How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="3b892-196">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span><span class="sxs-lookup"><span data-stu-id="3b892-196">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="3b892-197">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="3b892-197">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="3b892-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span><span class="sxs-lookup"><span data-stu-id="3b892-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="3b892-199">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span><span class="sxs-lookup"><span data-stu-id="3b892-199">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="3b892-200">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span><span class="sxs-lookup"><span data-stu-id="3b892-200">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="3b892-201">You can create the site in any language that returns XML responses; this topic assumes you will be using Python to create the TwiML.</span><span class="sxs-lookup"><span data-stu-id="3b892-201">You can create the site in any language that returns XML responses; this topic assumes you will be using Python to create the TwiML.</span></span>

<span data-ttu-id="3b892-202">The following examples will output a TwiML response that says **Hello World** on the call.</span><span class="sxs-lookup"><span data-stu-id="3b892-202">The following examples will output a TwiML response that says **Hello World** on the call.</span></span>

<span data-ttu-id="3b892-203">With Flask:</span><span class="sxs-lookup"><span data-stu-id="3b892-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="3b892-204">With Django:</span><span class="sxs-lookup"><span data-stu-id="3b892-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="3b892-205">As you can see from the example above, the TwiML response is simply an XML document.</span><span class="sxs-lookup"><span data-stu-id="3b892-205">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="3b892-206">The Twilio library for Python contains classes that will generate TwiML for you.</span><span class="sxs-lookup"><span data-stu-id="3b892-206">The Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="3b892-207">The example below produces the equivalent response as shown above, but uses the `twiml` module in the Twilio library for Python:</span><span class="sxs-lookup"><span data-stu-id="3b892-207">The example below produces the equivalent response as shown above, but uses the `twiml` module in the Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="3b892-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="3b892-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="3b892-209">Once you have your Python application set up to provide TwiML responses, use the URL of the application as the URL passed into the `client.calls.create`  method.</span><span class="sxs-lookup"><span data-stu-id="3b892-209">Once you have your Python application set up to provide TwiML responses, use the URL of the application as the URL passed into the `client.calls.create`  method.</span></span> <span data-ttu-id="3b892-210">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, you can use its url as webhook as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="3b892-210">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, you can use its url as webhook as shown in the following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <a id="AdditionalServices"></a><span data-ttu-id="3b892-211">How to: Use Additional Twilio Services</span><span class="sxs-lookup"><span data-stu-id="3b892-211">How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="3b892-212">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span><span class="sxs-lookup"><span data-stu-id="3b892-212">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="3b892-213">For full details, see the [Twilio API documentation][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="3b892-213">For full details, see the [Twilio API documentation][twilio_api].</span></span>

## <a id="NextSteps"></a><span data-ttu-id="3b892-214">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3b892-214">Next Steps</span></span>
<span data-ttu-id="3b892-215">Now that you have learned the basics of the Twilio service, follow these links to learn more:</span><span class="sxs-lookup"><span data-stu-id="3b892-215">Now that you have learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="3b892-216">[Twilio Security Guidelines][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="3b892-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="3b892-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="3b892-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="3b892-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="3b892-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="3b892-219">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="3b892-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="3b892-220">[Talk to Twilio Support][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="3b892-220">[Talk to Twilio Support][twilio_support]</span></span>

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
