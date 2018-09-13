---
title: Monitors in Durable Functions - Azure
description: Learn how to implement a status monitor using the Durable Functions extension for Azure Functions.
services: functions
author: kashimiz
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: azfuncdf
ms.openlocfilehash: f59fcecbb1f321c447e15469cf5584c5be8d7b96
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858081"
---
# <a name="monitor-scenario-in-durable-functions---weather-watcher-sample"></a><span data-ttu-id="9540e-103">Monitor scenario in Durable Functions - Weather watcher sample</span><span class="sxs-lookup"><span data-stu-id="9540e-103">Monitor scenario in Durable Functions - Weather watcher sample</span></span>

<span data-ttu-id="9540e-104">The monitor pattern refers to a flexible *recurring* process in a workflow - for example, polling until certain conditions are met.</span><span class="sxs-lookup"><span data-stu-id="9540e-104">The monitor pattern refers to a flexible *recurring* process in a workflow - for example, polling until certain conditions are met.</span></span> <span data-ttu-id="9540e-105">This article explains a sample that uses [Durable Functions](durable-functions-overview.md) to implement monitoring.</span><span class="sxs-lookup"><span data-stu-id="9540e-105">This article explains a sample that uses [Durable Functions](durable-functions-overview.md) to implement monitoring.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9540e-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9540e-106">Prerequisites</span></span>

* <span data-ttu-id="9540e-107">[Install Durable Functions](durable-functions-install.md).</span><span class="sxs-lookup"><span data-stu-id="9540e-107">[Install Durable Functions](durable-functions-install.md).</span></span>
* <span data-ttu-id="9540e-108">Complete the [Hello Sequence](durable-functions-sequence.md) walkthrough.</span><span class="sxs-lookup"><span data-stu-id="9540e-108">Complete the [Hello Sequence](durable-functions-sequence.md) walkthrough.</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="9540e-109">Scenario overview</span><span class="sxs-lookup"><span data-stu-id="9540e-109">Scenario overview</span></span>

<span data-ttu-id="9540e-110">This sample monitors a location's current weather conditions and alerts a user by SMS when the skies are clear.</span><span class="sxs-lookup"><span data-stu-id="9540e-110">This sample monitors a location's current weather conditions and alerts a user by SMS when the skies are clear.</span></span> <span data-ttu-id="9540e-111">You could use a regular timer-triggered function to check the weather and send alerts.</span><span class="sxs-lookup"><span data-stu-id="9540e-111">You could use a regular timer-triggered function to check the weather and send alerts.</span></span> <span data-ttu-id="9540e-112">However, one problem with this approach is **lifetime management**.</span><span class="sxs-lookup"><span data-stu-id="9540e-112">However, one problem with this approach is **lifetime management**.</span></span> <span data-ttu-id="9540e-113">If only one alert should be sent, the monitor needs to disable itself after clear weather is detected.</span><span class="sxs-lookup"><span data-stu-id="9540e-113">If only one alert should be sent, the monitor needs to disable itself after clear weather is detected.</span></span> <span data-ttu-id="9540e-114">The monitoring pattern can end its own execution, among other benefits:</span><span class="sxs-lookup"><span data-stu-id="9540e-114">The monitoring pattern can end its own execution, among other benefits:</span></span>

