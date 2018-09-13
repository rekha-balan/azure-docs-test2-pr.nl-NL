---
title: Azure Blockchain Workbench messages integration overview
description: Overview of using messages in Azure Blockchain Workbench.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 4/16/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: mmercuri
manager: femila
ms.openlocfilehash: f45396c3af285026e16ce641bd37bf0eadcee56d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856331"
---
# <a name="azure-blockchain-workbench-messaging-integration"></a><span data-ttu-id="94a6f-103">Azure Blockchain Workbench messaging integration</span><span class="sxs-lookup"><span data-stu-id="94a6f-103">Azure Blockchain Workbench messaging integration</span></span>

<span data-ttu-id="94a6f-104">In addition to providing a REST API, Azure Blockchain Workbench also provides messaging-based integration.</span><span class="sxs-lookup"><span data-stu-id="94a6f-104">In addition to providing a REST API, Azure Blockchain Workbench also provides messaging-based integration.</span></span> <span data-ttu-id="94a6f-105">Workbench publishes ledger-centric events via Azure Event Grid, enabling downstream consumers to ingest data or take action based on these events.</span><span class="sxs-lookup"><span data-stu-id="94a6f-105">Workbench publishes ledger-centric events via Azure Event Grid, enabling downstream consumers to ingest data or take action based on these events.</span></span> <span data-ttu-id="94a6f-106">For those clients that require reliable messaging, Azure Blockchain Workbench delivers messages to an Azure Service Bus endpoint as well.</span><span class="sxs-lookup"><span data-stu-id="94a6f-106">For those clients that require reliable messaging, Azure Blockchain Workbench delivers messages to an Azure Service Bus endpoint as well.</span></span>

<span data-ttu-id="94a6f-107">Developers have also expressed interest in the ability to have external systems communicate initiate transactions to create users, create contracts, and update contracts on a ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-107">Developers have also expressed interest in the ability to have external systems communicate initiate transactions to create users, create contracts, and update contracts on a ledger.</span></span> <span data-ttu-id="94a6f-108">While this functionality is not currently exposed in public preview, a sample that delivers that capability can be found at [http://aka.ms/blockchain-workbench-integration-sample](http://aka.ms/blockchain-workbench-integration-sample).</span><span class="sxs-lookup"><span data-stu-id="94a6f-108">While this functionality is not currently exposed in public preview, a sample that delivers that capability can be found at [http://aka.ms/blockchain-workbench-integration-sample](http://aka.ms/blockchain-workbench-integration-sample).</span></span>

## <a name="event-notifications"></a><span data-ttu-id="94a6f-109">Event notifications</span><span class="sxs-lookup"><span data-stu-id="94a6f-109">Event notifications</span></span>

<span data-ttu-id="94a6f-110">Event notifications can be used to notify users and downstream systems of events that happen in Blockchain Workbench and the blockchain network it is connected to.</span><span class="sxs-lookup"><span data-stu-id="94a6f-110">Event notifications can be used to notify users and downstream systems of events that happen in Blockchain Workbench and the blockchain network it is connected to.</span></span> <span data-ttu-id="94a6f-111">Event notifications can be consumed directly in code or used with tools such as Logic Apps and Flow to trigger flow of data to downstream systems.</span><span class="sxs-lookup"><span data-stu-id="94a6f-111">Event notifications can be consumed directly in code or used with tools such as Logic Apps and Flow to trigger flow of data to downstream systems.</span></span>

