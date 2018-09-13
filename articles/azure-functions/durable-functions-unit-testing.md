---
title: Azure Durable Functions unit testing
description: Learn how to unit test Durable Functions.
services: functions
author: kadimitr
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 02/28/2018
ms.author: kadimitr
ms.openlocfilehash: 81d187cf5b75b7bd943d9dcedc97b56ba9c397de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867782"
---
# <a name="durable-functions-unit-testing"></a><span data-ttu-id="5f2a5-103">Durable Functions unit testing</span><span class="sxs-lookup"><span data-stu-id="5f2a5-103">Durable Functions unit testing</span></span>

<span data-ttu-id="5f2a5-104">Unit testing is an important part of modern software development practices.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-104">Unit testing is an important part of modern software development practices.</span></span> <span data-ttu-id="5f2a5-105">Unit tests verify business logic behavior and protect from introducing unnoticed breaking changes in the future.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-105">Unit tests verify business logic behavior and protect from introducing unnoticed breaking changes in the future.</span></span> <span data-ttu-id="5f2a5-106">Durable Functions can easily grow in complexity so introducing unit tests will help to avoid breaking changes.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-106">Durable Functions can easily grow in complexity so introducing unit tests will help to avoid breaking changes.</span></span> <span data-ttu-id="5f2a5-107">The following sections explain how to unit test the three function types - Orchestration client, Orchestrator, and Activity functions.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-107">The following sections explain how to unit test the three function types - Orchestration client, Orchestrator, and Activity functions.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5f2a5-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5f2a5-108">Prerequisites</span></span>

<span data-ttu-id="5f2a5-109">The examples in this article require knowledge of the following concepts and frameworks:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-109">The examples in this article require knowledge of the following concepts and frameworks:</span></span> 

* <span data-ttu-id="5f2a5-110">Unit testing</span><span class="sxs-lookup"><span data-stu-id="5f2a5-110">Unit testing</span></span>

* <span data-ttu-id="5f2a5-111">Durable Functions</span><span class="sxs-lookup"><span data-stu-id="5f2a5-111">Durable Functions</span></span> 

