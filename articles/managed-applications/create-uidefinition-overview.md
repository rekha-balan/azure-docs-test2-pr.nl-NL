---
title: Understand creating UI definition for Azure managed applications | Microsoft Docs
description: Describes how to create UI definitions for Azure Managed Applications
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2017
ms.author: tomfitz
ms.openlocfilehash: 59003e71324f5342cb2b724f670603fd6b67afe4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864831"
---
# <a name="create-azure-portal-user-interface-for-your-managed-application"></a><span data-ttu-id="4ae15-103">Create Azure portal user interface for your managed application</span><span class="sxs-lookup"><span data-stu-id="4ae15-103">Create Azure portal user interface for your managed application</span></span>
<span data-ttu-id="4ae15-104">This document introduces the core concepts of the createUiDefinition.json file.</span><span class="sxs-lookup"><span data-stu-id="4ae15-104">This document introduces the core concepts of the createUiDefinition.json file.</span></span> <span data-ttu-id="4ae15-105">The Azure portal uses this file to generate the user interface for creating a managed application.</span><span class="sxs-lookup"><span data-stu-id="4ae15-105">The Azure portal uses this file to generate the user interface for creating a managed application.</span></span>

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json#",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

<span data-ttu-id="4ae15-106">A CreateUiDefinition always contains three properties:</span><span class="sxs-lookup"><span data-stu-id="4ae15-106">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="4ae15-107">handler</span><span class="sxs-lookup"><span data-stu-id="4ae15-107">handler</span></span>
* <span data-ttu-id="4ae15-108">version</span><span class="sxs-lookup"><span data-stu-id="4ae15-108">version</span></span>
* <span data-ttu-id="4ae15-109">parameters</span><span class="sxs-lookup"><span data-stu-id="4ae15-109">parameters</span></span>

<span data-ttu-id="4ae15-110">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="4ae15-110">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="4ae15-111">The schema of the parameters property depends on the combination of the specified handler and version.</span><span class="sxs-lookup"><span data-stu-id="4ae15-111">The schema of the parameters property depends on the combination of the specified handler and version.</span></span> <span data-ttu-id="4ae15-112">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span><span class="sxs-lookup"><span data-stu-id="4ae15-112">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="4ae15-113">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4ae15-113">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span></span> <span data-ttu-id="4ae15-114">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span><span class="sxs-lookup"><span data-stu-id="4ae15-114">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="4ae15-115">Including `$schema` is recommended, but optional.</span><span class="sxs-lookup"><span data-stu-id="4ae15-115">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="4ae15-116">If specified, the value for `version` must match the version within the `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="4ae15-116">If specified, the value for `version` must match the version within the `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="4ae15-117">Basics</span><span class="sxs-lookup"><span data-stu-id="4ae15-117">Basics</span></span>
<span data-ttu-id="4ae15-118">The Basics step is always the first step of the wizard generated when the Azure portal parses the file.</span><span class="sxs-lookup"><span data-stu-id="4ae15-118">The Basics step is always the first step of the wizard generated when the Azure portal parses the file.</span></span> <span data-ttu-id="4ae15-119">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span><span class="sxs-lookup"><span data-stu-id="4ae15-119">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span></span> <span data-ttu-id="4ae15-120">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span><span class="sxs-lookup"><span data-stu-id="4ae15-120">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="4ae15-121">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span><span class="sxs-lookup"><span data-stu-id="4ae15-121">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="4ae15-122">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span><span class="sxs-lookup"><span data-stu-id="4ae15-122">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span></span> <span data-ttu-id="4ae15-123">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span><span class="sxs-lookup"><span data-stu-id="4ae15-123">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="4ae15-124">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span><span class="sxs-lookup"><span data-stu-id="4ae15-124">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="4ae15-125">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span><span class="sxs-lookup"><span data-stu-id="4ae15-125">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="4ae15-126">Steps</span><span class="sxs-lookup"><span data-stu-id="4ae15-126">Steps</span></span>
<span data-ttu-id="4ae15-127">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span><span class="sxs-lookup"><span data-stu-id="4ae15-127">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="4ae15-128">Consider adding steps per role or tier of the application being deployed.</span><span class="sxs-lookup"><span data-stu-id="4ae15-128">Consider adding steps per role or tier of the application being deployed.</span></span> <span data-ttu-id="4ae15-129">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span><span class="sxs-lookup"><span data-stu-id="4ae15-129">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="4ae15-130">Outputs</span><span class="sxs-lookup"><span data-stu-id="4ae15-130">Outputs</span></span>
<span data-ttu-id="4ae15-131">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span><span class="sxs-lookup"><span data-stu-id="4ae15-131">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span></span> <span data-ttu-id="4ae15-132">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span><span class="sxs-lookup"><span data-stu-id="4ae15-132">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span></span>