* <span data-ttu-id="9540e-115">Monitors run on intervals, not schedules: a timer trigger *runs* every hour; a monitor *waits* one hour between actions.</span><span class="sxs-lookup"><span data-stu-id="9540e-115">Monitors run on intervals, not schedules: a timer trigger *runs* every hour; a monitor *waits* one hour between actions.</span></span> <span data-ttu-id="9540e-116">A monitor's actions will not overlap unless specified, which can be important for long-running tasks.</span><span class="sxs-lookup"><span data-stu-id="9540e-116">A monitor's actions will not overlap unless specified, which can be important for long-running tasks.</span></span>
* <span data-ttu-id="9540e-117">Monitors can have dynamic intervals: the wait time can change based on some condition.</span><span class="sxs-lookup"><span data-stu-id="9540e-117">Monitors can have dynamic intervals: the wait time can change based on some condition.</span></span>
* <span data-ttu-id="9540e-118">Monitors can terminate when some condition is met or be terminated by another process.</span><span class="sxs-lookup"><span data-stu-id="9540e-118">Monitors can terminate when some condition is met or be terminated by another process.</span></span>
* <span data-ttu-id="9540e-119">Monitors can take parameters.</span><span class="sxs-lookup"><span data-stu-id="9540e-119">Monitors can take parameters.</span></span> <span data-ttu-id="9540e-120">The sample shows how the same weather-monitoring process can be applied to any requested location and phone number.</span><span class="sxs-lookup"><span data-stu-id="9540e-120">The sample shows how the same weather-monitoring process can be applied to any requested location and phone number.</span></span>
* <span data-ttu-id="9540e-121">Monitors are scalable.</span><span class="sxs-lookup"><span data-stu-id="9540e-121">Monitors are scalable.</span></span> <span data-ttu-id="9540e-122">Because each monitor is an orchestration instance, multiple monitors can be created without having to create new functions or define more code.</span><span class="sxs-lookup"><span data-stu-id="9540e-122">Because each monitor is an orchestration instance, multiple monitors can be created without having to create new functions or define more code.</span></span>
* <span data-ttu-id="9540e-123">Monitors integrate easily into larger workflows.</span><span class="sxs-lookup"><span data-stu-id="9540e-123">Monitors integrate easily into larger workflows.</span></span> <span data-ttu-id="9540e-124">A monitor can be one section of a more complex orchestration function, or a [sub-orchestration](https://docs.microsoft.com/azure/azure-functions/durable-functions-sub-orchestrations).</span><span class="sxs-lookup"><span data-stu-id="9540e-124">A monitor can be one section of a more complex orchestration function, or a [sub-orchestration](https://docs.microsoft.com/azure/azure-functions/durable-functions-sub-orchestrations).</span></span>

## <a name="configuring-twilio-integration"></a><span data-ttu-id="9540e-125">Configuring Twilio integration</span><span class="sxs-lookup"><span data-stu-id="9540e-125">Configuring Twilio integration</span></span>

[!INCLUDE [functions-twilio-integration](../../includes/functions-twilio-integration.md)]

## <a name="configuring-weather-underground-integration"></a><span data-ttu-id="9540e-126">Configuring Weather Underground integration</span><span class="sxs-lookup"><span data-stu-id="9540e-126">Configuring Weather Underground integration</span></span>

<span data-ttu-id="9540e-127">This sample involves using the Weather Underground API to check current weather conditions for a location.</span><span class="sxs-lookup"><span data-stu-id="9540e-127">This sample involves using the Weather Underground API to check current weather conditions for a location.</span></span>

<span data-ttu-id="9540e-128">The first thing you need is a Weather Underground account.</span><span class="sxs-lookup"><span data-stu-id="9540e-128">The first thing you need is a Weather Underground account.</span></span> <span data-ttu-id="9540e-129">You can create one for free at [https://www.wunderground.com/signup](https://www.wunderground.com/signup).</span><span class="sxs-lookup"><span data-stu-id="9540e-129">You can create one for free at [https://www.wunderground.com/signup](https://www.wunderground.com/signup).</span></span> <span data-ttu-id="9540e-130">Once you have an account, you will need to acquire an API key.</span><span class="sxs-lookup"><span data-stu-id="9540e-130">Once you have an account, you will need to acquire an API key.</span></span> <span data-ttu-id="9540e-131">You can do so by visiting [https://www.wunderground.com/weather/api](https://www.wunderground.com/weather/api), then selecting Key Settings.</span><span class="sxs-lookup"><span data-stu-id="9540e-131">You can do so by visiting [https://www.wunderground.com/weather/api](https://www.wunderground.com/weather/api), then selecting Key Settings.</span></span> <span data-ttu-id="9540e-132">The Stratus Developer plan is free and sufficient to run this sample.</span><span class="sxs-lookup"><span data-stu-id="9540e-132">The Stratus Developer plan is free and sufficient to run this sample.</span></span>

<span data-ttu-id="9540e-133">Once you have an API key, add the following **app setting** to your function app.</span><span class="sxs-lookup"><span data-stu-id="9540e-133">Once you have an API key, add the following **app setting** to your function app.</span></span>

| <span data-ttu-id="9540e-134">App setting name</span><span class="sxs-lookup"><span data-stu-id="9540e-134">App setting name</span></span> | <span data-ttu-id="9540e-135">Value description</span><span class="sxs-lookup"><span data-stu-id="9540e-135">Value description</span></span> |
| - | - |
| <span data-ttu-id="9540e-136">**WeatherUndergroundApiKey**</span><span class="sxs-lookup"><span data-stu-id="9540e-136">**WeatherUndergroundApiKey**</span></span>  | <span data-ttu-id="9540e-137">Your Weather Underground API key.</span><span class="sxs-lookup"><span data-stu-id="9540e-137">Your Weather Underground API key.</span></span> |

## <a name="the-functions"></a><span data-ttu-id="9540e-138">The functions</span><span class="sxs-lookup"><span data-stu-id="9540e-138">The functions</span></span>

<span data-ttu-id="9540e-139">This article explains the following functions in the sample app:</span><span class="sxs-lookup"><span data-stu-id="9540e-139">This article explains the following functions in the sample app:</span></span>

* <span data-ttu-id="9540e-140">`E3_Monitor`: An orchestrator function that calls `E3_GetIsClear` periodically.</span><span class="sxs-lookup"><span data-stu-id="9540e-140">`E3_Monitor`: An orchestrator function that calls `E3_GetIsClear` periodically.</span></span> <span data-ttu-id="9540e-141">It calls `E3_SendGoodWeatherAlert` if `E3_GetIsClear` returns true.</span><span class="sxs-lookup"><span data-stu-id="9540e-141">It calls `E3_SendGoodWeatherAlert` if `E3_GetIsClear` returns true.</span></span>
* <span data-ttu-id="9540e-142">`E3_GetIsClear`: An activity function that checks the current weather conditions for a location.</span><span class="sxs-lookup"><span data-stu-id="9540e-142">`E3_GetIsClear`: An activity function that checks the current weather conditions for a location.</span></span>
* <span data-ttu-id="9540e-143">`E3_SendGoodWeatherAlert`: An activity function that sends an SMS message via Twilio.</span><span class="sxs-lookup"><span data-stu-id="9540e-143">`E3_SendGoodWeatherAlert`: An activity function that sends an SMS message via Twilio.</span></span>

<span data-ttu-id="9540e-144">The following sections explain the configuration and code that are used for C# scripting and JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9540e-144">The following sections explain the configuration and code that are used for C# scripting and JavaScript.</span></span> <span data-ttu-id="9540e-145">The code for Visual Studio development is shown at the end of the article.</span><span class="sxs-lookup"><span data-stu-id="9540e-145">The code for Visual Studio development is shown at the end of the article.</span></span>
 
## <a name="the-weather-monitoring-orchestration-visual-studio-code-and-azure-portal-sample-code"></a><span data-ttu-id="9540e-146">The weather monitoring orchestration (Visual Studio Code and Azure portal sample code)</span><span class="sxs-lookup"><span data-stu-id="9540e-146">The weather monitoring orchestration (Visual Studio Code and Azure portal sample code)</span></span>

<span data-ttu-id="9540e-147">The **E3_Monitor** function uses the standard *function.json* for orchestrator functions.</span><span class="sxs-lookup"><span data-stu-id="9540e-147">The **E3_Monitor** function uses the standard *function.json* for orchestrator functions.</span></span>

[!code-json[Main](~/samples-durable-functions/samples/csx/E3_Monitor/function.json)]

<span data-ttu-id="9540e-148">Here is the code that implements the function:</span><span class="sxs-lookup"><span data-stu-id="9540e-148">Here is the code that implements the function:</span></span>

### <a name="c"></a><span data-ttu-id="9540e-149">C#</span><span class="sxs-lookup"><span data-stu-id="9540e-149">C#</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E3_Monitor/run.csx)]

### <a name="javascript-functions-v2-only"></a><span data-ttu-id="9540e-150">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="9540e-150">JavaScript (Functions v2 only)</span></span>

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/E3_Monitor/index.js)]