* <span data-ttu-id="5f2a5-112">[xUnit](https://xunit.github.io/) - Testing framework</span><span class="sxs-lookup"><span data-stu-id="5f2a5-112">[xUnit](https://xunit.github.io/) - Testing framework</span></span>

* <span data-ttu-id="5f2a5-113">[moq](https://github.com/moq/moq4) - Mocking framework</span><span class="sxs-lookup"><span data-stu-id="5f2a5-113">[moq](https://github.com/moq/moq4) - Mocking framework</span></span>


## <a name="base-classes-for-mocking"></a><span data-ttu-id="5f2a5-114">Base classes for mocking</span><span class="sxs-lookup"><span data-stu-id="5f2a5-114">Base classes for mocking</span></span> 

<span data-ttu-id="5f2a5-115">Mocking is supported via two abstract classes in Durable Functions:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-115">Mocking is supported via two abstract classes in Durable Functions:</span></span>

* [<span data-ttu-id="5f2a5-116">DurableOrchestrationClientBase</span><span class="sxs-lookup"><span data-stu-id="5f2a5-116">DurableOrchestrationClientBase</span></span>](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClientBase.html) 

* [<span data-ttu-id="5f2a5-117">DurableOrchestrationContextBase</span><span class="sxs-lookup"><span data-stu-id="5f2a5-117">DurableOrchestrationContextBase</span></span>](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContextBase.html)

<span data-ttu-id="5f2a5-118">These classes are base classes for [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) and [DurableOrchestrationContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html) that define Orchestration Client and Orchestrator methods.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-118">These classes are base classes for [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) and [DurableOrchestrationContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html) that define Orchestration Client and Orchestrator methods.</span></span> <span data-ttu-id="5f2a5-119">The mocks will set expected behavior for base class methods so the unit test can verify the business logic.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-119">The mocks will set expected behavior for base class methods so the unit test can verify the business logic.</span></span> <span data-ttu-id="5f2a5-120">There is a two-step workflow for unit testing the business logic in the Orchestration Client and Orchestrator:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-120">There is a two-step workflow for unit testing the business logic in the Orchestration Client and Orchestrator:</span></span>

1. <span data-ttu-id="5f2a5-121">Use the base classes instead of the concrete implementation when defining Orchestration Client and Orchestrator's signatures.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-121">Use the base classes instead of the concrete implementation when defining Orchestration Client and Orchestrator's signatures.</span></span>
2. <span data-ttu-id="5f2a5-122">In the unit tests mock the behavior of the base classes and verify the business logic.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-122">In the unit tests mock the behavior of the base classes and verify the business logic.</span></span> 

<span data-ttu-id="5f2a5-123">Find more details in the following paragraphs for testing functions that use the orchestration client binding and the orchestrator trigger binding.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-123">Find more details in the following paragraphs for testing functions that use the orchestration client binding and the orchestrator trigger binding.</span></span>

## <a name="unit-testing-trigger-functions"></a><span data-ttu-id="5f2a5-124">Unit testing trigger functions</span><span class="sxs-lookup"><span data-stu-id="5f2a5-124">Unit testing trigger functions</span></span>

<span data-ttu-id="5f2a5-125">In this section, the unit test will validate the logic of the following HTTP trigger function for starting new orchestrations.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-125">In this section, the unit test will validate the logic of the following HTTP trigger function for starting new orchestrations.</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/HttpStart.cs)]

<span data-ttu-id="5f2a5-126">The unit test task will be to verify the value of the `Retry-After` header provided in the response payload.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-126">The unit test task will be to verify the value of the `Retry-After` header provided in the response payload.</span></span> <span data-ttu-id="5f2a5-127">So the unit test will mock some of [DurableOrchestrationClientBase](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClientBase.html) methods to ensure predictable behavior.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-127">So the unit test will mock some of [DurableOrchestrationClientBase](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClientBase.html) methods to ensure predictable behavior.</span></span> 

<span data-ttu-id="5f2a5-128">First, a mock of the base class is required, [DurableOrchestrationClientBase](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClientBase.html).</span><span class="sxs-lookup"><span data-stu-id="5f2a5-128">First, a mock of the base class is required, [DurableOrchestrationClientBase](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClientBase.html).</span></span> <span data-ttu-id="5f2a5-129">The mock can be a new class that implements [DurableOrchestrationClientBase](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClientBase.html).</span><span class="sxs-lookup"><span data-stu-id="5f2a5-129">The mock can be a new class that implements [DurableOrchestrationClientBase](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClientBase.html).</span></span> <span data-ttu-id="5f2a5-130">However, using a mocking framework like [moq](https://github.com/moq/moq4) simplifies the process:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-130">However, using a mocking framework like [moq](https://github.com/moq/moq4) simplifies the process:</span></span>    

```csharp
    // Mock DurableOrchestrationClientBase
    var durableOrchestrationClientBaseMock = new Mock<DurableOrchestrationClientBase>();
```

<span data-ttu-id="5f2a5-131">Then `StartNewAsync` method is mocked to return a well-known instance ID.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-131">Then `StartNewAsync` method is mocked to return a well-known instance ID.</span></span>

```csharp
    // Mock StartNewAsync method
    durableOrchestrationClientBaseMock.
        Setup(x => x.StartNewAsync(functionName, It.IsAny<object>())).
        ReturnsAsync(instanceId);
```

<span data-ttu-id="5f2a5-132">Next `CreateCheckStatusResponse` is mocked to always return an empty HTTP 200 response.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-132">Next `CreateCheckStatusResponse` is mocked to always return an empty HTTP 200 response.</span></span>

```csharp
    // Mock CreateCheckStatusResponse method
    durableOrchestrationClientBaseMock
        .Setup(x => x.CreateCheckStatusResponse(It.IsAny<HttpRequestMessage>(), instanceId))
        .Returns(new HttpResponseMessage
        {
            StatusCode = HttpStatusCode.OK,
            Content = new StringContent(string.Empty),
        });
```

<span data-ttu-id="5f2a5-133">`TraceWriter` is also mocked:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-133">`TraceWriter` is also mocked:</span></span>

```csharp
    // Mock TraceWriter
    var traceWriterMock = new Mock<TraceWriter>(TraceLevel.Info);

```  

<span data-ttu-id="5f2a5-134">Now the `Run` method is called from the unit test:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-134">Now the `Run` method is called from the unit test:</span></span>

```csharp
    // Call Orchestration trigger function
    var result = await HttpStart.Run(
        new HttpRequestMessage()
        {
            Content = new StringContent("{}", Encoding.UTF8, "application/json"),
            RequestUri = new Uri("http://localhost:7071/orchestrators/E1_HelloSequence"),
        },
        durableOrchestrationClientBaseMock.Object, 
        functionName,
        traceWriterMock.Object);
 ``` 

 <span data-ttu-id="5f2a5-135">The last step is to compare the output with the expected value:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-135">The last step is to compare the output with the expected value:</span></span>

```csharp
    // Validate that output is not null
    Assert.NotNull(result.Headers.RetryAfter);

    // Validate output's Retry-After header value
    Assert.Equal(TimeSpan.FromSeconds(10), result.Headers.RetryAfter.Delta);
```

<span data-ttu-id="5f2a5-136">After combining all steps, the unit test will have the following code:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-136">After combining all steps, the unit test will have the following code:</span></span> 

[!code-csharp[Main](~/samples-durable-functions/samples/VSSample.Tests/HttpStartTests.cs)]

## <a name="unit-testing-orchestrator-functions"></a><span data-ttu-id="5f2a5-137">Unit testing orchestrator functions</span><span class="sxs-lookup"><span data-stu-id="5f2a5-137">Unit testing orchestrator functions</span></span>

<span data-ttu-id="5f2a5-138">Orchestrator functions are even more interesting for unit testing since they usually have a lot more business logic.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-138">Orchestrator functions are even more interesting for unit testing since they usually have a lot more business logic.</span></span>

<span data-ttu-id="5f2a5-139">In this section the unit tests will validate the output of the `E1_HelloSequence` Orchestrator function:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-139">In this section the unit tests will validate the output of the `E1_HelloSequence` Orchestrator function:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/HelloSequence.cs)]

<span data-ttu-id="5f2a5-140">The unit test code will start with creating a mock:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-140">The unit test code will start with creating a mock:</span></span>

```csharp
    var durableOrchestrationContextMock = new Mock<DurableOrchestrationContextBase>();
```

<span data-ttu-id="5f2a5-141">Then the activity method calls will be mocked:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-141">Then the activity method calls will be mocked:</span></span>

```csharp
    durableOrchestrationContextMock.Setup(x => x.CallActivityAsync<string>("E1_SayHello", "Tokyo")).ReturnsAsync("Hello Tokyo!");
    durableOrchestrationContextMock.Setup(x => x.CallActivityAsync<string>("E1_SayHello", "Seattle")).ReturnsAsync("Hello Seattle!");
    durableOrchestrationContextMock.Setup(x => x.CallActivityAsync<string>("E1_SayHello", "London")).ReturnsAsync("Hello London!");
```

<span data-ttu-id="5f2a5-142">Next the unit test will call `HelloSequence.Run` method:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-142">Next the unit test will call `HelloSequence.Run` method:</span></span>

```csharp
    var result = await HelloSequence.Run(durableOrchestrationContextMock.Object);
```

<span data-ttu-id="5f2a5-143">And finally the output will be validated:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-143">And finally the output will be validated:</span></span>

```csharp
    Assert.Equal(3, result.Count);
    Assert.Equal("Hello Tokyo!", result[0]);
    Assert.Equal("Hello Seattle!", result[1]);
    Assert.Equal("Hello London!", result[2]);
```

<span data-ttu-id="5f2a5-144">After combining all steps, the unit test will have the following code:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-144">After combining all steps, the unit test will have the following code:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/VSSample.Tests/HelloSequenceOrchestratorTests.cs)]

## <a name="unit-testing-activity-functions"></a><span data-ttu-id="5f2a5-145">Unit testing activity functions</span><span class="sxs-lookup"><span data-stu-id="5f2a5-145">Unit testing activity functions</span></span>

<span data-ttu-id="5f2a5-146">Activity functions can be unit tested in the same way as non-durable functions.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-146">Activity functions can be unit tested in the same way as non-durable functions.</span></span> <span data-ttu-id="5f2a5-147">Activity functions don't have a base class for mocking.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-147">Activity functions don't have a base class for mocking.</span></span> <span data-ttu-id="5f2a5-148">So the unit tests use the parameter types directly.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-148">So the unit tests use the parameter types directly.</span></span>

<span data-ttu-id="5f2a5-149">In this section the unit test will validate the behavior of the `E1_SayHello` Activity function:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-149">In this section the unit test will validate the behavior of the `E1_SayHello` Activity function:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/HelloSequence.cs)]

<span data-ttu-id="5f2a5-150">And the unit test will verify the format of the output:</span><span class="sxs-lookup"><span data-stu-id="5f2a5-150">And the unit test will verify the format of the output:</span></span>

[!code-csharp[Main](~/samples-durable-functions/samples/VSSample.Tests/HelloSequenceActivityTests.cs)]

## <a name="next-steps"></a><span data-ttu-id="5f2a5-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="5f2a5-151">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5f2a5-152">Learn more about xUnit</span><span class="sxs-lookup"><span data-stu-id="5f2a5-152">Learn more about xUnit</span></span>](http://xunit.github.io/docs/getting-started-dotnet-core)

> [<span data-ttu-id="5f2a5-153">Learn more about moq</span><span class="sxs-lookup"><span data-stu-id="5f2a5-153">Learn more about moq</span></span>](https://github.com/Moq/moq4/wiki/Quickstart)
