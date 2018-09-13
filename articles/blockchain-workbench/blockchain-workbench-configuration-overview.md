---
title: Azure Blockchain Workbench configuration reference
description: Azure Blockchain Workbench application configuration overview.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 7/12/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: zeyadr
manager: femila
ms.openlocfilehash: 60a84609c6ec8c1733f0938c69ab683f01ecb975
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870713"
---
# <a name="azure-blockchain-workbench-configuration-reference"></a><span data-ttu-id="500ec-103">Azure Blockchain Workbench configuration reference</span><span class="sxs-lookup"><span data-stu-id="500ec-103">Azure Blockchain Workbench configuration reference</span></span>

 <span data-ttu-id="500ec-104">Azure Blockchain Workbench applications are multi-party workflows defined by configuration metadata and smart contract code.</span><span class="sxs-lookup"><span data-stu-id="500ec-104">Azure Blockchain Workbench applications are multi-party workflows defined by configuration metadata and smart contract code.</span></span> <span data-ttu-id="500ec-105">Configuration metadata defines the high-level workflows and interaction model of the blockchain application.</span><span class="sxs-lookup"><span data-stu-id="500ec-105">Configuration metadata defines the high-level workflows and interaction model of the blockchain application.</span></span> <span data-ttu-id="500ec-106">Smart contracts define the business logic of the blockchain application.</span><span class="sxs-lookup"><span data-stu-id="500ec-106">Smart contracts define the business logic of the blockchain application.</span></span> <span data-ttu-id="500ec-107">Workbench uses configuration and smart contract code to generate blockchain application user experiences.</span><span class="sxs-lookup"><span data-stu-id="500ec-107">Workbench uses configuration and smart contract code to generate blockchain application user experiences.</span></span>

<span data-ttu-id="500ec-108">Configuration metadata specifies the following information for each blockchain application:</span><span class="sxs-lookup"><span data-stu-id="500ec-108">Configuration metadata specifies the following information for each blockchain application:</span></span> 

* <span data-ttu-id="500ec-109">Name and description of the blockchain application</span><span class="sxs-lookup"><span data-stu-id="500ec-109">Name and description of the blockchain application</span></span>
* <span data-ttu-id="500ec-110">Unique roles for users who can act or participate within the blockchain application</span><span class="sxs-lookup"><span data-stu-id="500ec-110">Unique roles for users who can act or participate within the blockchain application</span></span>
* <span data-ttu-id="500ec-111">One or more workflows.</span><span class="sxs-lookup"><span data-stu-id="500ec-111">One or more workflows.</span></span> <span data-ttu-id="500ec-112">Each workflow acts as a state machine to control the flow of the business logic.</span><span class="sxs-lookup"><span data-stu-id="500ec-112">Each workflow acts as a state machine to control the flow of the business logic.</span></span> <span data-ttu-id="500ec-113">Workflows can be independent or interact with one another.</span><span class="sxs-lookup"><span data-stu-id="500ec-113">Workflows can be independent or interact with one another.</span></span>

<span data-ttu-id="500ec-114">Each defined workflow specifies the following:</span><span class="sxs-lookup"><span data-stu-id="500ec-114">Each defined workflow specifies the following:</span></span>

* <span data-ttu-id="500ec-115">Name and description of the workflow</span><span class="sxs-lookup"><span data-stu-id="500ec-115">Name and description of the workflow</span></span>
* <span data-ttu-id="500ec-116">States of the workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-116">States of the workflow.</span></span>  <span data-ttu-id="500ec-117">Each state is a stage in the business logic's control flow.</span><span class="sxs-lookup"><span data-stu-id="500ec-117">Each state is a stage in the business logic's control flow.</span></span> 
* <span data-ttu-id="500ec-118">Actions to transition to the next state</span><span class="sxs-lookup"><span data-stu-id="500ec-118">Actions to transition to the next state</span></span>
* <span data-ttu-id="500ec-119">User roles permitted to initiate each action</span><span class="sxs-lookup"><span data-stu-id="500ec-119">User roles permitted to initiate each action</span></span>
* <span data-ttu-id="500ec-120">Smart contracts that represent business logic in code files</span><span class="sxs-lookup"><span data-stu-id="500ec-120">Smart contracts that represent business logic in code files</span></span>

## <a name="application"></a><span data-ttu-id="500ec-121">Application</span><span class="sxs-lookup"><span data-stu-id="500ec-121">Application</span></span>

<span data-ttu-id="500ec-122">A blockchain application contains configuration metadata, workflows, and user roles who can act or participate within the application.</span><span class="sxs-lookup"><span data-stu-id="500ec-122">A blockchain application contains configuration metadata, workflows, and user roles who can act or participate within the application.</span></span>

