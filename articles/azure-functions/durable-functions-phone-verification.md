---
title: Human interaction and timeouts in Durable Functions - Azure
description: Learn how to handle human interaction and timeouts in the Durable Functions extension for Azure Functions.
services: functions
author: kashimiz
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: azfuncdf
ms.openlocfilehash: 54c0c8e07ee4a248565b4d71562400c8f427fa77
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865469"
---
# <a name="human-interaction-in-durable-functions---phone-verification-sample"></a><span data-ttu-id="ad0d1-103">Human interaction in Durable Functions - Phone verification sample</span><span class="sxs-lookup"><span data-stu-id="ad0d1-103">Human interaction in Durable Functions - Phone verification sample</span></span>

<span data-ttu-id="ad0d1-104">This sample demonstrates how to build a [Durable Functions](durable-functions-overview.md) orchestration that involves human interaction.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-104">This sample demonstrates how to build a [Durable Functions](durable-functions-overview.md) orchestration that involves human interaction.</span></span> <span data-ttu-id="ad0d1-105">Whenever a real person is involved in an automated process, the process must be able to send notifications to the person and receive responses asynchronously.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-105">Whenever a real person is involved in an automated process, the process must be able to send notifications to the person and receive responses asynchronously.</span></span> <span data-ttu-id="ad0d1-106">It must also allow for the possibility that the person is unavailable.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-106">It must also allow for the possibility that the person is unavailable.</span></span> <span data-ttu-id="ad0d1-107">(This last part is where timeouts become important.)</span><span class="sxs-lookup"><span data-stu-id="ad0d1-107">(This last part is where timeouts become important.)</span></span>

<span data-ttu-id="ad0d1-108">This sample implements an SMS-based phone verification system.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-108">This sample implements an SMS-based phone verification system.</span></span> <span data-ttu-id="ad0d1-109">These types of flows are often used when verifying a customer's phone number or for multi-factor authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="ad0d1-109">These types of flows are often used when verifying a customer's phone number or for multi-factor authentication (MFA).</span></span> <span data-ttu-id="ad0d1-110">This is a powerful example because the entire implementation is done using a couple small functions.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-110">This is a powerful example because the entire implementation is done using a couple small functions.</span></span> <span data-ttu-id="ad0d1-111">No external data store, such as a database, is required.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-111">No external data store, such as a database, is required.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad0d1-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ad0d1-112">Prerequisites</span></span>

* <span data-ttu-id="ad0d1-113">[Install Durable Functions](durable-functions-install.md).</span><span class="sxs-lookup"><span data-stu-id="ad0d1-113">[Install Durable Functions](durable-functions-install.md).</span></span>
* <span data-ttu-id="ad0d1-114">Complete the [Hello Sequence](durable-functions-sequence.md) walkthrough.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-114">Complete the [Hello Sequence](durable-functions-sequence.md) walkthrough.</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="ad0d1-115">Scenario overview</span><span class="sxs-lookup"><span data-stu-id="ad0d1-115">Scenario overview</span></span>

<span data-ttu-id="ad0d1-116">Phone verification is used to verify that end users of your application are not spammers and that they are who they say they are.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-116">Phone verification is used to verify that end users of your application are not spammers and that they are who they say they are.</span></span> <span data-ttu-id="ad0d1-117">Multi-factor authentication is a common use case for protecting user accounts from hackers.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-117">Multi-factor authentication is a common use case for protecting user accounts from hackers.</span></span> <span data-ttu-id="ad0d1-118">The challenge with implementing your own phone verification is that it requires a **stateful interaction** with a human being.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-118">The challenge with implementing your own phone verification is that it requires a **stateful interaction** with a human being.</span></span> <span data-ttu-id="ad0d1-119">An end user is typically provided some code (for example, a 4-digit number) and must respond **in a reasonable amount of time**.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-119">An end user is typically provided some code (for example, a 4-digit number) and must respond **in a reasonable amount of time**.</span></span>