<span data-ttu-id="9540e-151">This orchestrator function performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="9540e-151">This orchestrator function performs the following actions:</span></span>

1. <span data-ttu-id="9540e-152">Gets the **MonitorRequest** consisting of the *location* to monitor and the *phone number* to which it will send an SMS notification.</span><span class="sxs-lookup"><span data-stu-id="9540e-152">Gets the **MonitorRequest** consisting of the *location* to monitor and the *phone number* to which it will send an SMS notification.</span></span>
2. <span data-ttu-id="9540e-153">Determines the expiration time of the monitor.</span><span class="sxs-lookup"><span data-stu-id="9540e-153">Determines the expiration time of the monitor.</span></span> <span data-ttu-id="9540e-154">The sample uses a hard-coded value for brevity.</span><span class="sxs-lookup"><span data-stu-id="9540e-154">The sample uses a hard-coded value for brevity.</span></span>
3. <span data-ttu-id="9540e-155">Calls **E3_GetIsClear** to determine whether there are clear skies at the requested location.</span><span class="sxs-lookup"><span data-stu-id="9540e-155">Calls **E3_GetIsClear** to determine whether there are clear skies at the requested location.</span></span>
4. <span data-ttu-id="9540e-156">If the weather is clear, calls **E3_SendGoodWeatherAlert** to send an SMS notification to the requested phone number.</span><span class="sxs-lookup"><span data-stu-id="9540e-156">If the weather is clear, calls **E3_SendGoodWeatherAlert** to send an SMS notification to the requested phone number.</span></span>
5. <span data-ttu-id="9540e-157">Creates a durable timer to resume the orchestration at the next polling interval.</span><span class="sxs-lookup"><span data-stu-id="9540e-157">Creates a durable timer to resume the orchestration at the next polling interval.</span></span> <span data-ttu-id="9540e-158">The sample uses a hard-coded value for brevity.</span><span class="sxs-lookup"><span data-stu-id="9540e-158">The sample uses a hard-coded value for brevity.</span></span>
6. <span data-ttu-id="9540e-159">Continues running until the [CurrentUtcDateTime](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CurrentUtcDateTime) passes the monitor's expiration time, or an SMS alert is sent.</span><span class="sxs-lookup"><span data-stu-id="9540e-159">Continues running until the [CurrentUtcDateTime](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CurrentUtcDateTime) passes the monitor's expiration time, or an SMS alert is sent.</span></span>