<span data-ttu-id="4ae15-133">To set the managed application resource name, you must include a value named `applicationResourceName` in the outputs property.</span><span class="sxs-lookup"><span data-stu-id="4ae15-133">To set the managed application resource name, you must include a value named `applicationResourceName` in the outputs property.</span></span> <span data-ttu-id="4ae15-134">If you do not set this value, the application assigns a GUID for the name.</span><span class="sxs-lookup"><span data-stu-id="4ae15-134">If you do not set this value, the application assigns a GUID for the name.</span></span> <span data-ttu-id="4ae15-135">You can include a textbox in the user interface that requests a name from the user.</span><span class="sxs-lookup"><span data-stu-id="4ae15-135">You can include a textbox in the user interface that requests a name from the user.</span></span>

```json
"outputs": {
    "vmName": "[steps('appSettings').vmName]",
    "trialOrProduction": "[steps('appSettings').trialOrProd]",
    "userName": "[steps('vmCredentials').adminUsername]",
    "pwd": "[steps('vmCredentials').vmPwd.password]",
    "applicationResourceName": "[steps('appSettings').vmName]"
}
```

## <a name="functions"></a><span data-ttu-id="4ae15-136">Functions</span><span class="sxs-lookup"><span data-stu-id="4ae15-136">Functions</span></span>
<span data-ttu-id="4ae15-137">Similar to template functions in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span><span class="sxs-lookup"><span data-stu-id="4ae15-137">Similar to template functions in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ae15-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ae15-138">Next steps</span></span>
<span data-ttu-id="4ae15-139">The createUiDefinition.json file itself has a simple schema.</span><span class="sxs-lookup"><span data-stu-id="4ae15-139">The createUiDefinition.json file itself has a simple schema.</span></span> <span data-ttu-id="4ae15-140">The real depth of it comes from all the supported elements and functions.</span><span class="sxs-lookup"><span data-stu-id="4ae15-140">The real depth of it comes from all the supported elements and functions.</span></span> <span data-ttu-id="4ae15-141">Those items are described in greater detail at:</span><span class="sxs-lookup"><span data-stu-id="4ae15-141">Those items are described in greater detail at:</span></span>

- [<span data-ttu-id="4ae15-142">Elements</span><span class="sxs-lookup"><span data-stu-id="4ae15-142">Elements</span></span>](create-uidefinition-elements.md)
- [<span data-ttu-id="4ae15-143">Functions</span><span class="sxs-lookup"><span data-stu-id="4ae15-143">Functions</span></span>](create-uidefinition-functions.md)

<span data-ttu-id="4ae15-144">A current JSON schema for createUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="4ae15-144">A current JSON schema for createUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span>

<span data-ttu-id="4ae15-145">For an example user interface file, see [createUiDefinition.json](https://github.com/Azure/azure-managedapp-samples/blob/master/samples/201-managed-app-using-existing-vnet/createUiDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="4ae15-145">For an example user interface file, see [createUiDefinition.json](https://github.com/Azure/azure-managedapp-samples/blob/master/samples/201-managed-app-using-existing-vnet/createUiDefinition.json).</span></span>
