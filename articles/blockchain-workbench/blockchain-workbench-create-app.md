---
title: Create a blockchain application in Azure Blockchain Workbench
description: How to create a blockchain application in Azure Blockchain Workbench.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/17/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: zeyadr
manager: femila
ms.openlocfilehash: a4b704f433f02afcff7b94f98c19a478caaa02b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868922"
---
# <a name="create-a-blockchain-application-in-azure-blockchain-workbench"></a><span data-ttu-id="6c236-103">Create a blockchain application in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="6c236-103">Create a blockchain application in Azure Blockchain Workbench</span></span>

<span data-ttu-id="6c236-104">You can use Azure Blockchain Workbench to create blockchain applications that represent multi-party workflows defined by configuration and smart contract code.</span><span class="sxs-lookup"><span data-stu-id="6c236-104">You can use Azure Blockchain Workbench to create blockchain applications that represent multi-party workflows defined by configuration and smart contract code.</span></span>

<span data-ttu-id="6c236-105">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="6c236-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c236-106">Configure a blockchain application</span><span class="sxs-lookup"><span data-stu-id="6c236-106">Configure a blockchain application</span></span>
> * <span data-ttu-id="6c236-107">Create a smart contract code file</span><span class="sxs-lookup"><span data-stu-id="6c236-107">Create a smart contract code file</span></span>
> * <span data-ttu-id="6c236-108">Add a blockchain application to Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="6c236-108">Add a blockchain application to Blockchain Workbench</span></span>
> * <span data-ttu-id="6c236-109">Add members to the blockchain application</span><span class="sxs-lookup"><span data-stu-id="6c236-109">Add members to the blockchain application</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c236-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c236-110">Prerequisites</span></span>