<span data-ttu-id="9540e-160">Multiple orchestrator instances can run simultaneously by sending multiple **MonitorRequests**.</span><span class="sxs-lookup"><span data-stu-id="9540e-160">Multiple orchestrator instances can run simultaneously by sending multiple **MonitorRequests**.</span></span> <span data-ttu-id="9540e-161">The location to monitor and the phone number to send an SMS alert to can be specified.</span><span class="sxs-lookup"><span data-stu-id="9540e-161">The location to monitor and the phone number to send an SMS alert to can be specified.</span></span>

## <a name="strongly-typed-data-transfer-net-only"></a><span data-ttu-id="9540e-162">Strongly-typed data transfer (.NET only)</span><span class="sxs-lookup"><span data-stu-id="9540e-162">Strongly-typed data transfer (.NET only)</span></span>

<span data-ttu-id="9540e-163">The orchestrator requires multiple pieces of data, so [shared POCO objects](functions-reference-csharp.md#reusing-csx-code) are used for strongly-typed data transfer in C# and C# script: [!code-csharp[Main](~/samples-durable-functions/samples/csx/shared/MonitorRequest.csx)]</span><span class="sxs-lookup"><span data-stu-id="9540e-163">The orchestrator requires multiple pieces of data, so [shared POCO objects](functions-reference-csharp.md#reusing-csx-code) are used for strongly-typed data transfer in C# and C# script: [!code-csharp[Main](~/samples-durable-functions/samples/csx/shared/MonitorRequest.csx)]</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/shared/Location.csx)]

<span data-ttu-id="9540e-164">The JavaScript sample uses regular JSON objects as parameters.</span><span class="sxs-lookup"><span data-stu-id="9540e-164">The JavaScript sample uses regular JSON objects as parameters.</span></span>

## <a name="helper-activity-functions"></a><span data-ttu-id="9540e-165">Helper activity functions</span><span class="sxs-lookup"><span data-stu-id="9540e-165">Helper activity functions</span></span>

<span data-ttu-id="9540e-166">As with other samples, the helper activity functions are regular functions that use the `activityTrigger` trigger binding.</span><span class="sxs-lookup"><span data-stu-id="9540e-166">As with other samples, the helper activity functions are regular functions that use the `activityTrigger` trigger binding.</span></span> <span data-ttu-id="9540e-167">The **E3_GetIsClear** function gets the current weather conditions using the Weather Underground API and determines whether the sky is clear.</span><span class="sxs-lookup"><span data-stu-id="9540e-167">The **E3_GetIsClear** function gets the current weather conditions using the Weather Underground API and determines whether the sky is clear.</span></span> <span data-ttu-id="9540e-168">The *function.json* is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="9540e-168">The *function.json* is defined as follows:</span></span>

[!code-json[Main](~/samples-durable-functions/samples/csx/E3_GetIsClear/function.json)]

<span data-ttu-id="9540e-169">And here is the implementation.</span><span class="sxs-lookup"><span data-stu-id="9540e-169">And here is the implementation.</span></span> <span data-ttu-id="9540e-170">Like the POCOs used for data transfer, logic to handle the API call and parse the response JSON is abstracted into a shared class in C#.</span><span class="sxs-lookup"><span data-stu-id="9540e-170">Like the POCOs used for data transfer, logic to handle the API call and parse the response JSON is abstracted into a shared class in C#.</span></span> <span data-ttu-id="9540e-171">You can find it as part of the [Visual Studio sample code](#run-the-sample).</span><span class="sxs-lookup"><span data-stu-id="9540e-171">You can find it as part of the [Visual Studio sample code](#run-the-sample).</span></span>

### <a name="c"></a><span data-ttu-id="9540e-172">C#</span><span class="sxs-lookup"><span data-stu-id="9540e-172">C#</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E3_GetIsClear/run.csx)]

### <a name="javascript-functions-v2-only"></a><span data-ttu-id="9540e-173">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="9540e-173">JavaScript (Functions v2 only)</span></span>

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/E3_GetIsClear/index.js)]

