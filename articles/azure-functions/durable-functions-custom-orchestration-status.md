---
title: Custom orchestration status in Durable Functions - Azure
description: Learn how to configure and use custom orchestration status for Durable Functions.
services: functions
author: kadimitr
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: azfuncdf
ms.openlocfilehash: c8eb2be6836e11ddbaed81970024ea7200ea819d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855768"
---
# <a name="custom-orchestration-status-in-durable-functions-azure-functions"></a><span data-ttu-id="ada01-103">Custom orchestration status in Durable Functions (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="ada01-103">Custom orchestration status in Durable Functions (Azure Functions)</span></span>

<span data-ttu-id="ada01-104">Custom orchestration status lets you set a custom status value for your orchestrator function.</span><span class="sxs-lookup"><span data-stu-id="ada01-104">Custom orchestration status lets you set a custom status value for your orchestrator function.</span></span> <span data-ttu-id="ada01-105">This status is provided via the HTTP GetStatus API or the `DurableOrchestrationClient.GetStatusAsync` API.</span><span class="sxs-lookup"><span data-stu-id="ada01-105">This status is provided via the HTTP GetStatus API or the `DurableOrchestrationClient.GetStatusAsync` API.</span></span>

## <a name="sample-use-cases"></a><span data-ttu-id="ada01-106">Sample use cases</span><span class="sxs-lookup"><span data-stu-id="ada01-106">Sample use cases</span></span> 

### <a name="visualize-progress"></a><span data-ttu-id="ada01-107">Visualize progress</span><span class="sxs-lookup"><span data-stu-id="ada01-107">Visualize progress</span></span>

<span data-ttu-id="ada01-108">Clients can poll the status end point and display a progress UI that visualizes the current execution stage.</span><span class="sxs-lookup"><span data-stu-id="ada01-108">Clients can poll the status end point and display a progress UI that visualizes the current execution stage.</span></span> <span data-ttu-id="ada01-109">The following sample demonstrates progress sharing:</span><span class="sxs-lookup"><span data-stu-id="ada01-109">The following sample demonstrates progress sharing:</span></span>

```csharp
[FunctionName("E1_HelloSequence")]
public static async Task<List<string>> Run(
  [OrchestrationTrigger] DurableOrchestrationContextBase context)
{
  var outputs = new List<string>();

  outputs.Add(await context.CallActivityAsync<string>("E1_SayHello", "Tokyo"));
  context.SetCustomStatus("Tokyo");
  outputs.Add(await context.CallActivityAsync<string>("E1_SayHello", "Seattle"));
  context.SetCustomStatus("Seattle");
  outputs.Add(await context.CallActivityAsync<string>("E1_SayHello", "London"));
  context.SetCustomStatus("London");

  // returns ["Hello Tokyo!", "Hello Seattle!", "Hello London!"]
  return outputs;
}

[FunctionName("E1_SayHello")]
public static string SayHello([ActivityTrigger] string name)
{
  return $"Hello {name}!";
}
```

<span data-ttu-id="ada01-110">And then the client will receive the output of the orchestration only when `CustomStatus` field is set to "London":</span><span class="sxs-lookup"><span data-stu-id="ada01-110">And then the client will receive the output of the orchestration only when `CustomStatus` field is set to "London":</span></span>

```csharp
[FunctionName("HttpStart")]
public static async Task<HttpResponseMessage> Run(
  [HttpTrigger(AuthorizationLevel.Function, methods: "post", Route = "orchestrators/{functionName}")] HttpRequestMessage req,
  [OrchestrationClient] DurableOrchestrationClientBase starter,
  string functionName,
  ILogger log)
{
    // Function input comes from the request content.
    dynamic eventData = await req.Content.ReadAsAsync<object>();
    string instanceId = await starter.StartNewAsync(functionName, eventData);

    log.LogInformation($"Started orchestration with ID = '{instanceId}'.");

    DurableOrchestrationStatus durableOrchestrationStatus = await starter.GetStatusAsync(instanceId);
    while (durableOrchestrationStatus.CustomStatus.ToString() != "London")
    {
      await Task.Delay(200);
      durableOrchestrationStatus = await starter.GetStatusAsync(instanceId);
    }

    HttpResponseMessage httpResponseMessage = new HttpResponseMessage(HttpStatusCode.OK)
    {
      Content = new StringContent(JsonConvert.SerializeObject(durableOrchestrationStatus))
    };

    return httpResponseMessage;
  }
}
```

### <a name="output-customization"></a><span data-ttu-id="ada01-111">Output customization</span><span class="sxs-lookup"><span data-stu-id="ada01-111">Output customization</span></span> 

<span data-ttu-id="ada01-112">Another interesting scenario is segmenting users by returning customized output based on unique characteristics or interactions.</span><span class="sxs-lookup"><span data-stu-id="ada01-112">Another interesting scenario is segmenting users by returning customized output based on unique characteristics or interactions.</span></span> <span data-ttu-id="ada01-113">With the help of custom orchestration status, the client-side code will stay generic.</span><span class="sxs-lookup"><span data-stu-id="ada01-113">With the help of custom orchestration status, the client-side code will stay generic.</span></span> <span data-ttu-id="ada01-114">All main modifications will happen on the server side as shown in the following sample:</span><span class="sxs-lookup"><span data-stu-id="ada01-114">All main modifications will happen on the server side as shown in the following sample:</span></span>