<span data-ttu-id="ad0d1-120">Ordinary Azure Functions are stateless (as are many other cloud endpoints on other platforms), so these types of interactions involve explicitly managing state externally in a database or some other persistent store.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-120">Ordinary Azure Functions are stateless (as are many other cloud endpoints on other platforms), so these types of interactions involve explicitly managing state externally in a database or some other persistent store.</span></span> <span data-ttu-id="ad0d1-121">In addition, the interaction must be broken up into multiple functions that can be coordinated together.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-121">In addition, the interaction must be broken up into multiple functions that can be coordinated together.</span></span> <span data-ttu-id="ad0d1-122">For example, you need at least one function for deciding on a code, persisting it somewhere, and sending it to the user's phone.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-122">For example, you need at least one function for deciding on a code, persisting it somewhere, and sending it to the user's phone.</span></span> <span data-ttu-id="ad0d1-123">Additionally, you need at least one other function to receive a response from the user and somehow map it back to the original function call in order to do the code validation.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-123">Additionally, you need at least one other function to receive a response from the user and somehow map it back to the original function call in order to do the code validation.</span></span> <span data-ttu-id="ad0d1-124">A timeout is also an important aspect to ensure security.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-124">A timeout is also an important aspect to ensure security.</span></span> <span data-ttu-id="ad0d1-125">This can get fairly complex quickly.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-125">This can get fairly complex quickly.</span></span>

<span data-ttu-id="ad0d1-126">The complexity of this scenario is greatly reduced when you use Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-126">The complexity of this scenario is greatly reduced when you use Durable Functions.</span></span> <span data-ttu-id="ad0d1-127">As you will see in this sample, an orchestrator function can manage the stateful interaction easily and without involving any external data stores.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-127">As you will see in this sample, an orchestrator function can manage the stateful interaction easily and without involving any external data stores.</span></span> <span data-ttu-id="ad0d1-128">Because orchestrator functions are *durable*, these interactive flows are also highly reliable.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-128">Because orchestrator functions are *durable*, these interactive flows are also highly reliable.</span></span>

## <a name="configuring-twilio-integration"></a><span data-ttu-id="ad0d1-129">Configuring Twilio integration</span><span class="sxs-lookup"><span data-stu-id="ad0d1-129">Configuring Twilio integration</span></span>

[!INCLUDE [functions-twilio-integration](../../includes/functions-twilio-integration.md)]

## <a name="the-functions"></a><span data-ttu-id="ad0d1-130">The functions</span><span class="sxs-lookup"><span data-stu-id="ad0d1-130">The functions</span></span>

<span data-ttu-id="ad0d1-131">This article walks through the following functions in the sample app:</span><span class="sxs-lookup"><span data-stu-id="ad0d1-131">This article walks through the following functions in the sample app:</span></span>

* <span data-ttu-id="ad0d1-132">**E4_SmsPhoneVerification**</span><span class="sxs-lookup"><span data-stu-id="ad0d1-132">**E4_SmsPhoneVerification**</span></span>
* <span data-ttu-id="ad0d1-133">**E4_SendSmsChallenge**</span><span class="sxs-lookup"><span data-stu-id="ad0d1-133">**E4_SendSmsChallenge**</span></span>

<span data-ttu-id="ad0d1-134">The following sections explain the configuration and code that are used for C# scripting and JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-134">The following sections explain the configuration and code that are used for C# scripting and JavaScript.</span></span> <span data-ttu-id="ad0d1-135">The code for Visual Studio development is shown at the end of the article.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-135">The code for Visual Studio development is shown at the end of the article.</span></span>
 
## <a name="the-sms-verification-orchestration-visual-studio-code-and-azure-portal-sample-code"></a><span data-ttu-id="ad0d1-136">The SMS verification orchestration (Visual Studio Code and Azure portal sample code)</span><span class="sxs-lookup"><span data-stu-id="ad0d1-136">The SMS verification orchestration (Visual Studio Code and Azure portal sample code)</span></span> 

<span data-ttu-id="ad0d1-137">The **E4_SmsPhoneVerification** function uses the standard *function.json* for orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-137">The **E4_SmsPhoneVerification** function uses the standard *function.json* for orchestrator functions.</span></span>