<span data-ttu-id="9540e-174">The **E3_SendGoodWeatherAlert** function uses the Twilio binding to send an SMS message notifying the end user that it's a good time for a walk.</span><span class="sxs-lookup"><span data-stu-id="9540e-174">The **E3_SendGoodWeatherAlert** function uses the Twilio binding to send an SMS message notifying the end user that it's a good time for a walk.</span></span> <span data-ttu-id="9540e-175">Its *function.json* is simple:</span><span class="sxs-lookup"><span data-stu-id="9540e-175">Its *function.json* is simple:</span></span>

[!code-json[Main](~/samples-durable-functions/samples/csx/E3_SendGoodWeatherAlert/function.json)]

<span data-ttu-id="9540e-176">And here is the code that sends the SMS message:</span><span class="sxs-lookup"><span data-stu-id="9540e-176">And here is the code that sends the SMS message:</span></span>

### <a name="c"></a><span data-ttu-id="9540e-177">C#</span><span class="sxs-lookup"><span data-stu-id="9540e-177">C#</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E3_SendGoodWeatherAlert/run.csx)]

### <a name="javascript-functions-v2-only"></a><span data-ttu-id="9540e-178">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="9540e-178">JavaScript (Functions v2 only)</span></span>

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/E3_SendGoodWeatherAlert/index.js)]