```csharp
[FunctionName("CityRecommender")]
public static void Run(
  [OrchestrationTrigger] DurableOrchestrationContextBase context)
{
  int userChoice = context.GetInput<int>();

  switch (userChoice)
  {
    case 1:
    context.SetCustomStatus(new
    {
      recommendedCities = new[] {"Tokyo", "Seattle"},
      recommendedSeasons = new[] {"Spring", "Summer"}
     });
      break;
    case 2:
      context.SetCustomStatus(new
      {
        recommendedCity = new[] {"Seattle, London"},
        recommendedSeasons = new[] {"Summer"}
      });
        break;
      case 3:
      context.SetCustomStatus(new
      {
        recommendedCity = new[] {"Tokyo, London"},
        recommendedSeasons = new[] {"Spring", "Summer"}
      });
        break;
  }

  // Wait for user selection and refine the recommendation
} 
```

### <a name="instruction-specification"></a><span data-ttu-id="ada01-115">Instruction specification</span><span class="sxs-lookup"><span data-stu-id="ada01-115">Instruction specification</span></span> 

<span data-ttu-id="ada01-116">The orchestrator can provide unique instructions to the clients via the custom state.</span><span class="sxs-lookup"><span data-stu-id="ada01-116">The orchestrator can provide unique instructions to the clients via the custom state.</span></span> <span data-ttu-id="ada01-117">The custom status instructions will be mapped to the steps in the orchestration code:</span><span class="sxs-lookup"><span data-stu-id="ada01-117">The custom status instructions will be mapped to the steps in the orchestration code:</span></span>

```csharp
[FunctionName("ReserveTicket")]
public static async Task<bool> Run(
  [OrchestrationTrigger] DurableOrchestrationContextBase context)
{
  string userId = context.GetInput<string>();

  int discount = await context.CallActivityAsync<int>("CalculateDiscount", userId);

  context.SetCustomStatus(new
  {
    discount = discount,
    discountTimeout = 60,
    bookingUrl = "https://www.myawesomebookingweb.com",
  });

  bool isBookingConfirmed = await context.WaitForExternalEvent<bool>("BookingConfirmed");

  context.SetCustomStatus(isBookingConfirmed
    ? new {message = "Thank you for confirming your booking."}
    : new {message = "The booking was not confirmed on time. Please try again."});

  return isBookingConfirmed;
}
```

## <a name="sample"></a><span data-ttu-id="ada01-118">Sample</span><span class="sxs-lookup"><span data-stu-id="ada01-118">Sample</span></span>

<span data-ttu-id="ada01-119">In the following sample, the custom status is set first;</span><span class="sxs-lookup"><span data-stu-id="ada01-119">In the following sample, the custom status is set first;</span></span>

```csharp
public static async Task SetStatusTest([OrchestrationTrigger] DurableOrchestrationContext ctx)
{
    // ...do work...

    // update the status of the orchestration with some arbitrary data
    var customStatus = new { nextActions = new [] {"A", "B", "C"}, foo = 2, };
    ctx.SetCustomStatus(customStatus);

    // ...do more work...
}
```

<span data-ttu-id="ada01-120">While the orchestration is running, external clients can fetch this custom status:</span><span class="sxs-lookup"><span data-stu-id="ada01-120">While the orchestration is running, external clients can fetch this custom status:</span></span>

```http
GET /admin/extensions/DurableTaskExtension/instances/instance123

```

<span data-ttu-id="ada01-121">Clients will get the following response:</span><span class="sxs-lookup"><span data-stu-id="ada01-121">Clients will get the following response:</span></span> 

```http
{
  "runtimeStatus": "Running",
  "input": null,
  "customStatus": { "nextActions": ["A", "B", "C"], "foo": 2 },
  "output": null,
  "createdTime": "2017-10-06T18:30:24Z",
  "lastUpdatedTime": "2017-10-06T19:40:30Z"
}
```

> [!WARNING]
>  <span data-ttu-id="ada01-122">The custom status payload is limited to 16 KB of UTF-16 JSON text because it needs to be able to fit in an Azure Table Storage column.</span><span class="sxs-lookup"><span data-stu-id="ada01-122">The custom status payload is limited to 16 KB of UTF-16 JSON text because it needs to be able to fit in an Azure Table Storage column.</span></span> <span data-ttu-id="ada01-123">Developers can use external storage if they need larger payload.</span><span class="sxs-lookup"><span data-stu-id="ada01-123">Developers can use external storage if they need larger payload.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ada01-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="ada01-124">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ada01-125">Learn about HTTP APIs in Durable Functions</span><span class="sxs-lookup"><span data-stu-id="ada01-125">Learn about HTTP APIs in Durable Functions</span></span>](durable-functions-http-api.md)