[!code-json[Main](~/samples-durable-functions/samples/csx/E4_SmsPhoneVerification/function.json)]

<span data-ttu-id="ad0d1-138">Here is the code that implements the function:</span><span class="sxs-lookup"><span data-stu-id="ad0d1-138">Here is the code that implements the function:</span></span>

### <a name="c"></a><span data-ttu-id="ad0d1-139">C#</span><span class="sxs-lookup"><span data-stu-id="ad0d1-139">C#</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E4_SmsPhoneVerification/run.csx)]

### <a name="javascript-functions-v2-only"></a><span data-ttu-id="ad0d1-140">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="ad0d1-140">JavaScript (Functions v2 only)</span></span>

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/E4_SmsPhoneVerification/index.js)]

<span data-ttu-id="ad0d1-141">Once started, this orchestrator function does the following:</span><span class="sxs-lookup"><span data-stu-id="ad0d1-141">Once started, this orchestrator function does the following:</span></span>

1. <span data-ttu-id="ad0d1-142">Gets a phone number to which it will *send* the SMS notification.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-142">Gets a phone number to which it will *send* the SMS notification.</span></span>
2. <span data-ttu-id="ad0d1-143">Calls **E4_SendSmsChallenge** to send an SMS message to the user and returns back the expected 4-digit challenge code.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-143">Calls **E4_SendSmsChallenge** to send an SMS message to the user and returns back the expected 4-digit challenge code.</span></span>
3. <span data-ttu-id="ad0d1-144">Creates a durable timer that triggers 90 seconds from the current time.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-144">Creates a durable timer that triggers 90 seconds from the current time.</span></span>
4. <span data-ttu-id="ad0d1-145">In parallel with the timer, waits for an **SmsChallengeResponse** event from the user.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-145">In parallel with the timer, waits for an **SmsChallengeResponse** event from the user.</span></span>

<span data-ttu-id="ad0d1-146">The user receives an SMS message with a four-digit code.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-146">The user receives an SMS message with a four-digit code.</span></span> <span data-ttu-id="ad0d1-147">They have 90 seconds to send that same 4-digit code back to the orchestrator function instance to complete the verification process.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-147">They have 90 seconds to send that same 4-digit code back to the orchestrator function instance to complete the verification process.</span></span> <span data-ttu-id="ad0d1-148">If they submit the wrong code, they get an additional three tries to get it right (within the same 90-second window).</span><span class="sxs-lookup"><span data-stu-id="ad0d1-148">If they submit the wrong code, they get an additional three tries to get it right (within the same 90-second window).</span></span>

> [!NOTE]
> <span data-ttu-id="ad0d1-149">It may not be obvious at first, but this orchestrator function is completely deterministic.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-149">It may not be obvious at first, but this orchestrator function is completely deterministic.</span></span> <span data-ttu-id="ad0d1-150">This is because the `CurrentUtcDateTime` property is used to calculate the timer expiration time, and this property returns the same value on every replay at this point in the orchestrator code.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-150">This is because the `CurrentUtcDateTime` property is used to calculate the timer expiration time, and this property returns the same value on every replay at this point in the orchestrator code.</span></span> <span data-ttu-id="ad0d1-151">This is important to ensure that the same `winner` results from every repeated call to `Task.WhenAny`.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-151">This is important to ensure that the same `winner` results from every repeated call to `Task.WhenAny`.</span></span>

> [!WARNING]
> <span data-ttu-id="ad0d1-152">It's important to [cancel timers](durable-functions-timers.md) if you no longer need them to expire, as in the example above when a challenge response is accepted.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-152">It's important to [cancel timers](durable-functions-timers.md) if you no longer need them to expire, as in the example above when a challenge response is accepted.</span></span>

## <a name="send-the-sms-message"></a><span data-ttu-id="ad0d1-153">Send the SMS message</span><span class="sxs-lookup"><span data-stu-id="ad0d1-153">Send the SMS message</span></span>

