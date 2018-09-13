---
title: Using Azure Blockchain Workbench REST API
description: Scenarios for how to use the Azure Blockchain Workbench REST API
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/16/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: zeyadr
manager: femila
ms.openlocfilehash: 63e87c59a2e560b5a78708482c2ed89f5f8fb127
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869340"
---
# <a name="using-the-azure-blockchain-workbench-rest-api"></a><span data-ttu-id="83739-103">Using the Azure Blockchain Workbench REST API</span><span class="sxs-lookup"><span data-stu-id="83739-103">Using the Azure Blockchain Workbench REST API</span></span> 

<span data-ttu-id="83739-104">Azure Blockchain Workbench REST API provides developers and information workers a way to build rich integrations to blockchain applications.</span><span class="sxs-lookup"><span data-stu-id="83739-104">Azure Blockchain Workbench REST API provides developers and information workers a way to build rich integrations to blockchain applications.</span></span> <span data-ttu-id="83739-105">This document walks you through several key methods of the Workbench REST API.</span><span class="sxs-lookup"><span data-stu-id="83739-105">This document walks you through several key methods of the Workbench REST API.</span></span> <span data-ttu-id="83739-106">Consider a scenario where a developer wants to create a custom blockchain client, which allows signed in users to view and interact with their assigned blockchain applications.</span><span class="sxs-lookup"><span data-stu-id="83739-106">Consider a scenario where a developer wants to create a custom blockchain client, which allows signed in users to view and interact with their assigned blockchain applications.</span></span> <span data-ttu-id="83739-107">The client allows users to view contract instances and take actions on smart contracts.</span><span class="sxs-lookup"><span data-stu-id="83739-107">The client allows users to view contract instances and take actions on smart contracts.</span></span> <span data-ttu-id="83739-108">The client uses the Workbench REST API in the context of the signed-in user to do the following:</span><span class="sxs-lookup"><span data-stu-id="83739-108">The client uses the Workbench REST API in the context of the signed-in user to do the following:</span></span>

* <span data-ttu-id="83739-109">List applications</span><span class="sxs-lookup"><span data-stu-id="83739-109">List applications</span></span>
* <span data-ttu-id="83739-110">List workflows for an application</span><span class="sxs-lookup"><span data-stu-id="83739-110">List workflows for an application</span></span>
* <span data-ttu-id="83739-111">List smart contract instances for a workflow</span><span class="sxs-lookup"><span data-stu-id="83739-111">List smart contract instances for a workflow</span></span>
* <span data-ttu-id="83739-112">List available actions for a contract</span><span class="sxs-lookup"><span data-stu-id="83739-112">List available actions for a contract</span></span>
* <span data-ttu-id="83739-113">Execute an action for a contract</span><span class="sxs-lookup"><span data-stu-id="83739-113">Execute an action for a contract</span></span>