## <a name="run-the-sample"></a><span data-ttu-id="9540e-179">Run the sample</span><span class="sxs-lookup"><span data-stu-id="9540e-179">Run the sample</span></span>

<span data-ttu-id="9540e-180">Using the HTTP-triggered functions included in the sample, you can start the orchestration by sending the following HTTP POST request:</span><span class="sxs-lookup"><span data-stu-id="9540e-180">Using the HTTP-triggered functions included in the sample, you can start the orchestration by sending the following HTTP POST request:</span></span>

```
POST https://{host}/orchestrators/E3_Monitor
Content-Length: 77
Content-Type: application/json

{ "Location": { "City": "Redmond", "State": "WA" }, "Phone": "+1425XXXXXXX" }
```
```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://{host}/admin/extensions/DurableTaskExtension/instances/f6893f25acf64df2ab53a35c09d52635?taskHub=SampleHubVS&connection=Storage&code={SystemKey}
RetryAfter: 10

{"id": "f6893f25acf64df2ab53a35c09d52635", "statusQueryGetUri": "https://{host}/admin/extensions/DurableTaskExtension/instances/f6893f25acf64df2ab53a35c09d52635?taskHub=SampleHubVS&connection=Storage&code={systemKey}", "sendEventPostUri": "https://{host}/admin/extensions/DurableTaskExtension/instances/f6893f25acf64df2ab53a35c09d52635/raiseEvent/{eventName}?taskHub=SampleHubVS&connection=Storage&code={systemKey}", "terminatePostUri": "https://{host}/admin/extensions/DurableTaskExtension/instances/f6893f25acf64df2ab53a35c09d52635/terminate?reason={text}&taskHub=SampleHubVS&connection=Storage&code={systemKey}"}
```

   > [!NOTE]
   > <span data-ttu-id="9540e-181">Currently, JavaScript orchestration starter functions cannot return instance management URIs.</span><span class="sxs-lookup"><span data-stu-id="9540e-181">Currently, JavaScript orchestration starter functions cannot return instance management URIs.</span></span> <span data-ttu-id="9540e-182">This capability will be added in a later release.</span><span class="sxs-lookup"><span data-stu-id="9540e-182">This capability will be added in a later release.</span></span>

<span data-ttu-id="9540e-183">The **E3_Monitor** instance starts and queries the current weather conditions for the requested location.</span><span class="sxs-lookup"><span data-stu-id="9540e-183">The **E3_Monitor** instance starts and queries the current weather conditions for the requested location.</span></span> <span data-ttu-id="9540e-184">If the weather is clear, it calls an activity function to send an alert; otherwise, it sets a timer.</span><span class="sxs-lookup"><span data-stu-id="9540e-184">If the weather is clear, it calls an activity function to send an alert; otherwise, it sets a timer.</span></span> <span data-ttu-id="9540e-185">When the timer expires, the orchestration will resume.</span><span class="sxs-lookup"><span data-stu-id="9540e-185">When the timer expires, the orchestration will resume.</span></span>

<span data-ttu-id="9540e-186">You can see the orchestration's activity by looking at the function logs in the Azure Functions portal.</span><span class="sxs-lookup"><span data-stu-id="9540e-186">You can see the orchestration's activity by looking at the function logs in the Azure Functions portal.</span></span>