* <span data-ttu-id="6c236-111">A Blockchain Workbench deployment.</span><span class="sxs-lookup"><span data-stu-id="6c236-111">A Blockchain Workbench deployment.</span></span> <span data-ttu-id="6c236-112">For more information, see [Azure Blockchain Workbench deployment](blockchain-workbench-deploy.md) for details on deployment.</span><span class="sxs-lookup"><span data-stu-id="6c236-112">For more information, see [Azure Blockchain Workbench deployment](blockchain-workbench-deploy.md) for details on deployment.</span></span>
* <span data-ttu-id="6c236-113">Azure Active Directory users in the tenant associated with Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="6c236-113">Azure Active Directory users in the tenant associated with Blockchain Workbench.</span></span> <span data-ttu-id="6c236-114">For more information, see [add Azure AD users in Azure Blockchain Workbench](blockchain-workbench-manage-users.md#add-azure-ad-users).</span><span class="sxs-lookup"><span data-stu-id="6c236-114">For more information, see [add Azure AD users in Azure Blockchain Workbench](blockchain-workbench-manage-users.md#add-azure-ad-users).</span></span>
* <span data-ttu-id="6c236-115">A Blockchain Workbench administrator account.</span><span class="sxs-lookup"><span data-stu-id="6c236-115">A Blockchain Workbench administrator account.</span></span> <span data-ttu-id="6c236-116">For more information, see add [Blockchain Workbench administrators in Azure Blockchain Workbench](blockchain-workbench-manage-users.md#manage-blockchain-workbench-administrators).</span><span class="sxs-lookup"><span data-stu-id="6c236-116">For more information, see add [Blockchain Workbench administrators in Azure Blockchain Workbench](blockchain-workbench-manage-users.md#manage-blockchain-workbench-administrators).</span></span>

## <a name="hello-blockchain"></a><span data-ttu-id="6c236-117">Hello, Blockchain!</span><span class="sxs-lookup"><span data-stu-id="6c236-117">Hello, Blockchain!</span></span>

<span data-ttu-id="6c236-118">Let's build a basic application in which a requestor sends a request and a responder send a response to the request.</span><span class="sxs-lookup"><span data-stu-id="6c236-118">Let's build a basic application in which a requestor sends a request and a responder send a response to the request.</span></span> <span data-ttu-id="6c236-119">For example, a request can be, "Hello, how are you?", and the response can be, "I'm great!".</span><span class="sxs-lookup"><span data-stu-id="6c236-119">For example, a request can be, "Hello, how are you?", and the response can be, "I'm great!".</span></span> <span data-ttu-id="6c236-120">Both the request and the response are recorded on the underlying blockchain.</span><span class="sxs-lookup"><span data-stu-id="6c236-120">Both the request and the response are recorded on the underlying blockchain.</span></span> 

<span data-ttu-id="6c236-121">Follow the steps to create the application files or you can [download the sample from GitHub](https://github.com/Azure-Samples/blockchain/tree/master/blockchain-workbench/application-and-smart-contract-samples/hello-blockchain).</span><span class="sxs-lookup"><span data-stu-id="6c236-121">Follow the steps to create the application files or you can [download the sample from GitHub](https://github.com/Azure-Samples/blockchain/tree/master/blockchain-workbench/application-and-smart-contract-samples/hello-blockchain).</span></span> 

## <a name="configuration-file"></a><span data-ttu-id="6c236-122">Configuration file</span><span class="sxs-lookup"><span data-stu-id="6c236-122">Configuration file</span></span>

<span data-ttu-id="6c236-123">Configuration metadata defines the high-level workflows and interaction model of the blockchain application.</span><span class="sxs-lookup"><span data-stu-id="6c236-123">Configuration metadata defines the high-level workflows and interaction model of the blockchain application.</span></span> <span data-ttu-id="6c236-124">Configuration metadata represents the workflow stages and interaction model of the blockchain application.</span><span class="sxs-lookup"><span data-stu-id="6c236-124">Configuration metadata represents the workflow stages and interaction model of the blockchain application.</span></span>

1. <span data-ttu-id="6c236-125">In your favorite editor, create a file named `HelloBlockchain.json`.</span><span class="sxs-lookup"><span data-stu-id="6c236-125">In your favorite editor, create a file named `HelloBlockchain.json`.</span></span>
2. <span data-ttu-id="6c236-126">Add the following JSON to define the configuration of the blockchain application.</span><span class="sxs-lookup"><span data-stu-id="6c236-126">Add the following JSON to define the configuration of the blockchain application.</span></span>

    ``` json
    {
      "ApplicationName": "HelloBlockchain",
      "DisplayName": "Hello, Blockchain!",
      "Description": "A simple application to send request and get response",
      "ApplicationRoles": [
        {
          "Name": "Requestor",
          "Description": "A person sending a request."
        },
        {
          "Name": "Responder",
          "Description": "A person responding to a request"
        }
      ],
      "Workflows": [
        {
          "Name": "HelloBlockchain",
          "DisplayName": "Request Response",
          "Description": "A simple workflow to send a request and receive a response.",
          "Initiators": [ "Requestor" ],
          "StartState": "Request",
          "Properties": [
            {
              "Name": "State",
              "DisplayName": "State",
              "Description": "Holds the state of the contract.",
              "Type": {
                "Name": "state"
              }
            },
            {
              "Name": "Requestor",
              "DisplayName": "Requestor",
              "Description": "A person sending a request.",
              "Type": {
                "Name": "Requestor"
              }
            },
            {
              "Name": "Responder",
              "DisplayName": "Responder",
              "Description": "A person sending a response.",
              "Type": {
                "Name": "Responder"
              }
            },
            {
              "Name": "RequestMessage",
              "DisplayName": "Request Message",
              "Description": "A request message.",
              "Type": {
                "Name": "string"
              }
            },
            {
              "Name": "ResponseMessage",
              "DisplayName": "Response Message",
              "Description": "A response message.",
              "Type": {
                "Name": "string"
              }
            }
          ],
          "Constructor": {
            "Parameters": [
              {
                "Name": "message",
                "Description": "...",
                "DisplayName": "Request Message",
                "Type": {
                  "Name": "string"
                }
              }
            ]
          },
          "Functions": [
            {
              "Name": "SendRequest",
              "DisplayName": "Request",
              "Description": "...",
              "Parameters": [
                {
                  "Name": "requestMessage",
                  "Description": "...",
                  "DisplayName": "Request Message",
                  "Type": {
                    "Name": "string"
                  }
                }
              ]
            },
            {
              "Name": "SendResponse",
              "DisplayName": "Response",
              "Description": "...",
              "Parameters": [
                {
                  "Name": "responseMessage",
                  "Description": "...",
                  "DisplayName": "Response Message",
                  "Type": {
                    "Name": "string"
                  }
                }
              ]
            }
          ],
          "States": [
            {
              "Name": "Request",
              "DisplayName": "Request",
              "Description": "...",
              "PercentComplete": 50,
              "Value": 0,
              "Style": "Success",
              "Transitions": [
                {
                  "AllowedRoles": ["Responder"],
                  "AllowedInstanceRoles": [],
                  "Description": "...",
                  "Function": "SendResponse",
                  "NextStates": [ "Respond" ],
                  "DisplayName": "Send Response"
                }
              ]
            },
            {
              "Name": "Respond",
              "DisplayName": "Respond",
              "Description": "...",
              "PercentComplete": 90,
              "Value": 1,
              "Style": "Success",
              "Transitions": [
                {
                  "AllowedRoles": [],
                  "AllowedInstanceRoles": ["Requestor"],
                  "Description": "...",
                  "Function": "SendRequest",
                  "NextStates": [ "Request" ],
                  "DisplayName": "Send Request"
                }
              ]
            }
          ]
        }
      ]
    }
    ```

3. <span data-ttu-id="6c236-127">Save the `HelloBlockchain.json` file.</span><span class="sxs-lookup"><span data-stu-id="6c236-127">Save the `HelloBlockchain.json` file.</span></span>

<span data-ttu-id="6c236-128">The configuration file has several sections.</span><span class="sxs-lookup"><span data-stu-id="6c236-128">The configuration file has several sections.</span></span> <span data-ttu-id="6c236-129">Details about each section are as follows:</span><span class="sxs-lookup"><span data-stu-id="6c236-129">Details about each section are as follows:</span></span>

### <a name="application-metadata"></a><span data-ttu-id="6c236-130">Application metadata</span><span class="sxs-lookup"><span data-stu-id="6c236-130">Application metadata</span></span>

<span data-ttu-id="6c236-131">The beginning of the configuration file contains information about the application including application name and description.</span><span class="sxs-lookup"><span data-stu-id="6c236-131">The beginning of the configuration file contains information about the application including application name and description.</span></span>

### <a name="application-roles"></a><span data-ttu-id="6c236-132">Application roles</span><span class="sxs-lookup"><span data-stu-id="6c236-132">Application roles</span></span>

<span data-ttu-id="6c236-133">The application roles section defines the user roles who can act or participate within the blockchain application.</span><span class="sxs-lookup"><span data-stu-id="6c236-133">The application roles section defines the user roles who can act or participate within the blockchain application.</span></span> <span data-ttu-id="6c236-134">You define a set of distinct roles based on functionality.</span><span class="sxs-lookup"><span data-stu-id="6c236-134">You define a set of distinct roles based on functionality.</span></span> <span data-ttu-id="6c236-135">In the request-response scenario, there is a distinction between the functionality of a requestor as an entity that produces requests and a responder as an entity that produces responses.</span><span class="sxs-lookup"><span data-stu-id="6c236-135">In the request-response scenario, there is a distinction between the functionality of a requestor as an entity that produces requests and a responder as an entity that produces responses.</span></span>

### <a name="workflows"></a><span data-ttu-id="6c236-136">Workflows</span><span class="sxs-lookup"><span data-stu-id="6c236-136">Workflows</span></span>

<span data-ttu-id="6c236-137">Workflows define one or more stages and actions of the contract.</span><span class="sxs-lookup"><span data-stu-id="6c236-137">Workflows define one or more stages and actions of the contract.</span></span> <span data-ttu-id="6c236-138">In the request-response scenario, the first stage (state) of the workflow is a requestor (role) takes an action (transition) to send a request (function).</span><span class="sxs-lookup"><span data-stu-id="6c236-138">In the request-response scenario, the first stage (state) of the workflow is a requestor (role) takes an action (transition) to send a request (function).</span></span> <span data-ttu-id="6c236-139">The next stage (state) is a responder (role) takes an action (transition) to send a response (function).</span><span class="sxs-lookup"><span data-stu-id="6c236-139">The next stage (state) is a responder (role) takes an action (transition) to send a response (function).</span></span> <span data-ttu-id="6c236-140">An application's workflow can involve properties, functions, and states required describe the flow of a contract.</span><span class="sxs-lookup"><span data-stu-id="6c236-140">An application's workflow can involve properties, functions, and states required describe the flow of a contract.</span></span> 

<span data-ttu-id="6c236-141">For more information about the contents of configuration files, see [Azure Blockchain Workflow configuration reference](blockchain-workbench-configuration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c236-141">For more information about the contents of configuration files, see [Azure Blockchain Workflow configuration reference](blockchain-workbench-configuration-overview.md).</span></span>

## <a name="smart-contract-code-file"></a><span data-ttu-id="6c236-142">Smart contract code file</span><span class="sxs-lookup"><span data-stu-id="6c236-142">Smart contract code file</span></span>

<span data-ttu-id="6c236-143">Smart contracts represent the business logic of the blockchain application.</span><span class="sxs-lookup"><span data-stu-id="6c236-143">Smart contracts represent the business logic of the blockchain application.</span></span> <span data-ttu-id="6c236-144">Currently, Blockchain Workbench supports Ethereum for the blockchain ledger.</span><span class="sxs-lookup"><span data-stu-id="6c236-144">Currently, Blockchain Workbench supports Ethereum for the blockchain ledger.</span></span> <span data-ttu-id="6c236-145">Ethereum uses [Solidity](https://solidity.readthedocs.io) as its programming language for writing self-enforcing business logic for smart contracts.</span><span class="sxs-lookup"><span data-stu-id="6c236-145">Ethereum uses [Solidity](https://solidity.readthedocs.io) as its programming language for writing self-enforcing business logic for smart contracts.</span></span>

<span data-ttu-id="6c236-146">Smart contracts in Solidity are similar to classes in object-oriented languages.</span><span class="sxs-lookup"><span data-stu-id="6c236-146">Smart contracts in Solidity are similar to classes in object-oriented languages.</span></span> <span data-ttu-id="6c236-147">Each contract contains state and functions to implement stages and actions of the smart contract.</span><span class="sxs-lookup"><span data-stu-id="6c236-147">Each contract contains state and functions to implement stages and actions of the smart contract.</span></span>

<span data-ttu-id="6c236-148">In your favorite editor, create a file called `HelloBlockchain.sol`.</span><span class="sxs-lookup"><span data-stu-id="6c236-148">In your favorite editor, create a file called `HelloBlockchain.sol`.</span></span>

### <a name="version-pragma"></a><span data-ttu-id="6c236-149">Version pragma</span><span class="sxs-lookup"><span data-stu-id="6c236-149">Version pragma</span></span>

<span data-ttu-id="6c236-150">As a best practice, indicate the version of Solidity you are targeting.</span><span class="sxs-lookup"><span data-stu-id="6c236-150">As a best practice, indicate the version of Solidity you are targeting.</span></span> <span data-ttu-id="6c236-151">Specifying the version helps avoid incompatibilities with future Solidity versions.</span><span class="sxs-lookup"><span data-stu-id="6c236-151">Specifying the version helps avoid incompatibilities with future Solidity versions.</span></span> 

<span data-ttu-id="6c236-152">Add the following version pragma at the top of `HelloBlockchain.sol` smart contract code file.</span><span class="sxs-lookup"><span data-stu-id="6c236-152">Add the following version pragma at the top of `HelloBlockchain.sol` smart contract code file.</span></span>


  ``` solidity
  pragma solidity ^0.4.20;
  ```

### <a name="base-class"></a><span data-ttu-id="6c236-153">Base class</span><span class="sxs-lookup"><span data-stu-id="6c236-153">Base class</span></span>

<span data-ttu-id="6c236-154">**WorkbenchBase** base class enables Blockchain Workbench to create and update the contract.</span><span class="sxs-lookup"><span data-stu-id="6c236-154">**WorkbenchBase** base class enables Blockchain Workbench to create and update the contract.</span></span> <span data-ttu-id="6c236-155">The base class is required for Blockchain Workbench specific smart contract code.</span><span class="sxs-lookup"><span data-stu-id="6c236-155">The base class is required for Blockchain Workbench specific smart contract code.</span></span> <span data-ttu-id="6c236-156">Your contract needs to inherit from the **WorkbenchBase** base class.</span><span class="sxs-lookup"><span data-stu-id="6c236-156">Your contract needs to inherit from the **WorkbenchBase** base class.</span></span>

<span data-ttu-id="6c236-157">In `HelloBlockchain.sol` smart contract code file, add the **WorkbenchBase** class at the beginning of the file.</span><span class="sxs-lookup"><span data-stu-id="6c236-157">In `HelloBlockchain.sol` smart contract code file, add the **WorkbenchBase** class at the beginning of the file.</span></span> 

```
contract WorkbenchBase {
    event WorkbenchContractCreated(string applicationName, string workflowName, address originatingAddress);
    event WorkbenchContractUpdated(string applicationName, string workflowName, string action, address originatingAddress);

    string internal ApplicationName;
    string internal WorkflowName;

    function WorkbenchBase(string applicationName, string workflowName) internal {
        ApplicationName = applicationName;
        WorkflowName = workflowName;
    }

    function ContractCreated() internal {
        WorkbenchContractCreated(ApplicationName, WorkflowName, msg.sender);
    }

    function ContractUpdated(string action) internal {
        WorkbenchContractUpdated(ApplicationName, WorkflowName, action, msg.sender);
    }
}
```
<span data-ttu-id="6c236-158">The base class includes two important functions:</span><span class="sxs-lookup"><span data-stu-id="6c236-158">The base class includes two important functions:</span></span>

|<span data-ttu-id="6c236-159">Base class function</span><span class="sxs-lookup"><span data-stu-id="6c236-159">Base class function</span></span>  | <span data-ttu-id="6c236-160">Purpose</span><span class="sxs-lookup"><span data-stu-id="6c236-160">Purpose</span></span>  | <span data-ttu-id="6c236-161">When to call</span><span class="sxs-lookup"><span data-stu-id="6c236-161">When to call</span></span>  |
|---------|---------|---------|
| <span data-ttu-id="6c236-162">ContractCreated()</span><span class="sxs-lookup"><span data-stu-id="6c236-162">ContractCreated()</span></span> | <span data-ttu-id="6c236-163">Notifies Blockchain Workbench a contract has been created</span><span class="sxs-lookup"><span data-stu-id="6c236-163">Notifies Blockchain Workbench a contract has been created</span></span> | <span data-ttu-id="6c236-164">Before exiting the contract constructor</span><span class="sxs-lookup"><span data-stu-id="6c236-164">Before exiting the contract constructor</span></span> |
| <span data-ttu-id="6c236-165">ContractUpdated()</span><span class="sxs-lookup"><span data-stu-id="6c236-165">ContractUpdated()</span></span> | <span data-ttu-id="6c236-166">Notifies Blockchain Workbench a contract state has been updated</span><span class="sxs-lookup"><span data-stu-id="6c236-166">Notifies Blockchain Workbench a contract state has been updated</span></span> | <span data-ttu-id="6c236-167">Before exiting a contract function</span><span class="sxs-lookup"><span data-stu-id="6c236-167">Before exiting a contract function</span></span> |

### <a name="configuration-and-smart-contract-code-relationship"></a><span data-ttu-id="6c236-168">Configuration and smart contract code relationship</span><span class="sxs-lookup"><span data-stu-id="6c236-168">Configuration and smart contract code relationship</span></span>

<span data-ttu-id="6c236-169">Blockchain Workbench uses the configuration file and smart contract code file to create a blockchain application.</span><span class="sxs-lookup"><span data-stu-id="6c236-169">Blockchain Workbench uses the configuration file and smart contract code file to create a blockchain application.</span></span> <span data-ttu-id="6c236-170">There is a relationship between what is defined in the configuration and the code in the smart contract.</span><span class="sxs-lookup"><span data-stu-id="6c236-170">There is a relationship between what is defined in the configuration and the code in the smart contract.</span></span> <span data-ttu-id="6c236-171">Contract details, functions, parameters, and types are required to match to create the application.</span><span class="sxs-lookup"><span data-stu-id="6c236-171">Contract details, functions, parameters, and types are required to match to create the application.</span></span> <span data-ttu-id="6c236-172">Blockchain Workbench verifies the files prior to application creation.</span><span class="sxs-lookup"><span data-stu-id="6c236-172">Blockchain Workbench verifies the files prior to application creation.</span></span> 

### <a name="contract"></a><span data-ttu-id="6c236-173">Contract</span><span class="sxs-lookup"><span data-stu-id="6c236-173">Contract</span></span>

<span data-ttu-id="6c236-174">For Blockchain Workbench, contracts need to inherit from the **WorkbenchBase** base class.</span><span class="sxs-lookup"><span data-stu-id="6c236-174">For Blockchain Workbench, contracts need to inherit from the **WorkbenchBase** base class.</span></span> <span data-ttu-id="6c236-175">When declaring the contract, you need to pass the application name and the workflow name as arguments.</span><span class="sxs-lookup"><span data-stu-id="6c236-175">When declaring the contract, you need to pass the application name and the workflow name as arguments.</span></span>

<span data-ttu-id="6c236-176">Add the **contract** header to your `HelloBlockchain.sol` smart contract code file.</span><span class="sxs-lookup"><span data-stu-id="6c236-176">Add the **contract** header to your `HelloBlockchain.sol` smart contract code file.</span></span> 

```
contract HelloBlockchain is WorkbenchBase('HelloBlockchain', 'HelloBlockchain') {
```

<span data-ttu-id="6c236-177">Your contract needs to inherit from the **WorkbenchBase** base class and pass in the parameters **ApplicationName**  and the workflow **Name** as defined in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="6c236-177">Your contract needs to inherit from the **WorkbenchBase** base class and pass in the parameters **ApplicationName**  and the workflow **Name** as defined in the configuration file.</span></span> <span data-ttu-id="6c236-178">In this case, the application name and workflow name are the same.</span><span class="sxs-lookup"><span data-stu-id="6c236-178">In this case, the application name and workflow name are the same.</span></span>

### <a name="state-variables"></a><span data-ttu-id="6c236-179">State variables</span><span class="sxs-lookup"><span data-stu-id="6c236-179">State variables</span></span>

<span data-ttu-id="6c236-180">State variables store values of the state for each contract instance.</span><span class="sxs-lookup"><span data-stu-id="6c236-180">State variables store values of the state for each contract instance.</span></span> <span data-ttu-id="6c236-181">The state variables in your contract must match the workflow properties defined in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="6c236-181">The state variables in your contract must match the workflow properties defined in the configuration file.</span></span>

<span data-ttu-id="6c236-182">Add the state variables to your contract in your `HelloBlockchain.sol` smart contract code file.</span><span class="sxs-lookup"><span data-stu-id="6c236-182">Add the state variables to your contract in your `HelloBlockchain.sol` smart contract code file.</span></span> 

```
    //Set of States
    enum StateType { Request, Respond}
    
    //List of properties
    StateType public  State;
    address public  Requestor;
    address public  Responder;
    
    string public RequestMessage;
    string public ResponseMessage;
```

### <a name="constructor"></a><span data-ttu-id="6c236-183">Constructor</span><span class="sxs-lookup"><span data-stu-id="6c236-183">Constructor</span></span>

<span data-ttu-id="6c236-184">The constructor defines input parameters for a new smart contract instance of a workflow.</span><span class="sxs-lookup"><span data-stu-id="6c236-184">The constructor defines input parameters for a new smart contract instance of a workflow.</span></span> <span data-ttu-id="6c236-185">The constructor is declared as a function with the same name as the contract.</span><span class="sxs-lookup"><span data-stu-id="6c236-185">The constructor is declared as a function with the same name as the contract.</span></span> <span data-ttu-id="6c236-186">Required parameters for the constructor are defined as constructor parameters in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="6c236-186">Required parameters for the constructor are defined as constructor parameters in the configuration file.</span></span> <span data-ttu-id="6c236-187">The number, order, and type of parameters must match in both files.</span><span class="sxs-lookup"><span data-stu-id="6c236-187">The number, order, and type of parameters must match in both files.</span></span>

<span data-ttu-id="6c236-188">In the constructor function, write any business logic you want to perform prior to creating the contract.</span><span class="sxs-lookup"><span data-stu-id="6c236-188">In the constructor function, write any business logic you want to perform prior to creating the contract.</span></span> <span data-ttu-id="6c236-189">For example, initialize the state variables with starting values.</span><span class="sxs-lookup"><span data-stu-id="6c236-189">For example, initialize the state variables with starting values.</span></span>

<span data-ttu-id="6c236-190">Before exiting the constructor function, call the `ContractCreated()` function.</span><span class="sxs-lookup"><span data-stu-id="6c236-190">Before exiting the constructor function, call the `ContractCreated()` function.</span></span> <span data-ttu-id="6c236-191">This function notifies Blockchain Workbench a contract has been created.</span><span class="sxs-lookup"><span data-stu-id="6c236-191">This function notifies Blockchain Workbench a contract has been created.</span></span>

<span data-ttu-id="6c236-192">Add the constructor function to your contract in your `HelloBlockchain.sol` smart contract code file.</span><span class="sxs-lookup"><span data-stu-id="6c236-192">Add the constructor function to your contract in your `HelloBlockchain.sol` smart contract code file.</span></span> 

```
    // constructor function
    function HelloBlockchain(string message) public
    {
        Requestor = msg.sender;
        RequestMessage = message;
        State = StateType.Request;
    
        // call ContractCreated() to create an instance of this workflow
        ContractCreated();
    }
```

### <a name="functions"></a><span data-ttu-id="6c236-193">Functions</span><span class="sxs-lookup"><span data-stu-id="6c236-193">Functions</span></span>

<span data-ttu-id="6c236-194">Functions are the executable units of business logic within a contract.</span><span class="sxs-lookup"><span data-stu-id="6c236-194">Functions are the executable units of business logic within a contract.</span></span> <span data-ttu-id="6c236-195">Required parameters for the function are defined as function parameters in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="6c236-195">Required parameters for the function are defined as function parameters in the configuration file.</span></span> <span data-ttu-id="6c236-196">The number, order, and type of parameters must match in both files.</span><span class="sxs-lookup"><span data-stu-id="6c236-196">The number, order, and type of parameters must match in both files.</span></span> <span data-ttu-id="6c236-197">Functions are associated to transitions in a Blockchain Workbench workflow in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="6c236-197">Functions are associated to transitions in a Blockchain Workbench workflow in the configuration file.</span></span> <span data-ttu-id="6c236-198">A transition is an action performed to move to the next stage of an application's workflow as determined by the contract.</span><span class="sxs-lookup"><span data-stu-id="6c236-198">A transition is an action performed to move to the next stage of an application's workflow as determined by the contract.</span></span>

<span data-ttu-id="6c236-199">Write any business logic you want to perform in the function.</span><span class="sxs-lookup"><span data-stu-id="6c236-199">Write any business logic you want to perform in the function.</span></span> <span data-ttu-id="6c236-200">For example, modifying a state variable's value.</span><span class="sxs-lookup"><span data-stu-id="6c236-200">For example, modifying a state variable's value.</span></span>

<span data-ttu-id="6c236-201">Before exiting the function, call the `ContractUpdated()` function.</span><span class="sxs-lookup"><span data-stu-id="6c236-201">Before exiting the function, call the `ContractUpdated()` function.</span></span> <span data-ttu-id="6c236-202">The function notifies Blockchain Workbench contract state has been updated.</span><span class="sxs-lookup"><span data-stu-id="6c236-202">The function notifies Blockchain Workbench contract state has been updated.</span></span> <span data-ttu-id="6c236-203">If you want to undo state changes made in the function, call revert().</span><span class="sxs-lookup"><span data-stu-id="6c236-203">If you want to undo state changes made in the function, call revert().</span></span> <span data-ttu-id="6c236-204">Revert discards state changes made since the last call to ContractUpdated().</span><span class="sxs-lookup"><span data-stu-id="6c236-204">Revert discards state changes made since the last call to ContractUpdated().</span></span>

1. <span data-ttu-id="6c236-205">Add the following functions to your contract in your `HelloBlockchain.sol` smart contract code file.</span><span class="sxs-lookup"><span data-stu-id="6c236-205">Add the following functions to your contract in your `HelloBlockchain.sol` smart contract code file.</span></span> 

    ```
        // call this function to send a request
        function SendRequest(string requestMessage) public
        {
            if (Requestor != msg.sender)
            {
                revert();
            }
    
            RequestMessage = requestMessage;
            State = StateType.Request;
    
            // call ContractUpdated() to record this action
            ContractUpdated('SendRequest');
        }
    
        // call this function to send a response
        function SendResponse(string responseMessage) public
        {
            Responder = msg.sender;
    
            // call ContractUpdated() to record this action
            ResponseMessage = responseMessage;
            State = StateType.Respond;
            ContractUpdated('SendResponse');
        }
    }
    ```

2. <span data-ttu-id="6c236-206">Save your `HelloBlockchain.sol` smart contract code file.</span><span class="sxs-lookup"><span data-stu-id="6c236-206">Save your `HelloBlockchain.sol` smart contract code file.</span></span>

## <a name="add-blockchain-application-to-blockchain-workbench"></a><span data-ttu-id="6c236-207">Add blockchain application to Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="6c236-207">Add blockchain application to Blockchain Workbench</span></span>

<span data-ttu-id="6c236-208">To add a blockchain application to Blockchain Workbench, you upload the configuration and smart contract files to define the application.</span><span class="sxs-lookup"><span data-stu-id="6c236-208">To add a blockchain application to Blockchain Workbench, you upload the configuration and smart contract files to define the application.</span></span>

1. <span data-ttu-id="6c236-209">In a web browser, navigate to the Blockchain Workbench web address.</span><span class="sxs-lookup"><span data-stu-id="6c236-209">In a web browser, navigate to the Blockchain Workbench web address.</span></span> <span data-ttu-id="6c236-210">For example, `https://{workbench URL}.azurewebsites.net/` The web application is created when you deploy Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="6c236-210">For example, `https://{workbench URL}.azurewebsites.net/` The web application is created when you deploy Blockchain Workbench.</span></span> <span data-ttu-id="6c236-211">For information on how to find your Blockchain Workbench web address, see [Blockchain Workbench Web URL](blockchain-workbench-deploy.md#blockchain-workbench-web-url)</span><span class="sxs-lookup"><span data-stu-id="6c236-211">For information on how to find your Blockchain Workbench web address, see [Blockchain Workbench Web URL](blockchain-workbench-deploy.md#blockchain-workbench-web-url)</span></span>
2. <span data-ttu-id="6c236-212">Sign in as a [Blockchain Workbench administrator](blockchain-workbench-manage-users.md#manage-blockchain-workbench-administrators).</span><span class="sxs-lookup"><span data-stu-id="6c236-212">Sign in as a [Blockchain Workbench administrator](blockchain-workbench-manage-users.md#manage-blockchain-workbench-administrators).</span></span>
3. <span data-ttu-id="6c236-213">Select **Applications** > **New**.</span><span class="sxs-lookup"><span data-stu-id="6c236-213">Select **Applications** > **New**.</span></span> <span data-ttu-id="6c236-214">The **New application** pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="6c236-214">The **New application** pane is displayed.</span></span>
4. <span data-ttu-id="6c236-215">Select **Upload the contract configuration** > **Browse** to locate the **HelloBlockchain.json** configuration file you created.</span><span class="sxs-lookup"><span data-stu-id="6c236-215">Select **Upload the contract configuration** > **Browse** to locate the **HelloBlockchain.json** configuration file you created.</span></span> <span data-ttu-id="6c236-216">The configuration file is automatically validated.</span><span class="sxs-lookup"><span data-stu-id="6c236-216">The configuration file is automatically validated.</span></span> <span data-ttu-id="6c236-217">Select the **Show** link to display validation errors.</span><span class="sxs-lookup"><span data-stu-id="6c236-217">Select the **Show** link to display validation errors.</span></span> <span data-ttu-id="6c236-218">Fix validation errors before you deploy the application.</span><span class="sxs-lookup"><span data-stu-id="6c236-218">Fix validation errors before you deploy the application.</span></span>
5. <span data-ttu-id="6c236-219">Select **Upload the contract code** > **Browse** to locate the **HelloBlockchain.sol** smart contract code file.</span><span class="sxs-lookup"><span data-stu-id="6c236-219">Select **Upload the contract code** > **Browse** to locate the **HelloBlockchain.sol** smart contract code file.</span></span> <span data-ttu-id="6c236-220">The code file is automatically validated.</span><span class="sxs-lookup"><span data-stu-id="6c236-220">The code file is automatically validated.</span></span> <span data-ttu-id="6c236-221">Select the **Show** link to display validation errors.</span><span class="sxs-lookup"><span data-stu-id="6c236-221">Select the **Show** link to display validation errors.</span></span> <span data-ttu-id="6c236-222">Fix validation errors before you deploy the application.</span><span class="sxs-lookup"><span data-stu-id="6c236-222">Fix validation errors before you deploy the application.</span></span>
6. <span data-ttu-id="6c236-223">Select **Deploy** to create the blockchain application based on the configuration and smart contract files.</span><span class="sxs-lookup"><span data-stu-id="6c236-223">Select **Deploy** to create the blockchain application based on the configuration and smart contract files.</span></span>

<span data-ttu-id="6c236-224">Deployment of the blockchain application takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="6c236-224">Deployment of the blockchain application takes a few minutes.</span></span> <span data-ttu-id="6c236-225">When deployment is finished, the new application is displayed in **Applications**.</span><span class="sxs-lookup"><span data-stu-id="6c236-225">When deployment is finished, the new application is displayed in **Applications**.</span></span> 

> [!NOTE]
> <span data-ttu-id="6c236-226">You can also create blockchain applications by using the [Azure Blockchain Workbench REST API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench).</span><span class="sxs-lookup"><span data-stu-id="6c236-226">You can also create blockchain applications by using the [Azure Blockchain Workbench REST API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench).</span></span> 

## <a name="add-blockchain-application-members"></a><span data-ttu-id="6c236-227">Add blockchain application members</span><span class="sxs-lookup"><span data-stu-id="6c236-227">Add blockchain application members</span></span>

<span data-ttu-id="6c236-228">Add application members to your application to initiate and take actions on contracts.</span><span class="sxs-lookup"><span data-stu-id="6c236-228">Add application members to your application to initiate and take actions on contracts.</span></span> <span data-ttu-id="6c236-229">To add application members, you need to be a [Blockchain Workbench administrator](blockchain-workbench-manage-users.md#manage-blockchain-workbench-administrators).</span><span class="sxs-lookup"><span data-stu-id="6c236-229">To add application members, you need to be a [Blockchain Workbench administrator](blockchain-workbench-manage-users.md#manage-blockchain-workbench-administrators).</span></span>

1. <span data-ttu-id="6c236-230">Select **Applications** > **Hello, Blockchain!**.</span><span class="sxs-lookup"><span data-stu-id="6c236-230">Select **Applications** > **Hello, Blockchain!**.</span></span>
2. <span data-ttu-id="6c236-231">The number of members associated to the application is displayed in the upper right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="6c236-231">The number of members associated to the application is displayed in the upper right corner of the page.</span></span> <span data-ttu-id="6c236-232">For a new application, the number of members will be zero.</span><span class="sxs-lookup"><span data-stu-id="6c236-232">For a new application, the number of members will be zero.</span></span>
3. <span data-ttu-id="6c236-233">Select the **members** link in the upper right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="6c236-233">Select the **members** link in the upper right corner of the page.</span></span> <span data-ttu-id="6c236-234">A current list of members for the application is displayed.</span><span class="sxs-lookup"><span data-stu-id="6c236-234">A current list of members for the application is displayed.</span></span>
4. <span data-ttu-id="6c236-235">In the membership list, select **Add members**.</span><span class="sxs-lookup"><span data-stu-id="6c236-235">In the membership list, select **Add members**.</span></span>
5. <span data-ttu-id="6c236-236">Select or enter the member's name you want to add.</span><span class="sxs-lookup"><span data-stu-id="6c236-236">Select or enter the member's name you want to add.</span></span> <span data-ttu-id="6c236-237">Only Azure AD users that exist in the Blockchain Workbench tenant are listed.</span><span class="sxs-lookup"><span data-stu-id="6c236-237">Only Azure AD users that exist in the Blockchain Workbench tenant are listed.</span></span> <span data-ttu-id="6c236-238">If the user is not found, you need to [add Azure AD users](blockchain-workbench-manage-users.md#add-azure-ad-users).</span><span class="sxs-lookup"><span data-stu-id="6c236-238">If the user is not found, you need to [add Azure AD users](blockchain-workbench-manage-users.md#add-azure-ad-users).</span></span>
6. <span data-ttu-id="6c236-239">Select the **Role** for the member.</span><span class="sxs-lookup"><span data-stu-id="6c236-239">Select the **Role** for the member.</span></span> <span data-ttu-id="6c236-240">For the first member, select **Requestor** as the role.</span><span class="sxs-lookup"><span data-stu-id="6c236-240">For the first member, select **Requestor** as the role.</span></span>
7. <span data-ttu-id="6c236-241">Select **Add** to add the member with the associated role to the application.</span><span class="sxs-lookup"><span data-stu-id="6c236-241">Select **Add** to add the member with the associated role to the application.</span></span>
8. <span data-ttu-id="6c236-242">Add another member to the application with the **Responder** role.</span><span class="sxs-lookup"><span data-stu-id="6c236-242">Add another member to the application with the **Responder** role.</span></span>

<span data-ttu-id="6c236-243">For more information about managing users in Blockchain Workbench, see [managing users in Azure Blockchain Workbench](blockchain-workbench-manage-users.md)</span><span class="sxs-lookup"><span data-stu-id="6c236-243">For more information about managing users in Blockchain Workbench, see [managing users in Azure Blockchain Workbench](blockchain-workbench-manage-users.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c236-244">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c236-244">Next steps</span></span>

<span data-ttu-id="6c236-245">In this how-to article, you've created a basic request and response application.</span><span class="sxs-lookup"><span data-stu-id="6c236-245">In this how-to article, you've created a basic request and response application.</span></span> <span data-ttu-id="6c236-246">To learn how to use the application, continue to the next how-to article.</span><span class="sxs-lookup"><span data-stu-id="6c236-246">To learn how to use the application, continue to the next how-to article.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6c236-247">Using a blockchain application</span><span class="sxs-lookup"><span data-stu-id="6c236-247">Using a blockchain application</span></span>](blockchain-workbench-use.md)