<span data-ttu-id="83739-114">The example blockchain applications used in the scenarios, can be [downloaded from GitHub](https://github.com/Azure-Samples/blockchain).</span><span class="sxs-lookup"><span data-stu-id="83739-114">The example blockchain applications used in the scenarios, can be [downloaded from GitHub](https://github.com/Azure-Samples/blockchain).</span></span> 

## <a name="list-applications"></a><span data-ttu-id="83739-115">List applications</span><span class="sxs-lookup"><span data-stu-id="83739-115">List applications</span></span>

<span data-ttu-id="83739-116">Once a user has signed into the blockchain client, the first task is to retrieve all Blockchain Workbench applications for the user.</span><span class="sxs-lookup"><span data-stu-id="83739-116">Once a user has signed into the blockchain client, the first task is to retrieve all Blockchain Workbench applications for the user.</span></span> <span data-ttu-id="83739-117">In this scenario, the user has access to two applications:</span><span class="sxs-lookup"><span data-stu-id="83739-117">In this scenario, the user has access to two applications:</span></span>

1.  [<span data-ttu-id="83739-118">Asset transfer</span><span class="sxs-lookup"><span data-stu-id="83739-118">Asset transfer</span></span>](https://github.com/Azure-Samples/blockchain/blob/master/blockchain-workbench/application-and-smart-contract-samples/asset-transfer/readme.md)
2.  [<span data-ttu-id="83739-119">Refrigerated transportation</span><span class="sxs-lookup"><span data-stu-id="83739-119">Refrigerated transportation</span></span>](https://github.com/Azure-Samples/blockchain/blob/master/blockchain-workbench/application-and-smart-contract-samples/refrigerated-transportation/readme.md)

<span data-ttu-id="83739-120">Use the [Applications GET API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/applications/applicationsget):</span><span class="sxs-lookup"><span data-stu-id="83739-120">Use the [Applications GET API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/applications/applicationsget):</span></span>

``` http
GET /api/v1/applications 
Authorization : Bearer {access token}
```

<span data-ttu-id="83739-121">The response lists all blockchain applications to which a user has access in Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="83739-121">The response lists all blockchain applications to which a user has access in Blockchain Workbench.</span></span> <span data-ttu-id="83739-122">Blockchain Workbench administrators get all blockchain applications, while non-Workbench administrators get all blockchains for which they have at least one associated application role or an associated smart contract instance role.</span><span class="sxs-lookup"><span data-stu-id="83739-122">Blockchain Workbench administrators get all blockchain applications, while non-Workbench administrators get all blockchains for which they have at least one associated application role or an associated smart contract instance role.</span></span>

``` http
HTTP/1.1 200 OK
Content-type: application/json
{
    "nextLink": "/api/v1/applications?skip=2",
    "applications": [
        {
            "id": 1,
            "name": "AssetTransfer",
            "description": "Allows transfer of assets between a buyer and a seller, with appraisal/inspection functionality",
            "displayName": "Asset Transfer",
            "createdByUserId": 1,
            "createdDtTm": "2018-04-28T05:59:14.4733333",
            "enabled": true,
            "applicationRoles": null
        },
        {
            "id": 2,
            "name": "RefrigeratedTransportation",
            "description": "Application to track end-to-end transportation of perishable goods.",
            "displayName": "Refrigerated Transportation",
            "createdByUserId": 7,
            "createdDtTm": "2018-04-28T18:25:38.71",
            "enabled": true,
            "applicationRoles": null
        }
    ]
}
```

## <a name="list-workflows-for-an-application"></a><span data-ttu-id="83739-123">List workflows for an application</span><span class="sxs-lookup"><span data-stu-id="83739-123">List workflows for an application</span></span>

<span data-ttu-id="83739-124">Once a user selects the applicable blockchain application, in this case, **Asset Transfer**, the blockchain client retrieves all workflows of the specific blockchain application.</span><span class="sxs-lookup"><span data-stu-id="83739-124">Once a user selects the applicable blockchain application, in this case, **Asset Transfer**, the blockchain client retrieves all workflows of the specific blockchain application.</span></span> <span data-ttu-id="83739-125">Users can then select the applicable workflow before being shown all smart contract instances for the workflow.</span><span class="sxs-lookup"><span data-stu-id="83739-125">Users can then select the applicable workflow before being shown all smart contract instances for the workflow.</span></span> <span data-ttu-id="83739-126">Each blockchain application has one or more workflows and each workflow has zero or smart contract instances.</span><span class="sxs-lookup"><span data-stu-id="83739-126">Each blockchain application has one or more workflows and each workflow has zero or smart contract instances.</span></span> <span data-ttu-id="83739-127">When building blockchain client applications, it is recommended to skip the user experience flow allowing users to select the appropriate workflow when there is only one workflow for the blockchain application.</span><span class="sxs-lookup"><span data-stu-id="83739-127">When building blockchain client applications, it is recommended to skip the user experience flow allowing users to select the appropriate workflow when there is only one workflow for the blockchain application.</span></span> <span data-ttu-id="83739-128">In this case, **Asset Transfer** has only one workflow, also called **Asset Transfer**.</span><span class="sxs-lookup"><span data-stu-id="83739-128">In this case, **Asset Transfer** has only one workflow, also called **Asset Transfer**.</span></span>

<span data-ttu-id="83739-129">Use the [Applications Workflows GET API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/applications/workflowsget):</span><span class="sxs-lookup"><span data-stu-id="83739-129">Use the [Applications Workflows GET API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/applications/workflowsget):</span></span>

``` http
GET /api/v1/applications/{applicationId}/workflows
Authorization: Bearer {access token}
```

<span data-ttu-id="83739-130">Response lists all workflows of the specified blockchain application to which a user has access in Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="83739-130">Response lists all workflows of the specified blockchain application to which a user has access in Blockchain Workbench.</span></span> <span data-ttu-id="83739-131">Blockchain Workbench administrators get all blockchain workflows, while non-Workbench administrators get all workflows for which they have at least one associated application role or is associated with a smart contract instance role.</span><span class="sxs-lookup"><span data-stu-id="83739-131">Blockchain Workbench administrators get all blockchain workflows, while non-Workbench administrators get all workflows for which they have at least one associated application role or is associated with a smart contract instance role.</span></span>

``` http
HTTP/1.1 200 OK
Content-type: application/json
{
    "nextLink": "/api/v1/applications/1/workflows?skip=1",
    "workflows": [
        {
            "id": 1,
            "name": "AssetTransfer",
            "description": "Handles the business logic for the asset transfer scenario",
            "displayName": "Asset Transfer",
            "applicationId": 1,
            "constructorId": 1,
            "startStateId": 1
        }
    ]
}
```

## <a name="list-smart-contract-instances-for-a-workflow"></a><span data-ttu-id="83739-132">List smart contract instances for a workflow</span><span class="sxs-lookup"><span data-stu-id="83739-132">List smart contract instances for a workflow</span></span>

<span data-ttu-id="83739-133">Once a user selects the applicable workflow, this case **Asset Transfer**, the blockchain client will retrieve all smart contract instances for the specified workflow.</span><span class="sxs-lookup"><span data-stu-id="83739-133">Once a user selects the applicable workflow, this case **Asset Transfer**, the blockchain client will retrieve all smart contract instances for the specified workflow.</span></span> <span data-ttu-id="83739-134">You can use this information to show all smart contract instances for the workflow and allow users to deep dive into any of the shown smart contract instances.</span><span class="sxs-lookup"><span data-stu-id="83739-134">You can use this information to show all smart contract instances for the workflow and allow users to deep dive into any of the shown smart contract instances.</span></span> <span data-ttu-id="83739-135">In this example, consider a user would like to interact with one of the smart contract instances to take action.</span><span class="sxs-lookup"><span data-stu-id="83739-135">In this example, consider a user would like to interact with one of the smart contract instances to take action.</span></span>

<span data-ttu-id="83739-136">Use the [Contracts GET API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/contracts/contractsget):</span><span class="sxs-lookup"><span data-stu-id="83739-136">Use the [Contracts GET API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/contracts/contractsget):</span></span>

``` http
GET api/v1/contracts?workflowId={workflowId}
Authorization: Bearer {access token}
```

<span data-ttu-id="83739-137">Response lists all smart contract instances of the specified workflow.</span><span class="sxs-lookup"><span data-stu-id="83739-137">Response lists all smart contract instances of the specified workflow.</span></span> <span data-ttu-id="83739-138">Workbench administrators get all smart contract instances, while non-Workbench administrators get all smart contract instances for which they have at least one associated application role or is associated with a smart contract instance role.</span><span class="sxs-lookup"><span data-stu-id="83739-138">Workbench administrators get all smart contract instances, while non-Workbench administrators get all smart contract instances for which they have at least one associated application role or is associated with a smart contract instance role.</span></span>

``` http
HTTP/1.1 200 OK
Content-type: application/json
{
    "nextLink": "/api/v1/contracts?skip=3&workflowId=1",
    "contracts": [
        {
            "id": 1,
            "provisioningStatus": 2,
            "connectionID": 1,
            "ledgerIdentifier": "0xbcb6127be062acd37818af290c0e43479a153a1c",
            "deployedByUserId": 1,
            "workflowId": 1,
            "contractCodeId": 1,
            "contractProperties": [
                {
                    "workflowPropertyId": 1,
                    "value": "0"
                },
                {
                    "workflowPropertyId": 2,
                    "value": "My first car"
                },
                {
                    "workflowPropertyId": 3,
                    "value": "54321"
                },
                {
                    "workflowPropertyId": 4,
                    "value": "0"
                },
                {
                    "workflowPropertyId": 5,
                    "value": "0x0000000000000000000000000000000000000000"
                },
                {
                    "workflowPropertyId": 6,
                    "value": "0x0000000000000000000000000000000000000000"
                },
                {
                    "workflowPropertyId": 7,
                    "value": "0x0000000000000000000000000000000000000000"
                },
                {
                    "workflowPropertyId": 8,
                    "value": "0xd882530eb3d6395e697508287900c7679dbe02d7"
                }
            ],
            "transactions": [
                {
                    "id": 1,
                    "connectionId": 1,
                    "transactionHash": "0xf3abb829884dc396e03ae9e115a770b230fcf41bb03d39457201449e077080f4",
                    "blockID": 241,
                    "from": "0xd882530eb3d6395e697508287900c7679dbe02d7",
                    "to": null,
                    "value": 0,
                    "isAppBuilderTx": true
                }
            ],
            "contractActions": [
                {
                    "id": 1,
                    "userId": 1,
                    "provisioningStatus": 2,
                    "timestamp": "2018-04-29T23:41:14.9333333",
                    "parameters": [
                        {
                            "name": "Description",
                            "value": "My first car"
                        },
                        {
                            "name": "Price",
                            "value": "54321"
                        }
                    ],
                    "workflowFunctionId": 1,
                    "transactionId": 1,
                    "workflowStateId": 1
                }
            ]
        }
    ]
}
```

## <a name="list-available-actions-for-a-contract"></a><span data-ttu-id="83739-139">List available actions for a contract</span><span class="sxs-lookup"><span data-stu-id="83739-139">List available actions for a contract</span></span>

<span data-ttu-id="83739-140">Once a user has decided to deep dive into one of the contracts, the blockchain client can then show all available actions to the user given the state of the contract.</span><span class="sxs-lookup"><span data-stu-id="83739-140">Once a user has decided to deep dive into one of the contracts, the blockchain client can then show all available actions to the user given the state of the contract.</span></span> <span data-ttu-id="83739-141">In this example, the user is looking at all available actions for a new smart contract they created:</span><span class="sxs-lookup"><span data-stu-id="83739-141">In this example, the user is looking at all available actions for a new smart contract they created:</span></span>

* <span data-ttu-id="83739-142">Modify: Allows the user to modify the description and price of an asset.</span><span class="sxs-lookup"><span data-stu-id="83739-142">Modify: Allows the user to modify the description and price of an asset.</span></span>
* <span data-ttu-id="83739-143">Terminate: Allows the user to terminate the contract of the asset.</span><span class="sxs-lookup"><span data-stu-id="83739-143">Terminate: Allows the user to terminate the contract of the asset.</span></span>

<span data-ttu-id="83739-144">Use the [Contract Action GET API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/contracts/contractactionget):</span><span class="sxs-lookup"><span data-stu-id="83739-144">Use the [Contract Action GET API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/contracts/contractactionget):</span></span>

``` http
GET /api/v1/contracts/{contractId}/actions
Authorization: Bearer {access token}
```

<span data-ttu-id="83739-145">Response lists all actions to which a user can take given the current state of the specified smart contract instance.</span><span class="sxs-lookup"><span data-stu-id="83739-145">Response lists all actions to which a user can take given the current state of the specified smart contract instance.</span></span> <span data-ttu-id="83739-146">Users get all applicable actions if the user has an associated application role or is associated with a smart contract instance role for the current state of the specified smart contract instance.</span><span class="sxs-lookup"><span data-stu-id="83739-146">Users get all applicable actions if the user has an associated application role or is associated with a smart contract instance role for the current state of the specified smart contract instance.</span></span>

``` http
HTTP/1.1 200 OK
Content-type: application/json
{
    "nextLink": "/api/v1/contracts/1/actions?skip=2",
    "workflowFunctions": [
        {
            "id": 2,
            "name": "Modify",
            "description": "Modify the description/price attributes of this asset transfer instance",
            "displayName": "Modify",
            "parameters": [
                {
                    "id": 1,
                    "name": "description",
                    "description": "The new description of the asset",
                    "displayName": "Description",
                    "type": {
                        "id": 2,
                        "name": "string",
                        "elementType": null,
                        "elementTypeId": 0
                    }
                },
                {
                    "id": 2,
                    "name": "price",
                    "description": "The new price of the asset",
                    "displayName": "Price",
                    "type": {
                        "id": 3,
                        "name": "money",
                        "elementType": null,
                        "elementTypeId": 0
                    }
                }
            ],
            "workflowId": 1
        },
        {
            "id": 3,
            "name": "Terminate",
            "description": "Used to cancel this particular instance of asset transfer",
            "displayName": "Terminate",
            "parameters": [],
            "workflowId": 1
        }
    ]
}
```

## <a name="execute-an-action-for-a-contract"></a><span data-ttu-id="83739-147">Execute an action for a contract</span><span class="sxs-lookup"><span data-stu-id="83739-147">Execute an action for a contract</span></span>

<span data-ttu-id="83739-148">A user can then decide to take action for the specified smart contract instance.</span><span class="sxs-lookup"><span data-stu-id="83739-148">A user can then decide to take action for the specified smart contract instance.</span></span> <span data-ttu-id="83739-149">In this case, consider the scenario where a user would like to modify the description and price of an asset to the following:</span><span class="sxs-lookup"><span data-stu-id="83739-149">In this case, consider the scenario where a user would like to modify the description and price of an asset to the following:</span></span>

* <span data-ttu-id="83739-150">Description: "My updated car"</span><span class="sxs-lookup"><span data-stu-id="83739-150">Description: "My updated car"</span></span>
* <span data-ttu-id="83739-151">Price: 54321</span><span class="sxs-lookup"><span data-stu-id="83739-151">Price: 54321</span></span>

<span data-ttu-id="83739-152">Use the [Contract Action POST API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/contracts/contractactionpost):</span><span class="sxs-lookup"><span data-stu-id="83739-152">Use the [Contract Action POST API](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/contracts/contractactionpost):</span></span>

``` http
POST /api/v1/contracts/{contractId}/actions
Authorization: Bearer {access token}
actionInformation: {
    "workflowFunctionId": 2,
    "workflowActionParameters": [
        {
            "name": "description",
            "value": "My updated car"
        },
        {
            "name": "price",
            "value": "54321"
        }
    ]
}
```

<span data-ttu-id="83739-153">Users are only able to execute the action given the current state of the specified smart contract instance and the user's associated application role or smart contract instance role.</span><span class="sxs-lookup"><span data-stu-id="83739-153">Users are only able to execute the action given the current state of the specified smart contract instance and the user's associated application role or smart contract instance role.</span></span> <span data-ttu-id="83739-154">If the post is successful, an HTTP 200 OK response is returned with no response body.</span><span class="sxs-lookup"><span data-stu-id="83739-154">If the post is successful, an HTTP 200 OK response is returned with no response body.</span></span>

``` http
HTTP/1.1 200 OK
Content-type: application/json
```

## <a name="next-steps"></a><span data-ttu-id="83739-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="83739-155">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="83739-156">Azure Blockchain Workbench REST API reference</span><span class="sxs-lookup"><span data-stu-id="83739-156">Azure Blockchain Workbench REST API reference</span></span>](https://docs.microsoft.com/rest/api/azure-blockchain-workbench)