```
2018-03-01T01:14:41.649 Function started (Id=2d5fcadf-275b-4226-a174-f9f943c90cd1)
2018-03-01T01:14:42.741 Started orchestration with ID = '1608200bb2ce4b7face5fc3b8e674f2e'.
2018-03-01T01:14:42.780 Function completed (Success, Id=2d5fcadf-275b-4226-a174-f9f943c90cd1, Duration=1111ms)
2018-03-01T01:14:52.765 Function started (Id=b1b7eb4a-96d3-4f11-a0ff-893e08dd4cfb)
2018-03-01T01:14:52.890 Received monitor request. Location: Redmond, WA. Phone: +1425XXXXXXX.
2018-03-01T01:14:52.895 Instantiating monitor for Redmond, WA. Expires: 3/1/2018 7:14:52 AM.
2018-03-01T01:14:52.909 Checking current weather conditions for Redmond, WA at 3/1/2018 1:14:52 AM.
2018-03-01T01:14:52.954 Function completed (Success, Id=b1b7eb4a-96d3-4f11-a0ff-893e08dd4cfb, Duration=189ms)
2018-03-01T01:14:53.226 Function started (Id=80a4cb26-c4be-46ba-85c8-ea0c6d07d859)
2018-03-01T01:14:53.808 Function completed (Success, Id=80a4cb26-c4be-46ba-85c8-ea0c6d07d859, Duration=582ms)
2018-03-01T01:14:53.967 Function started (Id=561d0c78-ee6e-46cb-b6db-39ef639c9a2c)
2018-03-01T01:14:53.996 Next check for Redmond, WA at 3/1/2018 1:44:53 AM.
2018-03-01T01:14:54.030 Function completed (Success, Id=561d0c78-ee6e-46cb-b6db-39ef639c9a2c, Duration=62ms)
```

<span data-ttu-id="9540e-187">The orchestration will [terminate](durable-functions-instance-management.md#terminating-instances) once its timeout is reached or clear skies are detected.</span><span class="sxs-lookup"><span data-stu-id="9540e-187">The orchestration will [terminate](durable-functions-instance-management.md#terminating-instances) once its timeout is reached or clear skies are detected.</span></span> <span data-ttu-id="9540e-188">You can also use `TerminateAsync` inside another function or invoke the **terminatePostUri** HTTP POST webhook referenced in the 202 response above, replacing `{text}` with the reason for termination:</span><span class="sxs-lookup"><span data-stu-id="9540e-188">You can also use `TerminateAsync` inside another function or invoke the **terminatePostUri** HTTP POST webhook referenced in the 202 response above, replacing `{text}` with the reason for termination:</span></span>

```
POST https://{host}/admin/extensions/DurableTaskExtension/instances/f6893f25acf64df2ab53a35c09d52635/terminate?reason=Because&taskHub=SampleHubVS&connection=Storage&code={systemKey}
```

## <a name="visual-studio-sample-code"></a><span data-ttu-id="9540e-189">Visual Studio sample code</span><span class="sxs-lookup"><span data-stu-id="9540e-189">Visual Studio sample code</span></span>

<span data-ttu-id="9540e-190">Here is the orchestration as a single C# file in a Visual Studio project:</span><span class="sxs-lookup"><span data-stu-id="9540e-190">Here is the orchestration as a single C# file in a Visual Studio project:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/Monitor.cs)]

## <a name="next-steps"></a><span data-ttu-id="9540e-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="9540e-191">Next steps</span></span>

<span data-ttu-id="9540e-192">This sample has demonstrated how to use Durable Functions to monitor an external source's status using [durable timers](durable-functions-timers.md) and conditional logic.</span><span class="sxs-lookup"><span data-stu-id="9540e-192">This sample has demonstrated how to use Durable Functions to monitor an external source's status using [durable timers](durable-functions-timers.md) and conditional logic.</span></span> <span data-ttu-id="9540e-193">The next sample shows how to use external events and [durable timers](durable-functions-timers.md) to handle human interaction.</span><span class="sxs-lookup"><span data-stu-id="9540e-193">The next sample shows how to use external events and [durable timers](durable-functions-timers.md) to handle human interaction.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9540e-194">Run the human interaction sample</span><span class="sxs-lookup"><span data-stu-id="9540e-194">Run the human interaction sample</span></span>](durable-functions-phone-verification.md)