<span data-ttu-id="94a6f-112">See [Notification message reference](#notification-message-reference) for details of various messages that can be received.</span><span class="sxs-lookup"><span data-stu-id="94a6f-112">See [Notification message reference](#notification-message-reference) for details of various messages that can be received.</span></span>

### <a name="consuming-event-grid-events-with-azure-functions"></a><span data-ttu-id="94a6f-113">Consuming Event Grid events with Azure Functions</span><span class="sxs-lookup"><span data-stu-id="94a6f-113">Consuming Event Grid events with Azure Functions</span></span>

<span data-ttu-id="94a6f-114">If a user wants to use Event Grid to be notified about events that happen in Blockchain Workbench, you can consume events from Event Grid by using Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="94a6f-114">If a user wants to use Event Grid to be notified about events that happen in Blockchain Workbench, you can consume events from Event Grid by using Azure Functions.</span></span>

1. <span data-ttu-id="94a6f-115">Create an **Azure Function App** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94a6f-115">Create an **Azure Function App** in the Azure portal.</span></span>
2. <span data-ttu-id="94a6f-116">Create a new function.</span><span class="sxs-lookup"><span data-stu-id="94a6f-116">Create a new function.</span></span>
3. <span data-ttu-id="94a6f-117">Locate the template for Event Grid.</span><span class="sxs-lookup"><span data-stu-id="94a6f-117">Locate the template for Event Grid.</span></span> <span data-ttu-id="94a6f-118">Basic template code for reading the message is shown.</span><span class="sxs-lookup"><span data-stu-id="94a6f-118">Basic template code for reading the message is shown.</span></span> <span data-ttu-id="94a6f-119">Modify the code as needed.</span><span class="sxs-lookup"><span data-stu-id="94a6f-119">Modify the code as needed.</span></span>
4. <span data-ttu-id="94a6f-120">Save the Function.</span><span class="sxs-lookup"><span data-stu-id="94a6f-120">Save the Function.</span></span> 
5. <span data-ttu-id="94a6f-121">Select the Event Grid from Blockchain Workbench’s resource group.</span><span class="sxs-lookup"><span data-stu-id="94a6f-121">Select the Event Grid from Blockchain Workbench’s resource group.</span></span>

### <a name="consuming-event-grid-events-with-logic-apps"></a><span data-ttu-id="94a6f-122">Consuming Event Grid events with Logic Apps</span><span class="sxs-lookup"><span data-stu-id="94a6f-122">Consuming Event Grid events with Logic Apps</span></span>

1.  <span data-ttu-id="94a6f-123">Create a new **Azure Logic App** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94a6f-123">Create a new **Azure Logic App** in the Azure portal.</span></span>
2.  <span data-ttu-id="94a6f-124">When opening the Azure Logic App in the portal, you will be prompted to select a trigger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-124">When opening the Azure Logic App in the portal, you will be prompted to select a trigger.</span></span> <span data-ttu-id="94a6f-125">Select **Azure Event Grid -- When a resource event occurs**.</span><span class="sxs-lookup"><span data-stu-id="94a6f-125">Select **Azure Event Grid -- When a resource event occurs**.</span></span>
3. <span data-ttu-id="94a6f-126">When the workflow designer is displayed, you will be prompted to sign in.</span><span class="sxs-lookup"><span data-stu-id="94a6f-126">When the workflow designer is displayed, you will be prompted to sign in.</span></span>
4. <span data-ttu-id="94a6f-127">Select the Subscription.</span><span class="sxs-lookup"><span data-stu-id="94a6f-127">Select the Subscription.</span></span> <span data-ttu-id="94a6f-128">Resource as **Microsoft.EventGrid.Topics**.</span><span class="sxs-lookup"><span data-stu-id="94a6f-128">Resource as **Microsoft.EventGrid.Topics**.</span></span> <span data-ttu-id="94a6f-129">Select the **Resource Name** from the name of the resource from the Azure Blockchain Workbench resource group.</span><span class="sxs-lookup"><span data-stu-id="94a6f-129">Select the **Resource Name** from the name of the resource from the Azure Blockchain Workbench resource group.</span></span>
5. <span data-ttu-id="94a6f-130">Select the Event Grid from Blockchain Workbench's resource group.</span><span class="sxs-lookup"><span data-stu-id="94a6f-130">Select the Event Grid from Blockchain Workbench's resource group.</span></span>

## <a name="using-service-bus-topics-for-notifications"></a><span data-ttu-id="94a6f-131">Using Service Bus Topics for notifications</span><span class="sxs-lookup"><span data-stu-id="94a6f-131">Using Service Bus Topics for notifications</span></span>

<span data-ttu-id="94a6f-132">Service Bus Topics can be used to notify users about events that happen in Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="94a6f-132">Service Bus Topics can be used to notify users about events that happen in Blockchain Workbench.</span></span> 

1.  <span data-ttu-id="94a6f-133">Browse to the Service Bus within the Workbench’s resource group.</span><span class="sxs-lookup"><span data-stu-id="94a6f-133">Browse to the Service Bus within the Workbench’s resource group.</span></span>
2.  <span data-ttu-id="94a6f-134">Select **Topics**.</span><span class="sxs-lookup"><span data-stu-id="94a6f-134">Select **Topics**.</span></span>
3.  <span data-ttu-id="94a6f-135">Select **workbench-external**.</span><span class="sxs-lookup"><span data-stu-id="94a6f-135">Select **workbench-external**.</span></span>
4.  <span data-ttu-id="94a6f-136">Create a new subscription to this topic.</span><span class="sxs-lookup"><span data-stu-id="94a6f-136">Create a new subscription to this topic.</span></span> <span data-ttu-id="94a6f-137">Obtain a key for it.</span><span class="sxs-lookup"><span data-stu-id="94a6f-137">Obtain a key for it.</span></span>
5.  <span data-ttu-id="94a6f-138">Create a program, which subscribes to events from this subscription.</span><span class="sxs-lookup"><span data-stu-id="94a6f-138">Create a program, which subscribes to events from this subscription.</span></span>

### <a name="consuming-service-bus-messages-with-logic-apps"></a><span data-ttu-id="94a6f-139">Consuming Service Bus Messages with Logic Apps</span><span class="sxs-lookup"><span data-stu-id="94a6f-139">Consuming Service Bus Messages with Logic Apps</span></span>

1. <span data-ttu-id="94a6f-140">Create a new **Azure Logic App** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94a6f-140">Create a new **Azure Logic App** in the Azure portal.</span></span>
2. <span data-ttu-id="94a6f-141">When opening the Azure Logic App in the portal, you will be prompted to select a trigger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-141">When opening the Azure Logic App in the portal, you will be prompted to select a trigger.</span></span> <span data-ttu-id="94a6f-142">Type **Service Bus** into the search box and select the trigger appropriate for the type of interaction you want to have with the Service Bus.</span><span class="sxs-lookup"><span data-stu-id="94a6f-142">Type **Service Bus** into the search box and select the trigger appropriate for the type of interaction you want to have with the Service Bus.</span></span> <span data-ttu-id="94a6f-143">For example, **Service Bus -- When a message is received in a topic subscription (auto-complete)**.</span><span class="sxs-lookup"><span data-stu-id="94a6f-143">For example, **Service Bus -- When a message is received in a topic subscription (auto-complete)**.</span></span>
3. <span data-ttu-id="94a6f-144">When the workflow designer is displayed, specify the connection information for the Service Bus.</span><span class="sxs-lookup"><span data-stu-id="94a6f-144">When the workflow designer is displayed, specify the connection information for the Service Bus.</span></span>
4. <span data-ttu-id="94a6f-145">Select your subscription and specify the topic of **workbench-external**.</span><span class="sxs-lookup"><span data-stu-id="94a6f-145">Select your subscription and specify the topic of **workbench-external**.</span></span>
5. <span data-ttu-id="94a6f-146">Develop the logic for your application that utilizes the message from this trigger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-146">Develop the logic for your application that utilizes the message from this trigger.</span></span>

## <a name="notification-message-reference"></a><span data-ttu-id="94a6f-147">Notification message reference</span><span class="sxs-lookup"><span data-stu-id="94a6f-147">Notification message reference</span></span>

<span data-ttu-id="94a6f-148">Depending on the **OperationName**, the notification messages have one of the following message types.</span><span class="sxs-lookup"><span data-stu-id="94a6f-148">Depending on the **OperationName**, the notification messages have one of the following message types.</span></span>

### <a name="accountcreated"></a><span data-ttu-id="94a6f-149">AccountCreated</span><span class="sxs-lookup"><span data-stu-id="94a6f-149">AccountCreated</span></span>

<span data-ttu-id="94a6f-150">Indicates that a new account has been requested to be added to the specified chain.</span><span class="sxs-lookup"><span data-stu-id="94a6f-150">Indicates that a new account has been requested to be added to the specified chain.</span></span>

| <span data-ttu-id="94a6f-151">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-151">Name</span></span>    | <span data-ttu-id="94a6f-152">Description</span><span class="sxs-lookup"><span data-stu-id="94a6f-152">Description</span></span>  |
|----------|--------------|
| <span data-ttu-id="94a6f-153">UserId</span><span class="sxs-lookup"><span data-stu-id="94a6f-153">UserId</span></span>  | <span data-ttu-id="94a6f-154">ID of the user that was created.</span><span class="sxs-lookup"><span data-stu-id="94a6f-154">ID of the user that was created.</span></span> |
| <span data-ttu-id="94a6f-155">ChainIdentifier</span><span class="sxs-lookup"><span data-stu-id="94a6f-155">ChainIdentifier</span></span> | <span data-ttu-id="94a6f-156">Address of the user that was created on the blockchain network.</span><span class="sxs-lookup"><span data-stu-id="94a6f-156">Address of the user that was created on the blockchain network.</span></span> <span data-ttu-id="94a6f-157">In Ethereum, this would be the user's **on-chain** address.</span><span class="sxs-lookup"><span data-stu-id="94a6f-157">In Ethereum, this would be the user's **on-chain** address.</span></span> |

``` csharp
public class NewAccountRequest : MessageModelBase
{
  public int UserID { get; set; }
  public string ChainIdentifier { get; set; }
}
```

### <a name="contractinsertedorupdated"></a><span data-ttu-id="94a6f-158">ContractInsertedOrUpdated</span><span class="sxs-lookup"><span data-stu-id="94a6f-158">ContractInsertedOrUpdated</span></span>

<span data-ttu-id="94a6f-159">Indicates that a request has been made to insert or update a contract on a distributed ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-159">Indicates that a request has been made to insert or update a contract on a distributed ledger.</span></span>

| <span data-ttu-id="94a6f-160">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-160">Name</span></span> | <span data-ttu-id="94a6f-161">Description</span><span class="sxs-lookup"><span data-stu-id="94a6f-161">Description</span></span> |
|-----|--------------|
| <span data-ttu-id="94a6f-162">ChainID</span><span class="sxs-lookup"><span data-stu-id="94a6f-162">ChainID</span></span> | <span data-ttu-id="94a6f-163">A unique identifier for the chain associated with the request.</span><span class="sxs-lookup"><span data-stu-id="94a6f-163">A unique identifier for the chain associated with the request.</span></span>|
| <span data-ttu-id="94a6f-164">BlockId</span><span class="sxs-lookup"><span data-stu-id="94a6f-164">BlockId</span></span> | <span data-ttu-id="94a6f-165">The unique identifier for a block on the ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-165">The unique identifier for a block on the ledger.</span></span>|
| <span data-ttu-id="94a6f-166">ContractId</span><span class="sxs-lookup"><span data-stu-id="94a6f-166">ContractId</span></span> | <span data-ttu-id="94a6f-167">A unique identifier for the contract.</span><span class="sxs-lookup"><span data-stu-id="94a6f-167">A unique identifier for the contract.</span></span>|
| <span data-ttu-id="94a6f-168">ContractAddress</span><span class="sxs-lookup"><span data-stu-id="94a6f-168">ContractAddress</span></span> |       <span data-ttu-id="94a6f-169">The address of the contract on the ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-169">The address of the contract on the ledger.</span></span>|
| <span data-ttu-id="94a6f-170">TransactionHash</span><span class="sxs-lookup"><span data-stu-id="94a6f-170">TransactionHash</span></span>  |     <span data-ttu-id="94a6f-171">The hash of the transaction on the ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-171">The hash of the transaction on the ledger.</span></span>|
| <span data-ttu-id="94a6f-172">OriginatingAddress</span><span class="sxs-lookup"><span data-stu-id="94a6f-172">OriginatingAddress</span></span> |   <span data-ttu-id="94a6f-173">The address of the originator of the transaction.</span><span class="sxs-lookup"><span data-stu-id="94a6f-173">The address of the originator of the transaction.</span></span>|
| <span data-ttu-id="94a6f-174">ActionName</span><span class="sxs-lookup"><span data-stu-id="94a6f-174">ActionName</span></span>       |     <span data-ttu-id="94a6f-175">The name of the action.</span><span class="sxs-lookup"><span data-stu-id="94a6f-175">The name of the action.</span></span>|
| <span data-ttu-id="94a6f-176">IsUpdate</span><span class="sxs-lookup"><span data-stu-id="94a6f-176">IsUpdate</span></span>        |      <span data-ttu-id="94a6f-177">Identifies if this is an update.</span><span class="sxs-lookup"><span data-stu-id="94a6f-177">Identifies if this is an update.</span></span>|
| <span data-ttu-id="94a6f-178">Parameters</span><span class="sxs-lookup"><span data-stu-id="94a6f-178">Parameters</span></span>       |     <span data-ttu-id="94a6f-179">A list of objects that identify the name, value, and data type of parameters sent to an action.</span><span class="sxs-lookup"><span data-stu-id="94a6f-179">A list of objects that identify the name, value, and data type of parameters sent to an action.</span></span>|
| <span data-ttu-id="94a6f-180">TopLevelInputParams</span><span class="sxs-lookup"><span data-stu-id="94a6f-180">TopLevelInputParams</span></span> |  <span data-ttu-id="94a6f-181">In scenarios where a contract is connected to one or more other contracts, these are the parameters from the top-level contract.</span><span class="sxs-lookup"><span data-stu-id="94a6f-181">In scenarios where a contract is connected to one or more other contracts, these are the parameters from the top-level contract.</span></span> |

``` csharp
public class ContractInsertOrUpdateRequest : MessageModelBase
{
    public int ChainId { get; set; }
    public int BlockId { get; set; }
    public int ContractId { get; set; }
    public string ContractAddress { get; set; }
    public string TransactionHash { get; set; }
    public string OriginatingAddress { get; set; }
    public string ActionName { get; set; }
    public bool IsUpdate { get; set; }
    public List<ContractProperty> Parameters { get; set; }
    public bool IsTopLevelUpdate { get; set; }
    public List<ContractInputParameter> TopLevelInputParams { get; set; }
}
```

#### <a name="updatecontractaction"></a><span data-ttu-id="94a6f-182">UpdateContractAction</span><span class="sxs-lookup"><span data-stu-id="94a6f-182">UpdateContractAction</span></span>

<span data-ttu-id="94a6f-183">Indicates that a request has been made to execution an action on a specific contract on a distributed ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-183">Indicates that a request has been made to execution an action on a specific contract on a distributed ledger.</span></span>

| <span data-ttu-id="94a6f-184">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-184">Name</span></span>                     | <span data-ttu-id="94a6f-185">Description</span><span class="sxs-lookup"><span data-stu-id="94a6f-185">Description</span></span>                                                                                                                                                                   |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="94a6f-186">ContractActionId</span><span class="sxs-lookup"><span data-stu-id="94a6f-186">ContractActionId</span></span>         | <span data-ttu-id="94a6f-187">The unique identifier for this contract action</span><span class="sxs-lookup"><span data-stu-id="94a6f-187">The unique identifier for this contract action</span></span>                                                                                                                                |
| <span data-ttu-id="94a6f-188">ChainIdentifier</span><span class="sxs-lookup"><span data-stu-id="94a6f-188">ChainIdentifier</span></span>          | <span data-ttu-id="94a6f-189">The unique identifier for the chain</span><span class="sxs-lookup"><span data-stu-id="94a6f-189">The unique identifier for the chain</span></span>                                                                                                                                           |
| <span data-ttu-id="94a6f-190">ConnectionId</span><span class="sxs-lookup"><span data-stu-id="94a6f-190">ConnectionId</span></span>             | <span data-ttu-id="94a6f-191">The unique identifier for the connection</span><span class="sxs-lookup"><span data-stu-id="94a6f-191">The unique identifier for the connection</span></span>                                                                                                                                      |
| <span data-ttu-id="94a6f-192">UserChainIdentifier</span><span class="sxs-lookup"><span data-stu-id="94a6f-192">UserChainIdentifier</span></span>      | <span data-ttu-id="94a6f-193">Address of the user that was created on the blockchain network.</span><span class="sxs-lookup"><span data-stu-id="94a6f-193">Address of the user that was created on the blockchain network.</span></span> <span data-ttu-id="94a6f-194">In Ethereum, this would be the user’s “on chain” address.</span><span class="sxs-lookup"><span data-stu-id="94a6f-194">In Ethereum, this would be the user’s “on chain” address.</span></span>                                                     |
| <span data-ttu-id="94a6f-195">ContractLedgerIdentifier</span><span class="sxs-lookup"><span data-stu-id="94a6f-195">ContractLedgerIdentifier</span></span> | <span data-ttu-id="94a6f-196">Address of the contract on the ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-196">Address of the contract on the ledger.</span></span>                                                                                                                                        |
| <span data-ttu-id="94a6f-197">WorkflowFunctionName</span><span class="sxs-lookup"><span data-stu-id="94a6f-197">WorkflowFunctionName</span></span>     | <span data-ttu-id="94a6f-198">Name of the workflow function.</span><span class="sxs-lookup"><span data-stu-id="94a6f-198">Name of the workflow function.</span></span>                                                                                                                                                |
| <span data-ttu-id="94a6f-199">WorkflowName</span><span class="sxs-lookup"><span data-stu-id="94a6f-199">WorkflowName</span></span>             | <span data-ttu-id="94a6f-200">Name of the workflow.</span><span class="sxs-lookup"><span data-stu-id="94a6f-200">Name of the workflow.</span></span>                                                                                                                                                         |
| <span data-ttu-id="94a6f-201">WorkflowBlobStorageURL</span><span class="sxs-lookup"><span data-stu-id="94a6f-201">WorkflowBlobStorageURL</span></span>   | <span data-ttu-id="94a6f-202">The url of the contract in blob storage.</span><span class="sxs-lookup"><span data-stu-id="94a6f-202">The url of the contract in blob storage.</span></span>                                                                                                                                      |
| <span data-ttu-id="94a6f-203">ContractActionParameters</span><span class="sxs-lookup"><span data-stu-id="94a6f-203">ContractActionParameters</span></span> | <span data-ttu-id="94a6f-204">Parameters for the contract action.</span><span class="sxs-lookup"><span data-stu-id="94a6f-204">Parameters for the contract action.</span></span>                                                                                                                                           |
| <span data-ttu-id="94a6f-205">TransactionHash</span><span class="sxs-lookup"><span data-stu-id="94a6f-205">TransactionHash</span></span>          | <span data-ttu-id="94a6f-206">The hash of the transaction on the ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-206">The hash of the transaction on the ledger.</span></span>                                                                                                                                    |
| <span data-ttu-id="94a6f-207">Provisioning Status</span><span class="sxs-lookup"><span data-stu-id="94a6f-207">Provisioning Status</span></span>      | <span data-ttu-id="94a6f-208">The current provisioning status of the action.</span><span class="sxs-lookup"><span data-stu-id="94a6f-208">The current provisioning status of the action.</span></span></br><span data-ttu-id="94a6f-209">0 – Created</span><span class="sxs-lookup"><span data-stu-id="94a6f-209">0 – Created</span></span></br><span data-ttu-id="94a6f-210">1 – In Process</span><span class="sxs-lookup"><span data-stu-id="94a6f-210">1 – In Process</span></span></br><span data-ttu-id="94a6f-211">2 – Complete</span><span class="sxs-lookup"><span data-stu-id="94a6f-211">2 – Complete</span></span></br> <span data-ttu-id="94a6f-212">Complete indicates a confirmation from the ledger that this as been successfully added.</span><span class="sxs-lookup"><span data-stu-id="94a6f-212">Complete indicates a confirmation from the ledger that this as been successfully added.</span></span>                                               |
|                          |                                                                                                                                                                               |

```csharp
public class ContractActionRequest : MessageModelBase
{
    public int ContractActionId { get; set; }
    public int ConnectionId { get; set; }
    public string UserChainIdentifier { get; set; }
    public string ContractLedgerIdentifier { get; set; }
    public string WorkflowFunctionName { get; set; }
    public string WorkflowName { get; set; }
    public string WorkflowBlobStorageURL { get; set; }
    public IEnumerable<ContractActionParameter> ContractActionParameters { get; set; }
    public string TransactionHash { get; set; }
    public int ProvisioningStatus { get; set; }
}
```

### <a name="updateuserbalance"></a><span data-ttu-id="94a6f-213">UpdateUserBalance</span><span class="sxs-lookup"><span data-stu-id="94a6f-213">UpdateUserBalance</span></span>

<span data-ttu-id="94a6f-214">Indicates that a request has been made to update the user balance on a specific distributed ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-214">Indicates that a request has been made to update the user balance on a specific distributed ledger.</span></span>

> [!NOTE]
> <span data-ttu-id="94a6f-215">This message is generated only for those ledgers that require the funding of accounts.</span><span class="sxs-lookup"><span data-stu-id="94a6f-215">This message is generated only for those ledgers that require the funding of accounts.</span></span>
> 

| <span data-ttu-id="94a6f-216">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-216">Name</span></span>    | <span data-ttu-id="94a6f-217">Description</span><span class="sxs-lookup"><span data-stu-id="94a6f-217">Description</span></span>                              |
|---------|------------------------------------------|
| <span data-ttu-id="94a6f-218">Address</span><span class="sxs-lookup"><span data-stu-id="94a6f-218">Address</span></span> | <span data-ttu-id="94a6f-219">The address of the user that was funded.</span><span class="sxs-lookup"><span data-stu-id="94a6f-219">The address of the user that was funded.</span></span> |
| <span data-ttu-id="94a6f-220">Balance</span><span class="sxs-lookup"><span data-stu-id="94a6f-220">Balance</span></span> | <span data-ttu-id="94a6f-221">The balance of the user balance.</span><span class="sxs-lookup"><span data-stu-id="94a6f-221">The balance of the user balance.</span></span>         |
| <span data-ttu-id="94a6f-222">ChainID</span><span class="sxs-lookup"><span data-stu-id="94a6f-222">ChainID</span></span> | <span data-ttu-id="94a6f-223">The unique identifier for the chain.</span><span class="sxs-lookup"><span data-stu-id="94a6f-223">The unique identifier for the chain.</span></span>     |


``` csharp
public class UpdateUserBalanceRequest : MessageModelBase
{
    public string Address { get; set; }
    public decimal Balance { get; set; }
    public int ChainID { get; set; }
}
```

### <a name="insertblock"></a><span data-ttu-id="94a6f-224">InsertBlock</span><span class="sxs-lookup"><span data-stu-id="94a6f-224">InsertBlock</span></span>

<span data-ttu-id="94a6f-225">Message indicates that a request has been made to add a block on a distributed ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-225">Message indicates that a request has been made to add a block on a distributed ledger.</span></span>

| <span data-ttu-id="94a6f-226">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-226">Name</span></span>           | <span data-ttu-id="94a6f-227">Description</span><span class="sxs-lookup"><span data-stu-id="94a6f-227">Description</span></span>                                                            |
|----------------|------------------------------------------------------------------------|
| <span data-ttu-id="94a6f-228">ChainId</span><span class="sxs-lookup"><span data-stu-id="94a6f-228">ChainId</span></span>        | <span data-ttu-id="94a6f-229">The unique identifier of the chain to which the block was added.</span><span class="sxs-lookup"><span data-stu-id="94a6f-229">The unique identifier of the chain to which the block was added.</span></span>             |
| <span data-ttu-id="94a6f-230">BlockId</span><span class="sxs-lookup"><span data-stu-id="94a6f-230">BlockId</span></span>        | <span data-ttu-id="94a6f-231">The unique identifier for the block inside Azure Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="94a6f-231">The unique identifier for the block inside Azure Blockchain Workbench.</span></span> |
| <span data-ttu-id="94a6f-232">BlockHash</span><span class="sxs-lookup"><span data-stu-id="94a6f-232">BlockHash</span></span>      | <span data-ttu-id="94a6f-233">The hash of the block.</span><span class="sxs-lookup"><span data-stu-id="94a6f-233">The hash of the block.</span></span>                                                 |
| <span data-ttu-id="94a6f-234">BlockTimeStamp</span><span class="sxs-lookup"><span data-stu-id="94a6f-234">BlockTimeStamp</span></span> | <span data-ttu-id="94a6f-235">The timestamp of the block.</span><span class="sxs-lookup"><span data-stu-id="94a6f-235">The timestamp of the block.</span></span>                                            |

``` csharp
public class InsertBlockRequest : MessageModelBase
{
    public int ChainId { get; set; }
    public int BlockId { get; set; }
    public string BlockHash { get; set; }
    public int BlockTimestamp { get; set; }
}
```

### <a name="inserttransaction"></a><span data-ttu-id="94a6f-236">InsertTransaction</span><span class="sxs-lookup"><span data-stu-id="94a6f-236">InsertTransaction</span></span>

<span data-ttu-id="94a6f-237">Message provides details on a request to add a transaction on a distributed ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-237">Message provides details on a request to add a transaction on a distributed ledger.</span></span>

| <span data-ttu-id="94a6f-238">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-238">Name</span></span>            | <span data-ttu-id="94a6f-239">Description</span><span class="sxs-lookup"><span data-stu-id="94a6f-239">Description</span></span>                                                            |
|-----------------|------------------------------------------------------------------------|
| <span data-ttu-id="94a6f-240">ChainId</span><span class="sxs-lookup"><span data-stu-id="94a6f-240">ChainId</span></span>         | <span data-ttu-id="94a6f-241">The unique identifier of the chain to which the block was added.</span><span class="sxs-lookup"><span data-stu-id="94a6f-241">The unique identifier of the chain to which the block was added.</span></span>             |
| <span data-ttu-id="94a6f-242">BlockId</span><span class="sxs-lookup"><span data-stu-id="94a6f-242">BlockId</span></span>         | <span data-ttu-id="94a6f-243">The unique identifier for the block inside Azure Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="94a6f-243">The unique identifier for the block inside Azure Blockchain Workbench.</span></span> |
| <span data-ttu-id="94a6f-244">TransactionHash</span><span class="sxs-lookup"><span data-stu-id="94a6f-244">TransactionHash</span></span> | <span data-ttu-id="94a6f-245">The hash of the transaction.</span><span class="sxs-lookup"><span data-stu-id="94a6f-245">The hash of the transaction.</span></span>                                           |
| <span data-ttu-id="94a6f-246">From</span><span class="sxs-lookup"><span data-stu-id="94a6f-246">From</span></span>            | <span data-ttu-id="94a6f-247">The address of the originator of the transaction.</span><span class="sxs-lookup"><span data-stu-id="94a6f-247">The address of the originator of the transaction.</span></span>                      |
| <span data-ttu-id="94a6f-248">To</span><span class="sxs-lookup"><span data-stu-id="94a6f-248">To</span></span>              | <span data-ttu-id="94a6f-249">The address of the intended recipient of the transaction.</span><span class="sxs-lookup"><span data-stu-id="94a6f-249">The address of the intended recipient of the transaction.</span></span>              |
| <span data-ttu-id="94a6f-250">Value</span><span class="sxs-lookup"><span data-stu-id="94a6f-250">Value</span></span>           | <span data-ttu-id="94a6f-251">The value included in the transaction.</span><span class="sxs-lookup"><span data-stu-id="94a6f-251">The value included in the transaction.</span></span>                                 |
| <span data-ttu-id="94a6f-252">IsAppBuilderTx</span><span class="sxs-lookup"><span data-stu-id="94a6f-252">IsAppBuilderTx</span></span>  | <span data-ttu-id="94a6f-253">Identifies if this is a Blockchain Workbench transaction.</span><span class="sxs-lookup"><span data-stu-id="94a6f-253">Identifies if this is a Blockchain Workbench transaction.</span></span>                         |

``` csharp
public class InsertTransactionRequest : MessageModelBase
{
    public int ChainId { get; set; }
    public int BlockId { get; set; }
    public string TransactionHash { get; set; }
    public string From { get; set; }
    public string To { get; set; }
    public decimal Value { get; set; }
    public bool IsAppBuilderTx { get; set; }
}
```

### <a name="assigncontractchainidentifier"></a><span data-ttu-id="94a6f-254">AssignContractChainIdentifier</span><span class="sxs-lookup"><span data-stu-id="94a6f-254">AssignContractChainIdentifier</span></span>

<span data-ttu-id="94a6f-255">Provides details on the assignment of a chain identifier for a contract.</span><span class="sxs-lookup"><span data-stu-id="94a6f-255">Provides details on the assignment of a chain identifier for a contract.</span></span> <span data-ttu-id="94a6f-256">For example, in Ethereum blockchain, the address of a contract on the ledger.</span><span class="sxs-lookup"><span data-stu-id="94a6f-256">For example, in Ethereum blockchain, the address of a contract on the ledger.</span></span>

| <span data-ttu-id="94a6f-257">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-257">Name</span></span>            | <span data-ttu-id="94a6f-258">Description</span><span class="sxs-lookup"><span data-stu-id="94a6f-258">Description</span></span>                                                                       |
|-----------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="94a6f-259">ContractId</span><span class="sxs-lookup"><span data-stu-id="94a6f-259">ContractId</span></span>      | <span data-ttu-id="94a6f-260">This is the unique identifier for the contract inside Azure Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="94a6f-260">This is the unique identifier for the contract inside Azure Blockchain Workbench.</span></span> |
| <span data-ttu-id="94a6f-261">ChainIdentifier</span><span class="sxs-lookup"><span data-stu-id="94a6f-261">ChainIdentifier</span></span> | <span data-ttu-id="94a6f-262">This is the identifier for the contract on the chain.</span><span class="sxs-lookup"><span data-stu-id="94a6f-262">This is the identifier for the contract on the chain.</span></span>                             |

``` csharp
public class AssignContractChainIdentifierRequest : MessageModelBase
{
    public int ContractId { get; set; }
    public string ChainIdentifier { get; set; }
}
```

## <a name="classes-used-by-message-types"></a><span data-ttu-id="94a6f-263">Classes used by message types</span><span class="sxs-lookup"><span data-stu-id="94a6f-263">Classes used by message types</span></span>

### <a name="messagemodelbase"></a><span data-ttu-id="94a6f-264">MessageModelBase</span><span class="sxs-lookup"><span data-stu-id="94a6f-264">MessageModelBase</span></span>

<span data-ttu-id="94a6f-265">The base model for all messages.</span><span class="sxs-lookup"><span data-stu-id="94a6f-265">The base model for all messages.</span></span>

| <span data-ttu-id="94a6f-266">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-266">Name</span></span>          | <span data-ttu-id="94a6f-267">Description</span><span class="sxs-lookup"><span data-stu-id="94a6f-267">Description</span></span>                          |
|---------------|--------------------------------------|
| <span data-ttu-id="94a6f-268">OperationName</span><span class="sxs-lookup"><span data-stu-id="94a6f-268">OperationName</span></span> | <span data-ttu-id="94a6f-269">The name of the operation.</span><span class="sxs-lookup"><span data-stu-id="94a6f-269">The name of the operation.</span></span>           |
| <span data-ttu-id="94a6f-270">RequestId</span><span class="sxs-lookup"><span data-stu-id="94a6f-270">RequestId</span></span>     | <span data-ttu-id="94a6f-271">A unique identifier for the request.</span><span class="sxs-lookup"><span data-stu-id="94a6f-271">A unique identifier for the request.</span></span> |

``` csharp
public class MessageModelBase
{
    public string OperationName { get; set; }
    public string RequestId { get; set; }
}
```

### <a name="contractinputparameter"></a><span data-ttu-id="94a6f-272">ContractInputParameter</span><span class="sxs-lookup"><span data-stu-id="94a6f-272">ContractInputParameter</span></span>

<span data-ttu-id="94a6f-273">Contains the name, value and type of a parameter.</span><span class="sxs-lookup"><span data-stu-id="94a6f-273">Contains the name, value and type of a parameter.</span></span>

| <span data-ttu-id="94a6f-274">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-274">Name</span></span>  | <span data-ttu-id="94a6f-275">Description</span><span class="sxs-lookup"><span data-stu-id="94a6f-275">Description</span></span>                 |
|-------|-----------------------------|
| <span data-ttu-id="94a6f-276">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-276">Name</span></span>  | <span data-ttu-id="94a6f-277">The name of the parameter.</span><span class="sxs-lookup"><span data-stu-id="94a6f-277">The name of the parameter.</span></span>  |
| <span data-ttu-id="94a6f-278">Value</span><span class="sxs-lookup"><span data-stu-id="94a6f-278">Value</span></span> | <span data-ttu-id="94a6f-279">The value of the parameter.</span><span class="sxs-lookup"><span data-stu-id="94a6f-279">The value of the parameter.</span></span> |
| <span data-ttu-id="94a6f-280">Type</span><span class="sxs-lookup"><span data-stu-id="94a6f-280">Type</span></span>  | <span data-ttu-id="94a6f-281">The type of the parameter.</span><span class="sxs-lookup"><span data-stu-id="94a6f-281">The type of the parameter.</span></span>  |

``` csharp
public class ContractInputParameter
{
    public string Name { get; set; }
    public string Value { get; set; }
    public string Type { get; set; }
}
```

#### <a name="contractproperty"></a><span data-ttu-id="94a6f-282">ContractProperty</span><span class="sxs-lookup"><span data-stu-id="94a6f-282">ContractProperty</span></span>

<span data-ttu-id="94a6f-283">Contains the ID, name, value and type of a property.</span><span class="sxs-lookup"><span data-stu-id="94a6f-283">Contains the ID, name, value and type of a property.</span></span>

| <span data-ttu-id="94a6f-284">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-284">Name</span></span>  | <span data-ttu-id="94a6f-285">Description</span><span class="sxs-lookup"><span data-stu-id="94a6f-285">Description</span></span>                |
|-------|----------------------------|
| <span data-ttu-id="94a6f-286">Id</span><span class="sxs-lookup"><span data-stu-id="94a6f-286">Id</span></span>    | <span data-ttu-id="94a6f-287">The ID of the property.</span><span class="sxs-lookup"><span data-stu-id="94a6f-287">The ID of the property.</span></span>    |
| <span data-ttu-id="94a6f-288">Name</span><span class="sxs-lookup"><span data-stu-id="94a6f-288">Name</span></span>  | <span data-ttu-id="94a6f-289">The name of the property.</span><span class="sxs-lookup"><span data-stu-id="94a6f-289">The name of the property.</span></span>  |
| <span data-ttu-id="94a6f-290">Value</span><span class="sxs-lookup"><span data-stu-id="94a6f-290">Value</span></span> | <span data-ttu-id="94a6f-291">The value of the property.</span><span class="sxs-lookup"><span data-stu-id="94a6f-291">The value of the property.</span></span> |
| <span data-ttu-id="94a6f-292">Type</span><span class="sxs-lookup"><span data-stu-id="94a6f-292">Type</span></span>  | <span data-ttu-id="94a6f-293">The type of the property.</span><span class="sxs-lookup"><span data-stu-id="94a6f-293">The type of the property.</span></span>  |

``` csharp
public class ContractProperty
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Value { get; set; }
    public string DataType { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="94a6f-294">Next steps</span><span class="sxs-lookup"><span data-stu-id="94a6f-294">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94a6f-295">Smart contract integration patterns</span><span class="sxs-lookup"><span data-stu-id="94a6f-295">Smart contract integration patterns</span></span>](blockchain-workbench-integration-patterns.md)