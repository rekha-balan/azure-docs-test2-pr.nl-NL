---
title: How to Use Twilio for Voice and SMS (Java) | Microsoft Docs
description: Learn how to make a phone call and send a SMS message with the Twilio API service on Azure. Code samples written in Java.
services: ''
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 5a1b2ffa160a31b639605242b651dc8d14e7a01b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550187"
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="81875-104">How to Use Twilio for Voice and SMS Capabilities in Java</span><span class="sxs-lookup"><span data-stu-id="81875-104">How to Use Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="81875-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span><span class="sxs-lookup"><span data-stu-id="81875-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="81875-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span><span class="sxs-lookup"><span data-stu-id="81875-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="81875-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span><span class="sxs-lookup"><span data-stu-id="81875-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <a id="WhatIs"></a><span data-ttu-id="81875-108">What is Twilio?</span><span class="sxs-lookup"><span data-stu-id="81875-108">What is Twilio?</span></span>
<span data-ttu-id="81875-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span><span class="sxs-lookup"><span data-stu-id="81875-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="81875-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span><span class="sxs-lookup"><span data-stu-id="81875-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="81875-111">**Twilio Voice** allows your applications to make and receive phone calls.</span><span class="sxs-lookup"><span data-stu-id="81875-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="81875-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span><span class="sxs-lookup"><span data-stu-id="81875-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="81875-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span><span class="sxs-lookup"><span data-stu-id="81875-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <a id="Pricing"></a><span data-ttu-id="81875-114">Twilio Pricing and Special Offers</span><span class="sxs-lookup"><span data-stu-id="81875-114">Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="81875-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="81875-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="81875-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span><span class="sxs-lookup"><span data-stu-id="81875-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="81875-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="81875-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <a id="Concepts"></a><span data-ttu-id="81875-118">Concepts</span><span class="sxs-lookup"><span data-stu-id="81875-118">Concepts</span></span>
<span data-ttu-id="81875-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span><span class="sxs-lookup"><span data-stu-id="81875-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="81875-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="81875-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="81875-121">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="81875-121">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <a id="Verbs"></a><span data-ttu-id="81875-122">Twilio Verbs</span><span class="sxs-lookup"><span data-stu-id="81875-122">Twilio Verbs</span></span>
<span data-ttu-id="81875-123">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span><span class="sxs-lookup"><span data-stu-id="81875-123">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="81875-124">The following is a list of Twilio verbs.</span><span class="sxs-lookup"><span data-stu-id="81875-124">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="81875-125">**&lt;Dial&gt;**: Connects the caller to another phone.</span><span class="sxs-lookup"><span data-stu-id="81875-125">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="81875-126">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span><span class="sxs-lookup"><span data-stu-id="81875-126">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="81875-127">**&lt;Hangup&gt;**: Ends a call.</span><span class="sxs-lookup"><span data-stu-id="81875-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="81875-128">**&lt;Play&gt;**: Plays an audio file.</span><span class="sxs-lookup"><span data-stu-id="81875-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="81875-129">**&lt;Queue&gt;**: Add the to a queue of callers.</span><span class="sxs-lookup"><span data-stu-id="81875-129">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="81875-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span><span class="sxs-lookup"><span data-stu-id="81875-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="81875-131">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span><span class="sxs-lookup"><span data-stu-id="81875-131">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="81875-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span><span class="sxs-lookup"><span data-stu-id="81875-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="81875-133">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span><span class="sxs-lookup"><span data-stu-id="81875-133">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="81875-134">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span><span class="sxs-lookup"><span data-stu-id="81875-134">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="81875-135">**&lt;Sms&gt;**: Sends an SMS message.</span><span class="sxs-lookup"><span data-stu-id="81875-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <a id="TwiML"></a><span data-ttu-id="81875-136">TwiML</span><span class="sxs-lookup"><span data-stu-id="81875-136">TwiML</span></span>
<span data-ttu-id="81875-137">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span><span class="sxs-lookup"><span data-stu-id="81875-137">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="81875-138">As an example, the following TwiML would convert the text **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="81875-138">As an example, the following TwiML would convert the text **Hello World!**</span></span> <span data-ttu-id="81875-139">to speech.</span><span class="sxs-lookup"><span data-stu-id="81875-139">to speech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="81875-140">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span><span class="sxs-lookup"><span data-stu-id="81875-140">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="81875-141">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span><span class="sxs-lookup"><span data-stu-id="81875-141">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="81875-142">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span><span class="sxs-lookup"><span data-stu-id="81875-142">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="81875-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="81875-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="81875-144">For additional information about the Twilio API, see [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="81875-144">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <a id="CreateAccount"></a><span data-ttu-id="81875-145">Create a Twilio Account</span><span class="sxs-lookup"><span data-stu-id="81875-145">Create a Twilio Account</span></span>
<span data-ttu-id="81875-146">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="81875-146">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="81875-147">You can start with a free account, and upgrade your account later.</span><span class="sxs-lookup"><span data-stu-id="81875-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="81875-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span><span class="sxs-lookup"><span data-stu-id="81875-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="81875-149">Both will be needed to make Twilio API calls.</span><span class="sxs-lookup"><span data-stu-id="81875-149">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="81875-150">To prevent unauthorized access to your account, keep your authentication token secure.</span><span class="sxs-lookup"><span data-stu-id="81875-150">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="81875-151">Your account ID and authentication token are viewable at the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span><span class="sxs-lookup"><span data-stu-id="81875-151">Your account ID and authentication token are viewable at the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <a id="create_app"></a><span data-ttu-id="81875-152">Create a Java Application</span><span class="sxs-lookup"><span data-stu-id="81875-152">Create a Java Application</span></span>
1. <span data-ttu-id="81875-153">Obtain the Twilio JAR and add it to your Java build path and your WAR deployment assembly.</span><span class="sxs-lookup"><span data-stu-id="81875-153">Obtain the Twilio JAR and add it to your Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="81875-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span><span class="sxs-lookup"><span data-stu-id="81875-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="81875-155">Ensure your JDK's **cacerts** keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="81875-155">Ensure your JDK's **cacerts** keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="81875-156">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span><span class="sxs-lookup"><span data-stu-id="81875-156">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="81875-157">For information about ensuring your JDK's **cacerts** keystore contains the correct CA certificate, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="81875-157">For information about ensuring your JDK's **cacerts** keystore contains the correct CA certificate, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="81875-158">Detailed instructions for using the Twilio client library for Java are available at [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="81875-158">Detailed instructions for using the Twilio client library for Java are available at [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <a id="configure_app"></a><span data-ttu-id="81875-159">Configure Your Application to Use Twilio Libraries</span><span class="sxs-lookup"><span data-stu-id="81875-159">Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="81875-160">Within your code, you can add **import** statements at the top of your source files for the Twilio packages or classes you want to use in your application.</span><span class="sxs-lookup"><span data-stu-id="81875-160">Within your code, you can add **import** statements at the top of your source files for the Twilio packages or classes you want to use in your application.</span></span>

<span data-ttu-id="81875-161">For Java source files:</span><span class="sxs-lookup"><span data-stu-id="81875-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="81875-162">For Java Server Page (JSP) source files:</span><span class="sxs-lookup"><span data-stu-id="81875-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="81875-163">Depending on which Twilio packages or classes you want to use, your **import** statements may be different.</span><span class="sxs-lookup"><span data-stu-id="81875-163">Depending on which Twilio packages or classes you want to use, your **import** statements may be different.</span></span>

## <a id="howto_make_call"></a><span data-ttu-id="81875-164">How to: Make an outgoing call</span><span class="sxs-lookup"><span data-stu-id="81875-164">How to: Make an outgoing call</span></span>
<span data-ttu-id="81875-165">The following shows how to make an outgoing call using the **Call** class.</span><span class="sxs-lookup"><span data-stu-id="81875-165">The following shows how to make an outgoing call using the **Call** class.</span></span> <span data-ttu-id="81875-166">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span><span class="sxs-lookup"><span data-stu-id="81875-166">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="81875-167">Substitute your values for the **from** and **to** phone numbers, and ensure that you verify the **from** phone number for your Twilio account prior to running the code.</span><span class="sxs-lookup"><span data-stu-id="81875-167">Substitute your values for the **from** and **to** phone numbers, and ensure that you verify the **from** phone number for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare To and From numbers
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="81875-168">For more information about the parameters passed in to the **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="81875-168">For more information about the parameters passed in to the **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="81875-169">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span><span class="sxs-lookup"><span data-stu-id="81875-169">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="81875-170">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="81875-170">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <a id="howto_send_sms"></a><span data-ttu-id="81875-171">How to: Send an SMS message</span><span class="sxs-lookup"><span data-stu-id="81875-171">How to: Send an SMS message</span></span>
<span data-ttu-id="81875-172">The following shows how to send an SMS message using the **Message** class.</span><span class="sxs-lookup"><span data-stu-id="81875-172">The following shows how to send an SMS message using the **Message** class.</span></span> <span data-ttu-id="81875-173">The **from** number, **4155992671**, is provided by Twilio for trial accounts to send SMS messages.</span><span class="sxs-lookup"><span data-stu-id="81875-173">The **from** number, **4155992671**, is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="81875-174">The **to** number must be verified for your Twilio account prior to running the code.</span><span class="sxs-lookup"><span data-stu-id="81875-174">The **to** number must be verified for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare To and From numbers and the Body of the SMS message
    PhoneNumber to = new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, To and Body values
    // then send the SMS message by calling the create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="81875-175">For more information about the parameters passed in to the **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="81875-175">For more information about the parameters passed in to the **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <a id="howto_provide_twiml_responses"></a><span data-ttu-id="81875-176">How to: Provide TwiML Responses from your own Website</span><span class="sxs-lookup"><span data-stu-id="81875-176">How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="81875-177">When your application initiates a call to the Twilio API, for example via the **CallCreator.create** method, Twilio will send your request to a URL that is expected to return a TwiML response.</span><span class="sxs-lookup"><span data-stu-id="81875-177">When your application initiates a call to the Twilio API, for example via the **CallCreator.create** method, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="81875-178">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="81875-178">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="81875-179">(While TwiML is designed for use by Web services, you can view the TwiML in your browser.</span><span class="sxs-lookup"><span data-stu-id="81875-179">(While TwiML is designed for use by Web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="81875-180">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] to see a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span><span class="sxs-lookup"><span data-stu-id="81875-180">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] to see a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="81875-181">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span><span class="sxs-lookup"><span data-stu-id="81875-181">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="81875-182">You can create the site in any language that returns HTTP responses; this topic assumes you'll be hosting the URL in a JSP page.</span><span class="sxs-lookup"><span data-stu-id="81875-182">You can create the site in any language that returns HTTP responses; this topic assumes you'll be hosting the URL in a JSP page.</span></span>

<span data-ttu-id="81875-183">The following JSP page results in a TwiML response that says **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="81875-183">The following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="81875-184">on the call.</span><span class="sxs-lookup"><span data-stu-id="81875-184">on the call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="81875-185">The following JSP page results in a TwiML response that says some text, has several pauses, and says information about the Twilio API version and the Azure role name.</span><span class="sxs-lookup"><span data-stu-id="81875-185">The following JSP page results in a TwiML response that says some text, has several pauses, and says information about the Twilio API version and the Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>The Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>The Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="81875-186">The **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span><span class="sxs-lookup"><span data-stu-id="81875-186">The **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="81875-187">To see the available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span><span class="sxs-lookup"><span data-stu-id="81875-187">To see the available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="81875-188">The **RoleName** environment variable is available as part of an Azure deployment.</span><span class="sxs-lookup"><span data-stu-id="81875-188">The **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="81875-189">(If you want to add custom environment variables so they could be picked up from **System.getenv**, see the environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="81875-189">(If you want to add custom environment variables so they could be picked up from **System.getenv**, see the environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="81875-190">Once you have your JSP page set up to provide TwiML responses, use the URL of the JSP page as the URL passed into the **Call.creator** method.</span><span class="sxs-lookup"><span data-stu-id="81875-190">Once you have your JSP page set up to provide TwiML responses, use the URL of the JSP page as the URL passed into the **Call.creator** method.</span></span> <span data-ttu-id="81875-191">For example, if you have a Web application named MyTwiML deployed to an Azure hosted service, and the name of the JSP page is mytwiml.jsp, the URL can be passed to **Call.creator** as shown in the following:</span><span class="sxs-lookup"><span data-stu-id="81875-191">For example, if you have a Web application named MyTwiML deployed to an Azure hosted service, and the name of the JSP page is mytwiml.jsp, the URL can be passed to **Call.creator** as shown in the following:</span></span>

```java
    // Declare To and From numbers and the URL of your JSP page
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="81875-192">Another option for responding with TwiML is via the **VoiceResponse** class, which is available in the **com.twilio.twiml** package.</span><span class="sxs-lookup"><span data-stu-id="81875-192">Another option for responding with TwiML is via the **VoiceResponse** class, which is available in the **com.twilio.twiml** package.</span></span>

<span data-ttu-id="81875-193">For additional information about using Twilio in Azure with Java, see [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="81875-193">For additional information about using Twilio in Azure with Java, see [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <a id="AdditionalServices"></a><span data-ttu-id="81875-194">How to: Use Additional Twilio Services</span><span class="sxs-lookup"><span data-stu-id="81875-194">How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="81875-195">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span><span class="sxs-lookup"><span data-stu-id="81875-195">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="81875-196">For full details, see the [Twilio API documentation][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="81875-196">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <a id="NextSteps"></a><span data-ttu-id="81875-197">Next Steps</span><span class="sxs-lookup"><span data-stu-id="81875-197">Next Steps</span></span>
<span data-ttu-id="81875-198">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span><span class="sxs-lookup"><span data-stu-id="81875-198">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="81875-199">[Twilio Security Guidelines][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="81875-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="81875-200">[Twilio HowTo's and Example Code][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="81875-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="81875-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="81875-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="81875-202">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="81875-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="81875-203">[Talk to Twilio Support][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="81875-203">[Talk to Twilio Support][twilio_support]</span></span>

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
