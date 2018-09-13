---
title: How to Use Twilio for Voice and SMS (PHP) | Microsoft Docs
description: Learn how to make a phone call and send a SMS message with the Twilio API service on Azure. Code samples written in PHP.
documentationcenter: php
services: ''
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: bd50eac7390e8639f77894689388e6926cdb619c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555718"
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="5fc33-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span><span class="sxs-lookup"><span data-stu-id="5fc33-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="5fc33-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc33-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="5fc33-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span><span class="sxs-lookup"><span data-stu-id="5fc33-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="5fc33-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span><span class="sxs-lookup"><span data-stu-id="5fc33-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <a id="WhatIs"></a><span data-ttu-id="5fc33-108">What is Twilio?</span><span class="sxs-lookup"><span data-stu-id="5fc33-108">What is Twilio?</span></span>
<span data-ttu-id="5fc33-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span><span class="sxs-lookup"><span data-stu-id="5fc33-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="5fc33-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span><span class="sxs-lookup"><span data-stu-id="5fc33-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="5fc33-111">Applications are simple to build and scalable.</span><span class="sxs-lookup"><span data-stu-id="5fc33-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="5fc33-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span><span class="sxs-lookup"><span data-stu-id="5fc33-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="5fc33-113">**Twilio Voice** allows your applications to make and receive phone calls.</span><span class="sxs-lookup"><span data-stu-id="5fc33-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="5fc33-114">**Twilio SMS** enables your application to send and receive text messages.</span><span class="sxs-lookup"><span data-stu-id="5fc33-114">**Twilio SMS** enables your application to send and receive text messages.</span></span> <span data-ttu-id="5fc33-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span><span class="sxs-lookup"><span data-stu-id="5fc33-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <a id="Pricing"></a><span data-ttu-id="5fc33-116">Twilio Pricing and Special Offers</span><span class="sxs-lookup"><span data-stu-id="5fc33-116">Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="5fc33-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span><span class="sxs-lookup"><span data-stu-id="5fc33-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="5fc33-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span><span class="sxs-lookup"><span data-stu-id="5fc33-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="5fc33-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="5fc33-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="5fc33-120">Twilio is a pay-as-you-go service.</span><span class="sxs-lookup"><span data-stu-id="5fc33-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="5fc33-121">There are no set-up fees and you can close your account at any time.</span><span class="sxs-lookup"><span data-stu-id="5fc33-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="5fc33-122">You can find more details at [Twilio Pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="5fc33-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <a id="Concepts"></a><span data-ttu-id="5fc33-123">Concepts</span><span class="sxs-lookup"><span data-stu-id="5fc33-123">Concepts</span></span>
<span data-ttu-id="5fc33-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span><span class="sxs-lookup"><span data-stu-id="5fc33-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="5fc33-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="5fc33-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="5fc33-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="5fc33-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <a id="Verbs"></a><span data-ttu-id="5fc33-127">Twilio Verbs</span><span class="sxs-lookup"><span data-stu-id="5fc33-127">Twilio Verbs</span></span>
<span data-ttu-id="5fc33-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span><span class="sxs-lookup"><span data-stu-id="5fc33-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="5fc33-129">The following is a list of Twilio verbs.</span><span class="sxs-lookup"><span data-stu-id="5fc33-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="5fc33-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="5fc33-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="5fc33-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span><span class="sxs-lookup"><span data-stu-id="5fc33-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="5fc33-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span><span class="sxs-lookup"><span data-stu-id="5fc33-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="5fc33-133">**&lt;Hangup&gt;**: Ends a call.</span><span class="sxs-lookup"><span data-stu-id="5fc33-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="5fc33-134">**&lt;Play&gt;**: Plays an audio file.</span><span class="sxs-lookup"><span data-stu-id="5fc33-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="5fc33-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span><span class="sxs-lookup"><span data-stu-id="5fc33-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="5fc33-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span><span class="sxs-lookup"><span data-stu-id="5fc33-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="5fc33-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span><span class="sxs-lookup"><span data-stu-id="5fc33-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="5fc33-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span><span class="sxs-lookup"><span data-stu-id="5fc33-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="5fc33-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span><span class="sxs-lookup"><span data-stu-id="5fc33-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="5fc33-140">**&lt;Sms&gt;**: Sends an SMS message.</span><span class="sxs-lookup"><span data-stu-id="5fc33-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <a id="TwiML"></a><span data-ttu-id="5fc33-141">TwiML</span><span class="sxs-lookup"><span data-stu-id="5fc33-141">TwiML</span></span>
<span data-ttu-id="5fc33-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span><span class="sxs-lookup"><span data-stu-id="5fc33-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="5fc33-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span><span class="sxs-lookup"><span data-stu-id="5fc33-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="5fc33-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span><span class="sxs-lookup"><span data-stu-id="5fc33-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="5fc33-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span><span class="sxs-lookup"><span data-stu-id="5fc33-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="5fc33-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span><span class="sxs-lookup"><span data-stu-id="5fc33-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="5fc33-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="5fc33-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="5fc33-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="5fc33-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <a id="CreateAccount"></a><span data-ttu-id="5fc33-149">Create a Twilio Account</span><span class="sxs-lookup"><span data-stu-id="5fc33-149">Create a Twilio Account</span></span>
<span data-ttu-id="5fc33-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="5fc33-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="5fc33-151">You can start with a free account, and upgrade your account later.</span><span class="sxs-lookup"><span data-stu-id="5fc33-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="5fc33-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span><span class="sxs-lookup"><span data-stu-id="5fc33-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="5fc33-153">Both will be needed to make Twilio API calls.</span><span class="sxs-lookup"><span data-stu-id="5fc33-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="5fc33-154">To prevent unauthorized access to your account, keep your authentication token secure.</span><span class="sxs-lookup"><span data-stu-id="5fc33-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="5fc33-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span><span class="sxs-lookup"><span data-stu-id="5fc33-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <a id="create_app"></a><span data-ttu-id="5fc33-156">Create a PHP Application</span><span class="sxs-lookup"><span data-stu-id="5fc33-156">Create a PHP Application</span></span>
<span data-ttu-id="5fc33-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span><span class="sxs-lookup"><span data-stu-id="5fc33-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span></span> <span data-ttu-id="5fc33-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="5fc33-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="5fc33-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="5fc33-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="5fc33-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="5fc33-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <a id="configure_app"></a><span data-ttu-id="5fc33-161">Configure Your Application to Use Twilio Libraries</span><span class="sxs-lookup"><span data-stu-id="5fc33-161">Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="5fc33-162">You can configure your application to use the Twilio library for PHP in two ways:</span><span class="sxs-lookup"><span data-stu-id="5fc33-162">You can configure your application to use the Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="5fc33-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span><span class="sxs-lookup"><span data-stu-id="5fc33-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span></span>
   
    <span data-ttu-id="5fc33-164">-OR-</span><span class="sxs-lookup"><span data-stu-id="5fc33-164">-OR-</span></span>
2. <span data-ttu-id="5fc33-165">Install the Twilio library for PHP as a PEAR package.</span><span class="sxs-lookup"><span data-stu-id="5fc33-165">Install the Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="5fc33-166">It can be installed with the following commands:</span><span class="sxs-lookup"><span data-stu-id="5fc33-166">It can be installed with the following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="5fc33-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span><span class="sxs-lookup"><span data-stu-id="5fc33-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="5fc33-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="5fc33-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <a id="howto_make_call"></a><span data-ttu-id="5fc33-169">How to: Make an outgoing call</span><span class="sxs-lookup"><span data-stu-id="5fc33-169">How to: Make an outgoing call</span></span>
<span data-ttu-id="5fc33-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span><span class="sxs-lookup"><span data-stu-id="5fc33-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span></span> <span data-ttu-id="5fc33-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span><span class="sxs-lookup"><span data-stu-id="5fc33-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="5fc33-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span><span class="sxs-lookup"><span data-stu-id="5fc33-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // The number of the phone initiating the the call.
    $from_number = "NNNNNNNNNNN";

    // The number of the phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use the Twilio-provided site for the TwiML response.
    $url = "http://twimlets.com/message";

    // The phone message text.
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make the call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

<span data-ttu-id="5fc33-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span><span class="sxs-lookup"><span data-stu-id="5fc33-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="5fc33-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="5fc33-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="5fc33-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="5fc33-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <a id="howto_send_sms"></a><span data-ttu-id="5fc33-176">How to: Send an SMS message</span><span class="sxs-lookup"><span data-stu-id="5fc33-176">How to: Send an SMS message</span></span>
<span data-ttu-id="5fc33-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span><span class="sxs-lookup"><span data-stu-id="5fc33-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span></span> <span data-ttu-id="5fc33-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span><span class="sxs-lookup"><span data-stu-id="5fc33-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="5fc33-179">The **To** number must be verified for your Twilio account prior to running the code.</span><span class="sxs-lookup"><span data-stu-id="5fc33-179">The **To** number must be verified for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send the SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a><span data-ttu-id="5fc33-180">How to: Provide TwiML Responses from your own Website</span><span class="sxs-lookup"><span data-stu-id="5fc33-180">How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="5fc33-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span><span class="sxs-lookup"><span data-stu-id="5fc33-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="5fc33-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="5fc33-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="5fc33-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span><span class="sxs-lookup"><span data-stu-id="5fc33-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span></span> <span data-ttu-id="5fc33-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span><span class="sxs-lookup"><span data-stu-id="5fc33-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="5fc33-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span><span class="sxs-lookup"><span data-stu-id="5fc33-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="5fc33-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span><span class="sxs-lookup"><span data-stu-id="5fc33-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span></span>

<span data-ttu-id="5fc33-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span><span class="sxs-lookup"><span data-stu-id="5fc33-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="5fc33-188">As you can see from the example above, the TwiML response is simply an XML document.</span><span class="sxs-lookup"><span data-stu-id="5fc33-188">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="5fc33-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span><span class="sxs-lookup"><span data-stu-id="5fc33-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="5fc33-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span><span class="sxs-lookup"><span data-stu-id="5fc33-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="5fc33-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="5fc33-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="5fc33-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span><span class="sxs-lookup"><span data-stu-id="5fc33-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="5fc33-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5fc33-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // The phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

<span data-ttu-id="5fc33-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="5fc33-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <a id="AdditionalServices"></a><span data-ttu-id="5fc33-195">How to: Use Additional Twilio Services</span><span class="sxs-lookup"><span data-stu-id="5fc33-195">How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="5fc33-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span><span class="sxs-lookup"><span data-stu-id="5fc33-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="5fc33-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="5fc33-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <a id="NextSteps"></a><span data-ttu-id="5fc33-198">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5fc33-198">Next Steps</span></span>
<span data-ttu-id="5fc33-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span><span class="sxs-lookup"><span data-stu-id="5fc33-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="5fc33-200">[Twilio Security Guidelines][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="5fc33-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="5fc33-201">[Twilio HowTo's and Example Code][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="5fc33-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="5fc33-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="5fc33-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="5fc33-203">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="5fc33-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="5fc33-204">[Talk to Twilio Support][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="5fc33-204">[Talk to Twilio Support][twilio_support]</span></span>

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
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