<span data-ttu-id="ad0d1-154">The **E4_SendSmsChallenge** function uses the Twilio binding to send the SMS message with the 4-digit code to the end user.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-154">The **E4_SendSmsChallenge** function uses the Twilio binding to send the SMS message with the 4-digit code to the end user.</span></span> <span data-ttu-id="ad0d1-155">The *function.json* is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="ad0d1-155">The *function.json* is defined as follows:</span></span>

[!code-json[Main](~/samples-durable-functions/samples/csx/E4_SendSmsChallenge/function.json)]

<span data-ttu-id="ad0d1-156">And here is the code that generates the 4-digit challenge code and sends the SMS message:</span><span class="sxs-lookup"><span data-stu-id="ad0d1-156">And here is the code that generates the 4-digit challenge code and sends the SMS message:</span></span>

### <a name="c"></a><span data-ttu-id="ad0d1-157">C#</span><span class="sxs-lookup"><span data-stu-id="ad0d1-157">C#</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E4_SendSmsChallenge/run.csx)]

### <a name="javascript-functions-v2-only"></a><span data-ttu-id="ad0d1-158">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="ad0d1-158">JavaScript (Functions v2 only)</span></span>

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/E4_SendSmsChallenge/index.js)]

<span data-ttu-id="ad0d1-159">This **E4_SendSmsChallenge** function only gets called once, even if the process crashes or gets replayed.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-159">This **E4_SendSmsChallenge** function only gets called once, even if the process crashes or gets replayed.</span></span> <span data-ttu-id="ad0d1-160">This is good because you don't want the end user getting multiple SMS messages.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-160">This is good because you don't want the end user getting multiple SMS messages.</span></span> <span data-ttu-id="ad0d1-161">The `challengeCode` return value is automatically persisted, so the orchestrator function always knows what the correct code is.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-161">The `challengeCode` return value is automatically persisted, so the orchestrator function always knows what the correct code is.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="ad0d1-162">Run the sample</span><span class="sxs-lookup"><span data-stu-id="ad0d1-162">Run the sample</span></span>

<span data-ttu-id="ad0d1-163">Using the HTTP-triggered functions included in the sample, you can start the orchestration by sending the following HTTP POST request:</span><span class="sxs-lookup"><span data-stu-id="ad0d1-163">Using the HTTP-triggered functions included in the sample, you can start the orchestration by sending the following HTTP POST request:</span></span>

```
POST http://{host}/orchestrators/E4_SmsPhoneVerification
Content-Length: 14
Content-Type: application/json

"+1425XXXXXXX"
```
```
HTTP/1.1 202 Accepted
Content-Length: 695
Content-Type: application/json; charset=utf-8
Location: http://{host}/admin/extensions/DurableTaskExtension/instances/741c65651d4c40cea29acdd5bb47baf1?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}

{"id":"741c65651d4c40cea29acdd5bb47baf1","statusQueryGetUri":"http://{host}/admin/extensions/DurableTaskExtension/instances/741c65651d4c40cea29acdd5bb47baf1?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}","sendEventPostUri":"http://{host}/admin/extensions/DurableTaskExtension/instances/741c65651d4c40cea29acdd5bb47baf1/raiseEvent/{eventName}?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}","terminatePostUri":"http://{host}/admin/extensions/DurableTaskExtension/instances/741c65651d4c40cea29acdd5bb47baf1/terminate?reason={text}&taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}"}
```

   > [!NOTE]
   > <span data-ttu-id="ad0d1-164">Currently, JavaScript orchestration starter functions cannot return instance management URIs.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-164">Currently, JavaScript orchestration starter functions cannot return instance management URIs.</span></span> <span data-ttu-id="ad0d1-165">This capability will be added in a later release.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-165">This capability will be added in a later release.</span></span>

<span data-ttu-id="ad0d1-166">The orchestrator function receives the supplied phone number and immediately sends it an SMS message with a randomly generated 4-digit verification code &mdash; for example, *2168*.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-166">The orchestrator function receives the supplied phone number and immediately sends it an SMS message with a randomly generated 4-digit verification code &mdash; for example, *2168*.</span></span> <span data-ttu-id="ad0d1-167">The function then waits 90 seconds for a response.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-167">The function then waits 90 seconds for a response.</span></span>