| <span data-ttu-id="500ec-123">Field</span><span class="sxs-lookup"><span data-stu-id="500ec-123">Field</span></span> | <span data-ttu-id="500ec-124">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-124">Description</span></span> | <span data-ttu-id="500ec-125">Required</span><span class="sxs-lookup"><span data-stu-id="500ec-125">Required</span></span> |
|-------|-------------|:--------:|
| <span data-ttu-id="500ec-126">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="500ec-126">ApplicationName</span></span> | <span data-ttu-id="500ec-127">Unique application name.</span><span class="sxs-lookup"><span data-stu-id="500ec-127">Unique application name.</span></span> <span data-ttu-id="500ec-128">The corresponding smart contract must use the same **ApplicationName** for the applicable contract class.</span><span class="sxs-lookup"><span data-stu-id="500ec-128">The corresponding smart contract must use the same **ApplicationName** for the applicable contract class.</span></span>  | <span data-ttu-id="500ec-129">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-129">Yes</span></span> |
| <span data-ttu-id="500ec-130">DisplayName</span><span class="sxs-lookup"><span data-stu-id="500ec-130">DisplayName</span></span> | <span data-ttu-id="500ec-131">Friendly display name of the application.</span><span class="sxs-lookup"><span data-stu-id="500ec-131">Friendly display name of the application.</span></span> | <span data-ttu-id="500ec-132">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-132">Yes</span></span> |
| <span data-ttu-id="500ec-133">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-133">Description</span></span> | <span data-ttu-id="500ec-134">Description of the application.</span><span class="sxs-lookup"><span data-stu-id="500ec-134">Description of the application.</span></span> | <span data-ttu-id="500ec-135">No</span><span class="sxs-lookup"><span data-stu-id="500ec-135">No</span></span> |
| <span data-ttu-id="500ec-136">ApplicationRoles</span><span class="sxs-lookup"><span data-stu-id="500ec-136">ApplicationRoles</span></span> | <span data-ttu-id="500ec-137">Collection of [ApplicationRoles](#application-roles).</span><span class="sxs-lookup"><span data-stu-id="500ec-137">Collection of [ApplicationRoles](#application-roles).</span></span> <span data-ttu-id="500ec-138">User roles who can act or participate within the application.</span><span class="sxs-lookup"><span data-stu-id="500ec-138">User roles who can act or participate within the application.</span></span>  | <span data-ttu-id="500ec-139">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-139">Yes</span></span> |
| <span data-ttu-id="500ec-140">Workflows</span><span class="sxs-lookup"><span data-stu-id="500ec-140">Workflows</span></span> | <span data-ttu-id="500ec-141">Collection of  [Workflows](#workflows).</span><span class="sxs-lookup"><span data-stu-id="500ec-141">Collection of  [Workflows](#workflows).</span></span> <span data-ttu-id="500ec-142">Each workflow acts as a state machine to control the flow of the business logic.</span><span class="sxs-lookup"><span data-stu-id="500ec-142">Each workflow acts as a state machine to control the flow of the business logic.</span></span> | <span data-ttu-id="500ec-143">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-143">Yes</span></span> |

<span data-ttu-id="500ec-144">For an example, see [configuration file example](#configuration-file-example).</span><span class="sxs-lookup"><span data-stu-id="500ec-144">For an example, see [configuration file example](#configuration-file-example).</span></span>

## <a name="workflows"></a><span data-ttu-id="500ec-145">Workflows</span><span class="sxs-lookup"><span data-stu-id="500ec-145">Workflows</span></span>

<span data-ttu-id="500ec-146">An application's business logic may be modeled as a state machine where taking an action causes the flow of the business logic to move from one state to another.</span><span class="sxs-lookup"><span data-stu-id="500ec-146">An application's business logic may be modeled as a state machine where taking an action causes the flow of the business logic to move from one state to another.</span></span> <span data-ttu-id="500ec-147">A workflow is a collection of such states and actions.</span><span class="sxs-lookup"><span data-stu-id="500ec-147">A workflow is a collection of such states and actions.</span></span> <span data-ttu-id="500ec-148">Each workflow consists of one or more smart contracts, which represent the business logic in code files.</span><span class="sxs-lookup"><span data-stu-id="500ec-148">Each workflow consists of one or more smart contracts, which represent the business logic in code files.</span></span> <span data-ttu-id="500ec-149">An executable contract is an instance of a workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-149">An executable contract is an instance of a workflow.</span></span>

| <span data-ttu-id="500ec-150">Field</span><span class="sxs-lookup"><span data-stu-id="500ec-150">Field</span></span> | <span data-ttu-id="500ec-151">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-151">Description</span></span> | <span data-ttu-id="500ec-152">Required</span><span class="sxs-lookup"><span data-stu-id="500ec-152">Required</span></span> |
|-------|-------------|:--------:|
| <span data-ttu-id="500ec-153">Name</span><span class="sxs-lookup"><span data-stu-id="500ec-153">Name</span></span> | <span data-ttu-id="500ec-154">Unique workflow name.</span><span class="sxs-lookup"><span data-stu-id="500ec-154">Unique workflow name.</span></span> <span data-ttu-id="500ec-155">The corresponding smart contract must use the same **Name** for the applicable contract class.</span><span class="sxs-lookup"><span data-stu-id="500ec-155">The corresponding smart contract must use the same **Name** for the applicable contract class.</span></span> | <span data-ttu-id="500ec-156">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-156">Yes</span></span> |
| <span data-ttu-id="500ec-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="500ec-157">DisplayName</span></span> | <span data-ttu-id="500ec-158">Friendly display name of the workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-158">Friendly display name of the workflow.</span></span> | <span data-ttu-id="500ec-159">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-159">Yes</span></span> |
| <span data-ttu-id="500ec-160">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-160">Description</span></span> | <span data-ttu-id="500ec-161">Description of the workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-161">Description of the workflow.</span></span> | <span data-ttu-id="500ec-162">No</span><span class="sxs-lookup"><span data-stu-id="500ec-162">No</span></span> |
| <span data-ttu-id="500ec-163">Initiators</span><span class="sxs-lookup"><span data-stu-id="500ec-163">Initiators</span></span> | <span data-ttu-id="500ec-164">Collection of [ApplicationRoles](#application-roles).</span><span class="sxs-lookup"><span data-stu-id="500ec-164">Collection of [ApplicationRoles](#application-roles).</span></span> <span data-ttu-id="500ec-165">Roles that are assigned to users who are authorized to create contracts in the workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-165">Roles that are assigned to users who are authorized to create contracts in the workflow.</span></span> | <span data-ttu-id="500ec-166">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-166">Yes</span></span> |
| <span data-ttu-id="500ec-167">StartState</span><span class="sxs-lookup"><span data-stu-id="500ec-167">StartState</span></span> | <span data-ttu-id="500ec-168">Name of the initial state of the workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-168">Name of the initial state of the workflow.</span></span> | <span data-ttu-id="500ec-169">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-169">Yes</span></span> |
| <span data-ttu-id="500ec-170">Properties</span><span class="sxs-lookup"><span data-stu-id="500ec-170">Properties</span></span> | <span data-ttu-id="500ec-171">Collection of [identifiers](#identifiers).</span><span class="sxs-lookup"><span data-stu-id="500ec-171">Collection of [identifiers](#identifiers).</span></span> <span data-ttu-id="500ec-172">Represents data that can be read off-chain or visualized in a user experience tool.</span><span class="sxs-lookup"><span data-stu-id="500ec-172">Represents data that can be read off-chain or visualized in a user experience tool.</span></span> | <span data-ttu-id="500ec-173">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-173">Yes</span></span> |
| <span data-ttu-id="500ec-174">Constructor</span><span class="sxs-lookup"><span data-stu-id="500ec-174">Constructor</span></span> | <span data-ttu-id="500ec-175">Defines input parameters for creating an instance of the workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-175">Defines input parameters for creating an instance of the workflow.</span></span> | <span data-ttu-id="500ec-176">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-176">Yes</span></span> |
| <span data-ttu-id="500ec-177">Functions</span><span class="sxs-lookup"><span data-stu-id="500ec-177">Functions</span></span> | <span data-ttu-id="500ec-178">A collection of [functions](#functions) that can be executed in the workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-178">A collection of [functions](#functions) that can be executed in the workflow.</span></span> | <span data-ttu-id="500ec-179">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-179">Yes</span></span> |
| <span data-ttu-id="500ec-180">States</span><span class="sxs-lookup"><span data-stu-id="500ec-180">States</span></span> | <span data-ttu-id="500ec-181">A collection of workflow [states](#states).</span><span class="sxs-lookup"><span data-stu-id="500ec-181">A collection of workflow [states](#states).</span></span> | <span data-ttu-id="500ec-182">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-182">Yes</span></span> |

<span data-ttu-id="500ec-183">For an example, see [configuration file example](#configuration-file-example).</span><span class="sxs-lookup"><span data-stu-id="500ec-183">For an example, see [configuration file example](#configuration-file-example).</span></span>

## <a name="type"></a><span data-ttu-id="500ec-184">Type</span><span class="sxs-lookup"><span data-stu-id="500ec-184">Type</span></span>

<span data-ttu-id="500ec-185">Supported data types.</span><span class="sxs-lookup"><span data-stu-id="500ec-185">Supported data types.</span></span>

| <span data-ttu-id="500ec-186">Type</span><span class="sxs-lookup"><span data-stu-id="500ec-186">Type</span></span> | <span data-ttu-id="500ec-187">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-187">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="500ec-188">address</span><span class="sxs-lookup"><span data-stu-id="500ec-188">address</span></span>  | <span data-ttu-id="500ec-189">Blockchain address type, such as *contracts* or *users*</span><span class="sxs-lookup"><span data-stu-id="500ec-189">Blockchain address type, such as *contracts* or *users*</span></span> |
| <span data-ttu-id="500ec-190">bool</span><span class="sxs-lookup"><span data-stu-id="500ec-190">bool</span></span>     | <span data-ttu-id="500ec-191">Boolean data type</span><span class="sxs-lookup"><span data-stu-id="500ec-191">Boolean data type</span></span> |
| <span data-ttu-id="500ec-192">contract</span><span class="sxs-lookup"><span data-stu-id="500ec-192">contract</span></span> | <span data-ttu-id="500ec-193">Address of type contract</span><span class="sxs-lookup"><span data-stu-id="500ec-193">Address of type contract</span></span> |
| <span data-ttu-id="500ec-194">enum</span><span class="sxs-lookup"><span data-stu-id="500ec-194">enum</span></span>     | <span data-ttu-id="500ec-195">Enumerated set of named values.</span><span class="sxs-lookup"><span data-stu-id="500ec-195">Enumerated set of named values.</span></span> <span data-ttu-id="500ec-196">When using the enum type, you also specify a list of EnumValues.</span><span class="sxs-lookup"><span data-stu-id="500ec-196">When using the enum type, you also specify a list of EnumValues.</span></span> <span data-ttu-id="500ec-197">Each value is limited to 255 characters.</span><span class="sxs-lookup"><span data-stu-id="500ec-197">Each value is limited to 255 characters.</span></span> <span data-ttu-id="500ec-198">Valid value characters include upper and lower case letters (A-Z, a-z) and numbers (0-9).</span><span class="sxs-lookup"><span data-stu-id="500ec-198">Valid value characters include upper and lower case letters (A-Z, a-z) and numbers (0-9).</span></span> |
| <span data-ttu-id="500ec-199">int</span><span class="sxs-lookup"><span data-stu-id="500ec-199">int</span></span>      | <span data-ttu-id="500ec-200">Integer data type</span><span class="sxs-lookup"><span data-stu-id="500ec-200">Integer data type</span></span> |
| <span data-ttu-id="500ec-201">money</span><span class="sxs-lookup"><span data-stu-id="500ec-201">money</span></span>    | <span data-ttu-id="500ec-202">Money data type</span><span class="sxs-lookup"><span data-stu-id="500ec-202">Money data type</span></span> |
| <span data-ttu-id="500ec-203">state</span><span class="sxs-lookup"><span data-stu-id="500ec-203">state</span></span>    | <span data-ttu-id="500ec-204">Workflow state</span><span class="sxs-lookup"><span data-stu-id="500ec-204">Workflow state</span></span> |
| <span data-ttu-id="500ec-205">string</span><span class="sxs-lookup"><span data-stu-id="500ec-205">string</span></span>   | <span data-ttu-id="500ec-206">String data type</span><span class="sxs-lookup"><span data-stu-id="500ec-206">String data type</span></span> |
| <span data-ttu-id="500ec-207">user</span><span class="sxs-lookup"><span data-stu-id="500ec-207">user</span></span>     | <span data-ttu-id="500ec-208">Address of type user</span><span class="sxs-lookup"><span data-stu-id="500ec-208">Address of type user</span></span> |
| <span data-ttu-id="500ec-209">time</span><span class="sxs-lookup"><span data-stu-id="500ec-209">time</span></span>     | <span data-ttu-id="500ec-210">Time data type</span><span class="sxs-lookup"><span data-stu-id="500ec-210">Time data type</span></span> |
|`[ Application Role Name ]`| <span data-ttu-id="500ec-211">Any name specified in application role.</span><span class="sxs-lookup"><span data-stu-id="500ec-211">Any name specified in application role.</span></span> <span data-ttu-id="500ec-212">Limits users to be of that role type.</span><span class="sxs-lookup"><span data-stu-id="500ec-212">Limits users to be of that role type.</span></span> |

### <a name="example-configuration-of-type-string"></a><span data-ttu-id="500ec-213">Example configuration of type string</span><span class="sxs-lookup"><span data-stu-id="500ec-213">Example configuration of type string</span></span>

``` json
{
  "Name": "description",
  "Description": "Descriptive text",
  "DisplayName": "Description",
  "Type": {
    "Name": "string"
  }
}
```

### <a name="example-configuration-of-type-enum"></a><span data-ttu-id="500ec-214">Example configuration of type enum</span><span class="sxs-lookup"><span data-stu-id="500ec-214">Example configuration of type enum</span></span>

``` json
{
  "Name": "PropertyType",
  "DisplayName": "Property Type",
  "Description": "The type of the property",
  "Type": {
    "Name": "enum",
    "EnumValues": ["House", "Townhouse", "Condo", "Land"]
  }
}
```

#### <a name="using-enumeration-type-in-solidity"></a><span data-ttu-id="500ec-215">Using enumeration type in Solidity</span><span class="sxs-lookup"><span data-stu-id="500ec-215">Using enumeration type in Solidity</span></span>

<span data-ttu-id="500ec-216">Once an enum is defined in configuration, you can use enumeration types in Solidity.</span><span class="sxs-lookup"><span data-stu-id="500ec-216">Once an enum is defined in configuration, you can use enumeration types in Solidity.</span></span> <span data-ttu-id="500ec-217">For example, you can define an enum called PropertyTypeEnum.</span><span class="sxs-lookup"><span data-stu-id="500ec-217">For example, you can define an enum called PropertyTypeEnum.</span></span>

```
enum PropertyTypeEnum {House, Townhouse, Condo, Land} PropertyTypeEnum public PropertyType; 
```

<span data-ttu-id="500ec-218">The list of strings need to match between the configuration and smart contract to be valid and consistent declarations in Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="500ec-218">The list of strings need to match between the configuration and smart contract to be valid and consistent declarations in Blockchain Workbench.</span></span>

<span data-ttu-id="500ec-219">Assignment example:</span><span class="sxs-lookup"><span data-stu-id="500ec-219">Assignment example:</span></span>

```
PropertyType = PropertyTypeEnum.Townhouse;
```

<span data-ttu-id="500ec-220">Function parameter example:</span><span class="sxs-lookup"><span data-stu-id="500ec-220">Function parameter example:</span></span> 

``` 
function AssetTransfer(string description, uint256 price, PropertyTypeEnum propertyType) public
{
    InstanceOwner = msg.sender;
    AskingPrice = price;
    Description = description;
    PropertyType = propertyType;
    State = StateType.Active;
    ContractCreated();
}

```

## <a name="constructor"></a><span data-ttu-id="500ec-221">Constructor</span><span class="sxs-lookup"><span data-stu-id="500ec-221">Constructor</span></span>

<span data-ttu-id="500ec-222">Defines input parameters for an instance of a workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-222">Defines input parameters for an instance of a workflow.</span></span>

| <span data-ttu-id="500ec-223">Field</span><span class="sxs-lookup"><span data-stu-id="500ec-223">Field</span></span> | <span data-ttu-id="500ec-224">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-224">Description</span></span> | <span data-ttu-id="500ec-225">Required</span><span class="sxs-lookup"><span data-stu-id="500ec-225">Required</span></span> |
|-------|-------------|:--------:|
| <span data-ttu-id="500ec-226">Parameters</span><span class="sxs-lookup"><span data-stu-id="500ec-226">Parameters</span></span> | <span data-ttu-id="500ec-227">Collection of [identifiers](#identifiers) required to initiate a smart contract.</span><span class="sxs-lookup"><span data-stu-id="500ec-227">Collection of [identifiers](#identifiers) required to initiate a smart contract.</span></span> | <span data-ttu-id="500ec-228">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-228">Yes</span></span> |

### <a name="constructor-example"></a><span data-ttu-id="500ec-229">Constructor example</span><span class="sxs-lookup"><span data-stu-id="500ec-229">Constructor example</span></span>

``` json
{
  "Parameters": [
    {
      "Name": "description",
      "Description": "The description of this asset",
      "DisplayName": "Description",
      "Type": {
        "Name": "string"
      }
    },
    {
      "Name": "price",
      "Description": "The price of this asset",
      "DisplayName": "Price",
      "Type": {
        "Name": "money"
      }
    }
  ]
}
```

## <a name="functions"></a><span data-ttu-id="500ec-230">Functions</span><span class="sxs-lookup"><span data-stu-id="500ec-230">Functions</span></span>

<span data-ttu-id="500ec-231">Defines functions that can be executed on the workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-231">Defines functions that can be executed on the workflow.</span></span>

| <span data-ttu-id="500ec-232">Field</span><span class="sxs-lookup"><span data-stu-id="500ec-232">Field</span></span> | <span data-ttu-id="500ec-233">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-233">Description</span></span> | <span data-ttu-id="500ec-234">Required</span><span class="sxs-lookup"><span data-stu-id="500ec-234">Required</span></span> |
|-------|-------------|:--------:|
| <span data-ttu-id="500ec-235">Name</span><span class="sxs-lookup"><span data-stu-id="500ec-235">Name</span></span> | <span data-ttu-id="500ec-236">The unique name of the function.</span><span class="sxs-lookup"><span data-stu-id="500ec-236">The unique name of the function.</span></span> <span data-ttu-id="500ec-237">The corresponding smart contract must use the same **Name** for the applicable function.</span><span class="sxs-lookup"><span data-stu-id="500ec-237">The corresponding smart contract must use the same **Name** for the applicable function.</span></span> | <span data-ttu-id="500ec-238">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-238">Yes</span></span> |
| <span data-ttu-id="500ec-239">DisplayName</span><span class="sxs-lookup"><span data-stu-id="500ec-239">DisplayName</span></span> | <span data-ttu-id="500ec-240">Friendly display name of the function.</span><span class="sxs-lookup"><span data-stu-id="500ec-240">Friendly display name of the function.</span></span> | <span data-ttu-id="500ec-241">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-241">Yes</span></span> |
| <span data-ttu-id="500ec-242">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-242">Description</span></span> | <span data-ttu-id="500ec-243">Description of the function</span><span class="sxs-lookup"><span data-stu-id="500ec-243">Description of the function</span></span> | <span data-ttu-id="500ec-244">No</span><span class="sxs-lookup"><span data-stu-id="500ec-244">No</span></span> |
| <span data-ttu-id="500ec-245">Parameters</span><span class="sxs-lookup"><span data-stu-id="500ec-245">Parameters</span></span> | <span data-ttu-id="500ec-246">Collection of [identifiers](#identifiers) corresponding to the parameters of the function.</span><span class="sxs-lookup"><span data-stu-id="500ec-246">Collection of [identifiers](#identifiers) corresponding to the parameters of the function.</span></span> | <span data-ttu-id="500ec-247">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-247">Yes</span></span> |

### <a name="functions-example"></a><span data-ttu-id="500ec-248">Functions example</span><span class="sxs-lookup"><span data-stu-id="500ec-248">Functions example</span></span>

``` json
"Functions": [
  {
    "Name": "Modify",
    "DisplayName": "Modify",
    "Description": "Modify the description/price attributes of this asset transfer instance",
    "Parameters": [
      {
        "Name": "description",
        "Description": "The new description of the asset",
        "DisplayName": "Description",
        "Type": {
          "Name": "string"
        }
      },
      {
        "Name": "price",
        "Description": "The new price of the asset",
        "DisplayName": "Price",
        "Type": {
          "Name": "money"
        }
      }
    ]
  },
  {
    "Name": "Terminate",
    "DisplayName": "Terminate",
    "Description": "Used to cancel this particular instance of asset transfer",
    "Parameters": []
  }
]

```

## <a name="states"></a><span data-ttu-id="500ec-249">States</span><span class="sxs-lookup"><span data-stu-id="500ec-249">States</span></span>

<span data-ttu-id="500ec-250">A collection of unique states within a workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-250">A collection of unique states within a workflow.</span></span> <span data-ttu-id="500ec-251">Each state captures a step in the business logic's control flow.</span><span class="sxs-lookup"><span data-stu-id="500ec-251">Each state captures a step in the business logic's control flow.</span></span> 

| <span data-ttu-id="500ec-252">Field</span><span class="sxs-lookup"><span data-stu-id="500ec-252">Field</span></span> | <span data-ttu-id="500ec-253">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-253">Description</span></span> | <span data-ttu-id="500ec-254">Required</span><span class="sxs-lookup"><span data-stu-id="500ec-254">Required</span></span> |
|-------|-------------|:--------:|
| <span data-ttu-id="500ec-255">Name</span><span class="sxs-lookup"><span data-stu-id="500ec-255">Name</span></span> | <span data-ttu-id="500ec-256">Unique name of the state.</span><span class="sxs-lookup"><span data-stu-id="500ec-256">Unique name of the state.</span></span> <span data-ttu-id="500ec-257">The corresponding smart contract must use the same **Name** for the applicable state.</span><span class="sxs-lookup"><span data-stu-id="500ec-257">The corresponding smart contract must use the same **Name** for the applicable state.</span></span> | <span data-ttu-id="500ec-258">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-258">Yes</span></span> |
| <span data-ttu-id="500ec-259">DisplayName</span><span class="sxs-lookup"><span data-stu-id="500ec-259">DisplayName</span></span> | <span data-ttu-id="500ec-260">Friendly display name of the state.</span><span class="sxs-lookup"><span data-stu-id="500ec-260">Friendly display name of the state.</span></span> | <span data-ttu-id="500ec-261">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-261">Yes</span></span> |
| <span data-ttu-id="500ec-262">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-262">Description</span></span> | <span data-ttu-id="500ec-263">Description of the state.</span><span class="sxs-lookup"><span data-stu-id="500ec-263">Description of the state.</span></span> | <span data-ttu-id="500ec-264">No</span><span class="sxs-lookup"><span data-stu-id="500ec-264">No</span></span> |
| <span data-ttu-id="500ec-265">PercentComplete</span><span class="sxs-lookup"><span data-stu-id="500ec-265">PercentComplete</span></span> | <span data-ttu-id="500ec-266">An integer value displayed in the Blockchain Workbench user interface to show the progress within the business logic control flow.</span><span class="sxs-lookup"><span data-stu-id="500ec-266">An integer value displayed in the Blockchain Workbench user interface to show the progress within the business logic control flow.</span></span> | <span data-ttu-id="500ec-267">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-267">Yes</span></span> |
| <span data-ttu-id="500ec-268">Style</span><span class="sxs-lookup"><span data-stu-id="500ec-268">Style</span></span> | <span data-ttu-id="500ec-269">Visual hint indicating whether the state represents a success or failure state.</span><span class="sxs-lookup"><span data-stu-id="500ec-269">Visual hint indicating whether the state represents a success or failure state.</span></span> <span data-ttu-id="500ec-270">There are two valid values: `Success` or `Failure`.</span><span class="sxs-lookup"><span data-stu-id="500ec-270">There are two valid values: `Success` or `Failure`.</span></span> | <span data-ttu-id="500ec-271">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-271">Yes</span></span> |
| <span data-ttu-id="500ec-272">Transitions</span><span class="sxs-lookup"><span data-stu-id="500ec-272">Transitions</span></span> | <span data-ttu-id="500ec-273">Collection of available [transitions](#transitions) from the current state to the next set of states.</span><span class="sxs-lookup"><span data-stu-id="500ec-273">Collection of available [transitions](#transitions) from the current state to the next set of states.</span></span> | <span data-ttu-id="500ec-274">No</span><span class="sxs-lookup"><span data-stu-id="500ec-274">No</span></span> |

### <a name="states-example"></a><span data-ttu-id="500ec-275">States example</span><span class="sxs-lookup"><span data-stu-id="500ec-275">States example</span></span>

``` json
"States": [
    {
      "Name": "Active",
      "DisplayName": "Active",
      "Description": "The initial state of the asset transfer workflow",
      "PercentComplete": 20,
      "Style": "Success",
      "Transitions": [
        {
          "AllowedRoles": [],
          "AllowedInstanceRoles": [ "InstanceOwner" ],
          "Description": "Cancels this instance of asset transfer",
          "Function": "Terminate",
          "NextStates": [ "Terminated" ],
          "DisplayName": "Terminate Offer"
        },
        {
          "AllowedRoles": [ "Buyer" ],
          "AllowedInstanceRoles": [],
          "Description": "Make an offer for this asset",
          "Function": "MakeOffer",
          "NextStates": [ "OfferPlaced" ],
          "DisplayName": "Make Offer"
        },
        {
          "AllowedRoles": [],
          "AllowedInstanceRoles": [ "InstanceOwner" ],
          "Description": "Modify attributes of this asset transfer instance",
          "Function": "Modify",
          "NextStates": [ "Active" ],
          "DisplayName": "Modify"
        }
      ]
    },
    {
      "Name": "Accepted",
      "DisplayName": "Accepted",
      "Description": "Asset transfer process is complete",
      "PercentComplete": 100,
      "Style": "Success",
      "Transitions": []
    },
    {
      "Name": "Terminated",
      "DisplayName": "Terminated",
      "Description": "Asset transfer has been cancelled",
      "PercentComplete": 100,
      "Style": "Failure",
      "Transitions": []
    }
  ]
```

## <a name="transitions"></a><span data-ttu-id="500ec-276">Transitions</span><span class="sxs-lookup"><span data-stu-id="500ec-276">Transitions</span></span>

<span data-ttu-id="500ec-277">Available actions to the next state.</span><span class="sxs-lookup"><span data-stu-id="500ec-277">Available actions to the next state.</span></span> <span data-ttu-id="500ec-278">One or more user roles may perform an action at each state, where an action may transition a state to another state in the workflow.</span><span class="sxs-lookup"><span data-stu-id="500ec-278">One or more user roles may perform an action at each state, where an action may transition a state to another state in the workflow.</span></span> 

| <span data-ttu-id="500ec-279">Field</span><span class="sxs-lookup"><span data-stu-id="500ec-279">Field</span></span> | <span data-ttu-id="500ec-280">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-280">Description</span></span> | <span data-ttu-id="500ec-281">Required</span><span class="sxs-lookup"><span data-stu-id="500ec-281">Required</span></span> |
|-------|-------------|:--------:|
| <span data-ttu-id="500ec-282">AllowedRoles</span><span class="sxs-lookup"><span data-stu-id="500ec-282">AllowedRoles</span></span> | <span data-ttu-id="500ec-283">List of applications roles allowed to initiate the transition.</span><span class="sxs-lookup"><span data-stu-id="500ec-283">List of applications roles allowed to initiate the transition.</span></span> <span data-ttu-id="500ec-284">All users of the specified role may be able to perform the action.</span><span class="sxs-lookup"><span data-stu-id="500ec-284">All users of the specified role may be able to perform the action.</span></span> | <span data-ttu-id="500ec-285">No</span><span class="sxs-lookup"><span data-stu-id="500ec-285">No</span></span> |
| <span data-ttu-id="500ec-286">AllowedInstanceRoles</span><span class="sxs-lookup"><span data-stu-id="500ec-286">AllowedInstanceRoles</span></span> | <span data-ttu-id="500ec-287">List of user roles participating or specified in the smart contract allowed to initiate the transition.</span><span class="sxs-lookup"><span data-stu-id="500ec-287">List of user roles participating or specified in the smart contract allowed to initiate the transition.</span></span> <span data-ttu-id="500ec-288">Instance roles are defined in **Properties** within workflows.</span><span class="sxs-lookup"><span data-stu-id="500ec-288">Instance roles are defined in **Properties** within workflows.</span></span> <span data-ttu-id="500ec-289">AllowedInstanceRoles represent a user participating in an instance of a smart contract.</span><span class="sxs-lookup"><span data-stu-id="500ec-289">AllowedInstanceRoles represent a user participating in an instance of a smart contract.</span></span> <span data-ttu-id="500ec-290">AllowedInstanceRoles give you the ability to restrict taking an action to a user role in a contract instance.</span><span class="sxs-lookup"><span data-stu-id="500ec-290">AllowedInstanceRoles give you the ability to restrict taking an action to a user role in a contract instance.</span></span>  <span data-ttu-id="500ec-291">For example, you may only want to allow the user who created the contract (InstanceOwner) to be able to terminate rather than all users in role type (Owner) if you specified the role in AllowedRoles.</span><span class="sxs-lookup"><span data-stu-id="500ec-291">For example, you may only want to allow the user who created the contract (InstanceOwner) to be able to terminate rather than all users in role type (Owner) if you specified the role in AllowedRoles.</span></span> | <span data-ttu-id="500ec-292">No</span><span class="sxs-lookup"><span data-stu-id="500ec-292">No</span></span> |
| <span data-ttu-id="500ec-293">DisplayName</span><span class="sxs-lookup"><span data-stu-id="500ec-293">DisplayName</span></span> | <span data-ttu-id="500ec-294">Friendly display name of the transition.</span><span class="sxs-lookup"><span data-stu-id="500ec-294">Friendly display name of the transition.</span></span> | <span data-ttu-id="500ec-295">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-295">Yes</span></span> |
| <span data-ttu-id="500ec-296">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-296">Description</span></span> | <span data-ttu-id="500ec-297">Description of the transition.</span><span class="sxs-lookup"><span data-stu-id="500ec-297">Description of the transition.</span></span> | <span data-ttu-id="500ec-298">No</span><span class="sxs-lookup"><span data-stu-id="500ec-298">No</span></span> |
| <span data-ttu-id="500ec-299">Function</span><span class="sxs-lookup"><span data-stu-id="500ec-299">Function</span></span> | <span data-ttu-id="500ec-300">The name of the function to initiate the transition.</span><span class="sxs-lookup"><span data-stu-id="500ec-300">The name of the function to initiate the transition.</span></span> | <span data-ttu-id="500ec-301">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-301">Yes</span></span> |
| <span data-ttu-id="500ec-302">NextStates</span><span class="sxs-lookup"><span data-stu-id="500ec-302">NextStates</span></span> | <span data-ttu-id="500ec-303">A collection of potential next states after a successful transition.</span><span class="sxs-lookup"><span data-stu-id="500ec-303">A collection of potential next states after a successful transition.</span></span> | <span data-ttu-id="500ec-304">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-304">Yes</span></span> |

### <a name="transitions-example"></a><span data-ttu-id="500ec-305">Transitions example</span><span class="sxs-lookup"><span data-stu-id="500ec-305">Transitions example</span></span>

``` json
"Transitions": [
  {
    "AllowedRoles": [],
    "AllowedInstanceRoles": [ "InstanceOwner" ],
    "Description": "Cancels this instance of asset transfer",
    "Function": "Terminate",
    "NextStates": [ "Terminated" ],
    "DisplayName": "Terminate Offer"
  },
  {
    "AllowedRoles": [ "Buyer" ],
    "AllowedInstanceRoles": [],
    "Description": "Make an offer for this asset",
    "Function": "MakeOffer",
    "NextStates": [ "OfferPlaced" ],
    "DisplayName": "Make Offer"
  },
  {
    "AllowedRoles": [],
    "AllowedInstanceRoles": [ "InstanceOwner" ],
    "Description": "Modify attributes of this asset transfer instance",
    "Function": "Modify",
    "NextStates": [ "Active" ],
    "DisplayName": "Modify"
  }
]

```

## <a name="application-roles"></a><span data-ttu-id="500ec-306">Application roles</span><span class="sxs-lookup"><span data-stu-id="500ec-306">Application roles</span></span>

<span data-ttu-id="500ec-307">Application roles define a set of roles that can be assigned to users who want to act or participate within the application.</span><span class="sxs-lookup"><span data-stu-id="500ec-307">Application roles define a set of roles that can be assigned to users who want to act or participate within the application.</span></span> <span data-ttu-id="500ec-308">Application roles can be used to restrict actions and participation within the blockchain application and corresponding workflows.</span><span class="sxs-lookup"><span data-stu-id="500ec-308">Application roles can be used to restrict actions and participation within the blockchain application and corresponding workflows.</span></span> 

| <span data-ttu-id="500ec-309">Field</span><span class="sxs-lookup"><span data-stu-id="500ec-309">Field</span></span> | <span data-ttu-id="500ec-310">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-310">Description</span></span> | <span data-ttu-id="500ec-311">Required</span><span class="sxs-lookup"><span data-stu-id="500ec-311">Required</span></span> |
|-------|-------------|:--------:|
| <span data-ttu-id="500ec-312">Name</span><span class="sxs-lookup"><span data-stu-id="500ec-312">Name</span></span> | <span data-ttu-id="500ec-313">The unique name of the application role.</span><span class="sxs-lookup"><span data-stu-id="500ec-313">The unique name of the application role.</span></span> <span data-ttu-id="500ec-314">The corresponding smart contract must use the same **Name** for the applicable role.</span><span class="sxs-lookup"><span data-stu-id="500ec-314">The corresponding smart contract must use the same **Name** for the applicable role.</span></span> <span data-ttu-id="500ec-315">Base type names are reserved.</span><span class="sxs-lookup"><span data-stu-id="500ec-315">Base type names are reserved.</span></span> <span data-ttu-id="500ec-316">You cannot name an application role with the same name as [Type](#type)</span><span class="sxs-lookup"><span data-stu-id="500ec-316">You cannot name an application role with the same name as [Type](#type)</span></span>| <span data-ttu-id="500ec-317">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-317">Yes</span></span> |
| <span data-ttu-id="500ec-318">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-318">Description</span></span> | <span data-ttu-id="500ec-319">Description of the application role.</span><span class="sxs-lookup"><span data-stu-id="500ec-319">Description of the application role.</span></span> | <span data-ttu-id="500ec-320">No</span><span class="sxs-lookup"><span data-stu-id="500ec-320">No</span></span> |

### <a name="application-roles-example"></a><span data-ttu-id="500ec-321">Application roles example</span><span class="sxs-lookup"><span data-stu-id="500ec-321">Application roles example</span></span>

``` json
"ApplicationRoles": [
  {
    "Name": "Appraiser",
    "Description": "User that signs off on the asset price"
  },
  {
    "Name": "Buyer",
    "Description": "User that places an offer on an asset"
  }
]
```
## <a name="identifiers"></a><span data-ttu-id="500ec-322">Identifiers</span><span class="sxs-lookup"><span data-stu-id="500ec-322">Identifiers</span></span>

<span data-ttu-id="500ec-323">Identifiers represent a collection of information used to describe workflow properties, constructor, and function parameters.</span><span class="sxs-lookup"><span data-stu-id="500ec-323">Identifiers represent a collection of information used to describe workflow properties, constructor, and function parameters.</span></span> 

| <span data-ttu-id="500ec-324">Field</span><span class="sxs-lookup"><span data-stu-id="500ec-324">Field</span></span> | <span data-ttu-id="500ec-325">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-325">Description</span></span> | <span data-ttu-id="500ec-326">Required</span><span class="sxs-lookup"><span data-stu-id="500ec-326">Required</span></span> |
|-------|-------------|:--------:|
| <span data-ttu-id="500ec-327">Name</span><span class="sxs-lookup"><span data-stu-id="500ec-327">Name</span></span> | <span data-ttu-id="500ec-328">The unique name of the property or parameter.</span><span class="sxs-lookup"><span data-stu-id="500ec-328">The unique name of the property or parameter.</span></span> <span data-ttu-id="500ec-329">The corresponding smart contract must use the same **Name** for the applicable property or parameter.</span><span class="sxs-lookup"><span data-stu-id="500ec-329">The corresponding smart contract must use the same **Name** for the applicable property or parameter.</span></span> | <span data-ttu-id="500ec-330">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-330">Yes</span></span> |
| <span data-ttu-id="500ec-331">DisplayName</span><span class="sxs-lookup"><span data-stu-id="500ec-331">DisplayName</span></span> | <span data-ttu-id="500ec-332">Friendly display name for the property or parameter.</span><span class="sxs-lookup"><span data-stu-id="500ec-332">Friendly display name for the property or parameter.</span></span> | <span data-ttu-id="500ec-333">Yes</span><span class="sxs-lookup"><span data-stu-id="500ec-333">Yes</span></span> |
| <span data-ttu-id="500ec-334">Description</span><span class="sxs-lookup"><span data-stu-id="500ec-334">Description</span></span> | <span data-ttu-id="500ec-335">Description of the property or parameter.</span><span class="sxs-lookup"><span data-stu-id="500ec-335">Description of the property or parameter.</span></span> | <span data-ttu-id="500ec-336">No</span><span class="sxs-lookup"><span data-stu-id="500ec-336">No</span></span> |

### <a name="identifiers-example"></a><span data-ttu-id="500ec-337">Identifiers example</span><span class="sxs-lookup"><span data-stu-id="500ec-337">Identifiers example</span></span>

``` json
"Properties": [
  {
    "Name": "State",
    "DisplayName": "State",
    "Description": "Holds the state of the contract",
    "Type": {
      "Name": "state"
    }
  },
  {
    "Name": "Description",
    "DisplayName": "Description",
    "Description": "Describes the asset being sold",
    "Type": {
      "Name": "string"
    }
  }
]
```

## <a name="configuration-file-example"></a><span data-ttu-id="500ec-338">Configuration file example</span><span class="sxs-lookup"><span data-stu-id="500ec-338">Configuration file example</span></span>

<span data-ttu-id="500ec-339">Asset transfer is a smart contract scenario for buying and selling high value assets, which require an inspector and appraiser.</span><span class="sxs-lookup"><span data-stu-id="500ec-339">Asset transfer is a smart contract scenario for buying and selling high value assets, which require an inspector and appraiser.</span></span> <span data-ttu-id="500ec-340">Sellers can list their assets by instantiating an asset transfer smart contract.</span><span class="sxs-lookup"><span data-stu-id="500ec-340">Sellers can list their assets by instantiating an asset transfer smart contract.</span></span> <span data-ttu-id="500ec-341">Buyers can make offers by taking an action on the smart contract, and other parties can take actions to inspect or appraise the asset.</span><span class="sxs-lookup"><span data-stu-id="500ec-341">Buyers can make offers by taking an action on the smart contract, and other parties can take actions to inspect or appraise the asset.</span></span> <span data-ttu-id="500ec-342">Once the asset is marked both inspected and appraised, the buyer and seller will confirm the sale again before the contract is set to complete.</span><span class="sxs-lookup"><span data-stu-id="500ec-342">Once the asset is marked both inspected and appraised, the buyer and seller will confirm the sale again before the contract is set to complete.</span></span> <span data-ttu-id="500ec-343">At each point in the process, all participants have visibility into the state of the contract as it is updated.</span><span class="sxs-lookup"><span data-stu-id="500ec-343">At each point in the process, all participants have visibility into the state of the contract as it is updated.</span></span> 

<span data-ttu-id="500ec-344">For more information including the code files, see [asset transfer sample for Azure Blockchain Workbench](https://github.com/Azure-Samples/blockchain/tree/master/blockchain-workbench/application-and-smart-contract-samples/asset-transfer)</span><span class="sxs-lookup"><span data-stu-id="500ec-344">For more information including the code files, see [asset transfer sample for Azure Blockchain Workbench](https://github.com/Azure-Samples/blockchain/tree/master/blockchain-workbench/application-and-smart-contract-samples/asset-transfer)</span></span>

<span data-ttu-id="500ec-345">The following configuration file is for the asset transfer sample:</span><span class="sxs-lookup"><span data-stu-id="500ec-345">The following configuration file is for the asset transfer sample:</span></span>

``` json
{
  "ApplicationName": "AssetTransfer",
  "DisplayName": "Asset Transfer",
  "Description": "Allows transfer of assets between a buyer and a seller, with appraisal/inspection functionality",
  "ApplicationRoles": [
    {
      "Name": "Appraiser",
      "Description": "User that signs off on the asset price"
    },
    {
      "Name": "Buyer",
      "Description": "User that places an offer on an asset"
    },
    {
      "Name": "Inspector",
      "Description": "User that inspects the asset and signs off on inspection"
    },
    {
      "Name": "Owner",
      "Description": "User that signs off on the asset price"
    }
  ],
  "Workflows": [
    {
      "Name": "AssetTransfer",
      "DisplayName": "Asset Transfer",
      "Description": "Handles the business logic for the asset transfer scenario",
      "Initiators": [ "Owner" ],
      "StartState":  "Active",
      "Properties": [
        {
          "Name": "State",
          "DisplayName": "State",
          "Description": "Holds the state of the contract",
          "Type": {
            "Name": "state"
          }
        },
        {
          "Name": "Description",
          "DisplayName": "Description",
          "Description": "Describes the asset being sold",
          "Type": {
            "Name": "string"
          }
        },
        {
          "Name": "AskingPrice",
          "DisplayName": "Asking Price",
          "Description": "The asking price for the asset",
          "Type": {
            "Name": "money"
          }
        },
        {
          "Name": "OfferPrice",
          "DisplayName": "Offer Price",
          "Description": "The price being offered for the asset",
          "Type": {
            "Name": "money"
          }
        },
        {
          "Name": "InstanceAppraiser",
          "DisplayName": "Instance Appraiser",
          "Description": "The user that appraises the asset",
          "Type": {
            "Name": "Appraiser"
          }
        },
        {
          "Name": "InstanceBuyer",
          "DisplayName": "Instance Buyer",
          "Description": "The user that places an offer for this asset",
          "Type": {
            "Name": "Buyer"
          }
        },
        {
          "Name": "InstanceInspector",
          "DisplayName": "Instance Inspector",
          "Description": "The user that inspects this asset",
          "Type": {
            "Name": "Inspector"
          }
        },
        {
          "Name": "InstanceOwner",
          "DisplayName": "Instance Owner",
          "Description": "The seller of this particular asset",
          "Type": {
            "Name": "Owner"
          }
        }
      ],
      "Constructor": {
        "Parameters": [
          {
            "Name": "description",
            "Description": "The description of this asset",
            "DisplayName": "Description",
            "Type": {
              "Name": "string"
            }
          },
          {
            "Name": "price",
            "Description": "The price of this asset",
            "DisplayName": "Price",
            "Type": {
              "Name": "money"
            }
          }
        ]
      },
      "Functions": [
        {
          "Name": "Modify",
          "DisplayName": "Modify",
          "Description": "Modify the description/price attributes of this asset transfer instance",
          "Parameters": [
            {
              "Name": "description",
              "Description": "The new description of the asset",
              "DisplayName": "Description",
              "Type": {
                "Name": "string"
              }
            },
            {
              "Name": "price",
              "Description": "The new price of the asset",
              "DisplayName": "Price",
              "Type": {
                "Name": "money"
              }
            }
          ]
        },
        {
          "Name": "Terminate",
          "DisplayName": "Terminate",
          "Description": "Used to cancel this particular instance of asset transfer",
          "Parameters": []
        },
        {
          "Name": "MakeOffer",
          "DisplayName": "Make Offer",
          "Description": "Place an offer for this asset",
          "Parameters": [
            {
              "Name": "inspector",
              "Description": "Specify a user to inspect this asset",
              "DisplayName": "Inspector",
              "Type": {
                "Name": "Inspector"
              }
            },
            {
              "Name": "appraiser",
              "Description": "Specify a user to appraise this asset",
              "DisplayName": "Appraiser",
              "Type": {
                "Name": "Appraiser"
              }
            },
            {
              "Name": "offerPrice",
              "Description": "Specify your offer price for this asset",
              "DisplayName": "Offer Price",
              "Type": {
                "Name": "money"
              }
            }
          ]
        },
        {
          "Name": "Reject",
          "DisplayName": "Reject",
          "Description": "Reject the user's offer",
          "Parameters": []
        },
        {
          "Name": "AcceptOffer",
          "DisplayName": "Accept Offer",
          "Description": "Accept the user's offer",
          "Parameters": []
        },
        {
          "Name": "RescindOffer",
          "DisplayName": "Rescind Offer",
          "Description": "Rescind your placed offer",
          "Parameters": []
        },
        {
          "Name": "ModifyOffer",
          "DisplayName": "Modify Offer",
          "Description": "Modify the price of your placed offer",
          "Parameters": [
            {
              "Name": "offerPrice",
              "DisplayName": "Price",
              "Type": {
                "Name": "money"
              }
            }
          ]
        },
        {
          "Name": "Accept",
          "DisplayName": "Accept",
          "Description": "Accept the inspection/appraisal results",
          "Parameters": []
        },
        {
          "Name": "MarkInspected",
          "DisplayName": "Mark Inspected",
          "Description": "Mark the asset as inspected",
          "Parameters": []
        },
        {
          "Name": "MarkAppraised",
          "DisplayName": "Mark Appraised",
          "Description": "Mark the asset as appraised",
          "Parameters": []
        }
      ],
      "States": [
        {
          "Name": "Active",
          "DisplayName": "Active",
          "Description": "The initial state of the asset transfer workflow",
          "PercentComplete": 20,
          "Style": "Success",
          "Transitions": [
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Cancels this instance of asset transfer",
              "Function": "Terminate",
              "NextStates": [ "Terminated" ],
              "DisplayName": "Terminate Offer"
            },
            {
              "AllowedRoles": [ "Buyer" ],
              "AllowedInstanceRoles": [],
              "Description": "Make an offer for this asset",
              "Function": "MakeOffer",
              "NextStates": [ "OfferPlaced" ],
              "DisplayName": "Make Offer"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Modify attributes of this asset transfer instance",
              "Function": "Modify",
              "NextStates": [ "Active" ],
              "DisplayName": "Modify"
            }
          ]
        },
        {
          "Name": "OfferPlaced",
          "DisplayName": "Offer Placed",
          "Description": "Offer has been placed for the asset",
          "PercentComplete": 30,
          "Style": "Success",
          "Transitions": [
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Accept the proposed offer for the asset",
              "Function": "AcceptOffer",
              "NextStates": [ "PendingInspection" ],
              "DisplayName": "Accept Offer"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Reject the proposed offer for the asset",
              "Function": "Reject",
              "NextStates": [ "Active" ],
              "DisplayName": "Reject"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Cancel this instance of asset transfer",
              "Function": "Terminate",
              "NextStates": [ "Terminated" ],
              "DisplayName": "Terminate"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceBuyer" ],
              "Description": "Rescind the offer you previously placed for this asset",
              "Function": "RescindOffer",
              "NextStates": [ "Active" ],
              "DisplayName": "Rescind Offer"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceBuyer" ],
              "Description": "Modify the price that you specified for your offer",
              "Function": "ModifyOffer",
              "NextStates": [ "OfferPlaced" ],
              "DisplayName": "Modify Offer"
            }
          ]
        },
        {
          "Name": "PendingInspection",
          "DisplayName": "Pending Inspection",
          "Description": "Asset is pending inspection",
          "PercentComplete": 40,
          "Style": "Success",
          "Transitions": [
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Reject the offer",
              "Function": "Reject",
              "NextStates": [ "Active" ],
              "DisplayName": "Reject"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Cancel the offer",
              "Function": "Terminate",
              "NextStates": [ "Terminated" ],
              "DisplayName": "Terminate"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceBuyer" ],
              "Description": "Rescind the offer you placed for this asset",
              "Function": "RescindOffer",
              "NextStates": [ "Active" ],
              "DisplayName": "Rescind Offer"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceInspector" ],
              "Description": "Mark this asset as inspected",
              "Function": "MarkInspected",
              "NextStates": [ "Inspected" ],
              "DisplayName": "Mark Inspected"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceAppraiser" ],
              "Description": "Mark this asset as appraised",
              "Function": "MarkAppraised",
              "NextStates": [ "Appraised" ],
              "DisplayName": "Mark Appraised"
            }
          ]
        },
        {
          "Name": "Inspected",
          "DisplayName": "Inspected",
          "PercentComplete": 45,
          "Style": "Success",
          "Transitions": [
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Reject the offer",
              "Function": "Reject",
              "NextStates": [ "Active" ],
              "DisplayName": "Reject"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Cancel the offer",
              "Function": "Terminate",
              "NextStates": [ "Terminated" ],
              "DisplayName": "Terminate"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceBuyer" ],
              "Description": "Rescind the offer you placed for this asset",
              "Function": "RescindOffer",
              "NextStates": [ "Active" ],
              "DisplayName": "Rescind Offer"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceAppraiser" ],
              "Description": "Mark this asset as appraised",
              "Function": "MarkAppraised",
              "NextStates": [ "NotionalAcceptance" ],
              "DisplayName": "Mark Appraised"
            }
          ]
        },
        {
          "Name": "Appraised",
          "DisplayName": "Appraised",
          "Description": "Asset has been appraised, now awaiting inspection",
          "PercentComplete": 45,
          "Style": "Success",
          "Transitions": [
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Reject the offer",
              "Function": "Reject",
              "NextStates": [ "Active" ],
              "DisplayName": "Reject"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Cancel the offer",
              "Function": "Terminate",
              "NextStates": [ "Terminated" ],
              "DisplayName": "Terminate"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceBuyer" ],
              "Description": "Rescind the offer you placed for this asset",
              "Function": "RescindOffer",
              "NextStates": [ "Active" ],
              "DisplayName": "Rescind Offer"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceInspector" ],
              "Description": "Mark the asset as inspected",
              "Function": "MarkInspected",
              "NextStates": [ "NotionalAcceptance" ],
              "DisplayName": "Mark Inspected"
            }
          ]
        },
        {
          "Name": "NotionalAcceptance",
          "DisplayName": "Notional Acceptance",
          "Description": "Asset has been inspected and appraised, awaiting final sign-off from buyer and seller",
          "PercentComplete": 50,
          "Style": "Success",
          "Transitions": [
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Sign-off on inspection and appraisal",
              "Function": "Accept",
              "NextStates": [ "SellerAccepted" ],
              "DisplayName": "SellerAccept"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Reject the proposed offer for the asset",
              "Function": "Reject",
              "NextStates": [ "Active" ],
              "DisplayName": "Reject"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Cancel this instance of asset transfer",
              "Function": "Terminate",
              "NextStates": [ "Terminated" ],
              "DisplayName": "Terminate"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceBuyer" ],
              "Description": "Sign-off on inspection and appraisal",
              "Function": "Accept",
              "NextStates": [ "BuyerAccepted" ],
              "DisplayName": "BuyerAccept"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceBuyer" ],
              "Description": "Rescind the offer you placed for this asset",
              "Function": "RescindOffer",
              "NextStates": [ "Active" ],
              "DisplayName": "Rescind Offer"
            }
          ]
        },
        {
          "Name": "BuyerAccepted",
          "DisplayName": "Buyer Accepted",
          "Description": "Buyer has signed-off on inspection and appraisal",
          "PercentComplete": 75,
          "Style": "Success",
          "Transitions": [
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Sign-off on inspection and appraisal",
              "Function": "Accept",
              "NextStates": [ "SellerAccepted" ],
              "DisplayName": "Accept"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Reject the proposed offer for the asset",
              "Function": "Reject",
              "NextStates": [ "Active" ],
              "DisplayName": "Reject"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceOwner" ],
              "Description": "Cancel this instance of asset transfer",
              "Function": "Terminate",
              "NextStates": [ "Terminated" ],
              "DisplayName": "Terminate"
            }
          ]
        },
        {
          "Name": "SellerAccepted",
          "DisplayName": "Seller Accepted",
          "Description": "Seller has signed-off on inspection and appraisal",
          "PercentComplete": 75,
          "Style": "Success",
          "Transitions": [
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceBuyer" ],
              "Description": "Sign-off on inspection and appraisal",
              "Function": "Accept",
              "NextStates": [ "Accepted" ],
              "DisplayName": "Accept"
            },
            {
              "AllowedRoles": [],
              "AllowedInstanceRoles": [ "InstanceBuyer" ],
              "Description": "Rescind the offer you placed for this asset",
              "Function": "RescindOffer",
              "NextStates": [ "Active" ],
              "DisplayName": "Rescind Offer"
            }
          ]
        },
        {
          "Name": "Accepted",
          "DisplayName": "Accepted",
          "Description": "Asset transfer process is complete",
          "PercentComplete": 100,
          "Style": "Success",
          "Transitions": []
        },
        {
          "Name": "Terminated",
          "DisplayName": "Terminated",
          "Description": "Asset transfer has been cancelled",
          "PercentComplete": 100,
          "Style": "Failure",
          "Transitions": []
        }
      ]
    }
  ]
}
```
## <a name="next-steps"></a><span data-ttu-id="500ec-346">Next steps</span><span class="sxs-lookup"><span data-stu-id="500ec-346">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="500ec-347">Azure Blockchain Workbench REST API reference</span><span class="sxs-lookup"><span data-stu-id="500ec-347">Azure Blockchain Workbench REST API reference</span></span>](https://docs.microsoft.com/rest/api/azure-blockchain-workbench)