<span data-ttu-id="ad0d1-168">To reply with the code, you can use `RaiseEventAsync` inside another function or invoke the **sendEventUrl** HTTP POST webhook referenced in the 202 response above, replacing `{eventName}` with the name of the event, `SmsChallengeResponse`:</span><span class="sxs-lookup"><span data-stu-id="ad0d1-168">To reply with the code, you can use `RaiseEventAsync` inside another function or invoke the **sendEventUrl** HTTP POST webhook referenced in the 202 response above, replacing `{eventName}` with the name of the event, `SmsChallengeResponse`:</span></span>

```
POST http://{host}/admin/extensions/DurableTaskExtension/instances/741c65651d4c40cea29acdd5bb47baf1/raiseEvent/SmsChallengeResponse?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
Content-Length: 4
Content-Type: application/json

2168
```

<span data-ttu-id="ad0d1-169">If you send this before the timer expires, the orchestration completes and the `output` field is set to `true`, indicating a successful verification.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-169">If you send this before the timer expires, the orchestration completes and the `output` field is set to `true`, indicating a successful verification.</span></span>

```
GET http://{host}/admin/extensions/DurableTaskExtension/instances/741c65651d4c40cea29acdd5bb47baf1?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
```
```
HTTP/1.1 200 OK
Content-Length: 144
Content-Type: application/json; charset=utf-8

{"runtimeStatus":"Completed","input":"+1425XXXXXXX","output":true,"createdTime":"2017-06-29T19:10:49Z","lastUpdatedTime":"2017-06-29T19:12:23Z"}
```

<span data-ttu-id="ad0d1-170">If you let the timer expire, or if you enter the wrong code four times, you can query for the status and see a `false` orchestration function output, indicating that phone verification failed.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-170">If you let the timer expire, or if you enter the wrong code four times, you can query for the status and see a `false` orchestration function output, indicating that phone verification failed.</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 145

{"runtimeStatus":"Completed","input":"+1425XXXXXXX","output":false,"createdTime":"2017-06-29T19:20:49Z","lastUpdatedTime":"2017-06-29T19:22:23Z"}
```

## <a name="visual-studio-sample-code"></a><span data-ttu-id="ad0d1-171">Visual Studio sample code</span><span class="sxs-lookup"><span data-stu-id="ad0d1-171">Visual Studio sample code</span></span>

<span data-ttu-id="ad0d1-172">Here is the orchestration as a single C# file in a Visual Studio project:</span><span class="sxs-lookup"><span data-stu-id="ad0d1-172">Here is the orchestration as a single C# file in a Visual Studio project:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/PhoneVerification.cs)]

## <a name="next-steps"></a><span data-ttu-id="ad0d1-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad0d1-173">Next steps</span></span>

<span data-ttu-id="ad0d1-174">This sample has demonstrated some of the advanced capabilities of Durable Functions, notably `WaitForExternalEvent` and `CreateTimer`.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-174">This sample has demonstrated some of the advanced capabilities of Durable Functions, notably `WaitForExternalEvent` and `CreateTimer`.</span></span> <span data-ttu-id="ad0d1-175">You've seen how these can be combined with `Task.WaitAny` to implement a reliable timeout system, which is often useful for interacting with real people.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-175">You've seen how these can be combined with `Task.WaitAny` to implement a reliable timeout system, which is often useful for interacting with real people.</span></span> <span data-ttu-id="ad0d1-176">You can learn more about how to use Durable Functions by reading a series of articles that offer in-depth coverage of specific topics.</span><span class="sxs-lookup"><span data-stu-id="ad0d1-176">You can learn more about how to use Durable Functions by reading a series of articles that offer in-depth coverage of specific topics.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ad0d1-177">Go to the first article in the series</span><span class="sxs-lookup"><span data-stu-id="ad0d1-177">Go to the first article in the series</span></span>](durable-functions-bindings.md)
