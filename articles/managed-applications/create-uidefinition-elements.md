---
title: Azure create UI definition element | Microsoft Docs
description: Describes the elements to use when constructing UI definitions for Azure portal.
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2018
ms.author: tomfitz
ms.openlocfilehash: 0a69f46294fc370b1eb403440af5bb3c25ef995d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868931"
---
# <a name="createuidefinition-elements"></a><span data-ttu-id="658b2-103">CreateUiDefinition elements</span><span class="sxs-lookup"><span data-stu-id="658b2-103">CreateUiDefinition elements</span></span>
<span data-ttu-id="658b2-104">This article describes the schema and properties for all supported elements of a CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="658b2-104">This article describes the schema and properties for all supported elements of a CreateUiDefinition.</span></span> 

## <a name="schema"></a><span data-ttu-id="658b2-105">Schema</span><span class="sxs-lookup"><span data-stu-id="658b2-105">Schema</span></span>

<span data-ttu-id="658b2-106">The schema for most elements is as follows:</span><span class="sxs-lookup"><span data-stu-id="658b2-106">The schema for most elements is as follows:</span></span>

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "my value",
  "toolTip": "Provide a descriptive name.",
  "constraints": {},
  "options": {},
  "visible": true
}
```

| <span data-ttu-id="658b2-107">Property</span><span class="sxs-lookup"><span data-stu-id="658b2-107">Property</span></span> | <span data-ttu-id="658b2-108">Required</span><span class="sxs-lookup"><span data-stu-id="658b2-108">Required</span></span> | <span data-ttu-id="658b2-109">Description</span><span class="sxs-lookup"><span data-stu-id="658b2-109">Description</span></span> |
| -------- | -------- | ----------- |
| <span data-ttu-id="658b2-110">name</span><span class="sxs-lookup"><span data-stu-id="658b2-110">name</span></span> | <span data-ttu-id="658b2-111">Yes</span><span class="sxs-lookup"><span data-stu-id="658b2-111">Yes</span></span> | <span data-ttu-id="658b2-112">An internal identifier to reference a specific instance of an element.</span><span class="sxs-lookup"><span data-stu-id="658b2-112">An internal identifier to reference a specific instance of an element.</span></span> <span data-ttu-id="658b2-113">The most common usage of the element name is in `outputs`, where the output values of the specified elements are mapped to the parameters of the template.</span><span class="sxs-lookup"><span data-stu-id="658b2-113">The most common usage of the element name is in `outputs`, where the output values of the specified elements are mapped to the parameters of the template.</span></span> <span data-ttu-id="658b2-114">You can also use it to bind the output value of an element to the `defaultValue` of another element.</span><span class="sxs-lookup"><span data-stu-id="658b2-114">You can also use it to bind the output value of an element to the `defaultValue` of another element.</span></span> |
| <span data-ttu-id="658b2-115">type</span><span class="sxs-lookup"><span data-stu-id="658b2-115">type</span></span> | <span data-ttu-id="658b2-116">Yes</span><span class="sxs-lookup"><span data-stu-id="658b2-116">Yes</span></span> | <span data-ttu-id="658b2-117">The UI control to render for the element.</span><span class="sxs-lookup"><span data-stu-id="658b2-117">The UI control to render for the element.</span></span> <span data-ttu-id="658b2-118">For a list of supported types, see [Elements](#elements).</span><span class="sxs-lookup"><span data-stu-id="658b2-118">For a list of supported types, see [Elements](#elements).</span></span> |
| <span data-ttu-id="658b2-119">label</span><span class="sxs-lookup"><span data-stu-id="658b2-119">label</span></span> | <span data-ttu-id="658b2-120">Yes</span><span class="sxs-lookup"><span data-stu-id="658b2-120">Yes</span></span> | <span data-ttu-id="658b2-121">The display text of the element.</span><span class="sxs-lookup"><span data-stu-id="658b2-121">The display text of the element.</span></span> <span data-ttu-id="658b2-122">Some element types contain multiple labels, so the value could be an object containing multiple strings.</span><span class="sxs-lookup"><span data-stu-id="658b2-122">Some element types contain multiple labels, so the value could be an object containing multiple strings.</span></span> |
| <span data-ttu-id="658b2-123">defaultValue</span><span class="sxs-lookup"><span data-stu-id="658b2-123">defaultValue</span></span> | <span data-ttu-id="658b2-124">No</span><span class="sxs-lookup"><span data-stu-id="658b2-124">No</span></span> | <span data-ttu-id="658b2-125">The default value of the element.</span><span class="sxs-lookup"><span data-stu-id="658b2-125">The default value of the element.</span></span> <span data-ttu-id="658b2-126">Some element types support complex default values, so the value could be an object.</span><span class="sxs-lookup"><span data-stu-id="658b2-126">Some element types support complex default values, so the value could be an object.</span></span> |
| <span data-ttu-id="658b2-127">toolTip</span><span class="sxs-lookup"><span data-stu-id="658b2-127">toolTip</span></span> | <span data-ttu-id="658b2-128">No</span><span class="sxs-lookup"><span data-stu-id="658b2-128">No</span></span> | <span data-ttu-id="658b2-129">The text to display in the tool tip of the element.</span><span class="sxs-lookup"><span data-stu-id="658b2-129">The text to display in the tool tip of the element.</span></span> <span data-ttu-id="658b2-130">Similar to `label`, some elements support multiple tool tip strings.</span><span class="sxs-lookup"><span data-stu-id="658b2-130">Similar to `label`, some elements support multiple tool tip strings.</span></span> <span data-ttu-id="658b2-131">Inline links can be embedded using Markdown syntax.</span><span class="sxs-lookup"><span data-stu-id="658b2-131">Inline links can be embedded using Markdown syntax.</span></span>
| <span data-ttu-id="658b2-132">constraints</span><span class="sxs-lookup"><span data-stu-id="658b2-132">constraints</span></span> | <span data-ttu-id="658b2-133">No</span><span class="sxs-lookup"><span data-stu-id="658b2-133">No</span></span> | <span data-ttu-id="658b2-134">One or more properties that are used to customize the validation behavior of the element.</span><span class="sxs-lookup"><span data-stu-id="658b2-134">One or more properties that are used to customize the validation behavior of the element.</span></span> <span data-ttu-id="658b2-135">The supported properties for constraints vary by element type.</span><span class="sxs-lookup"><span data-stu-id="658b2-135">The supported properties for constraints vary by element type.</span></span> <span data-ttu-id="658b2-136">Some element types do not support customization of the validation behavior, and thus have no constraints property.</span><span class="sxs-lookup"><span data-stu-id="658b2-136">Some element types do not support customization of the validation behavior, and thus have no constraints property.</span></span> |
| <span data-ttu-id="658b2-137">options</span><span class="sxs-lookup"><span data-stu-id="658b2-137">options</span></span> | <span data-ttu-id="658b2-138">No</span><span class="sxs-lookup"><span data-stu-id="658b2-138">No</span></span> | <span data-ttu-id="658b2-139">Additional properties that customize the behavior of the element.</span><span class="sxs-lookup"><span data-stu-id="658b2-139">Additional properties that customize the behavior of the element.</span></span> <span data-ttu-id="658b2-140">Similar to `constraints`, the supported properties vary by element type.</span><span class="sxs-lookup"><span data-stu-id="658b2-140">Similar to `constraints`, the supported properties vary by element type.</span></span> |
| <span data-ttu-id="658b2-141">visible</span><span class="sxs-lookup"><span data-stu-id="658b2-141">visible</span></span> | <span data-ttu-id="658b2-142">No</span><span class="sxs-lookup"><span data-stu-id="658b2-142">No</span></span> | <span data-ttu-id="658b2-143">Indicates whether the element is displayed.</span><span class="sxs-lookup"><span data-stu-id="658b2-143">Indicates whether the element is displayed.</span></span> <span data-ttu-id="658b2-144">If `true`, the element and applicable child elements are displayed.</span><span class="sxs-lookup"><span data-stu-id="658b2-144">If `true`, the element and applicable child elements are displayed.</span></span> <span data-ttu-id="658b2-145">The default value is `true`.</span><span class="sxs-lookup"><span data-stu-id="658b2-145">The default value is `true`.</span></span> <span data-ttu-id="658b2-146">Use [logical functions](create-uidefinition-functions.md#logical-functions) to dynamically control this property's value.</span><span class="sxs-lookup"><span data-stu-id="658b2-146">Use [logical functions](create-uidefinition-functions.md#logical-functions) to dynamically control this property's value.</span></span>

## <a name="elements"></a><span data-ttu-id="658b2-147">Elements</span><span class="sxs-lookup"><span data-stu-id="658b2-147">Elements</span></span>

<span data-ttu-id="658b2-148">The documentation for each element contains a UI sample, schema, remarks on the behavior of the element (usually concerning validation and supported customization), and sample output.</span><span class="sxs-lookup"><span data-stu-id="658b2-148">The documentation for each element contains a UI sample, schema, remarks on the behavior of the element (usually concerning validation and supported customization), and sample output.</span></span>

- [<span data-ttu-id="658b2-149">Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="658b2-149">Microsoft.Common.DropDown</span></span>](microsoft-common-dropdown.md)
- [<span data-ttu-id="658b2-150">Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="658b2-150">Microsoft.Common.FileUpload</span></span>](microsoft-common-fileupload.md)
- [<span data-ttu-id="658b2-151">Microsoft.Common.InfoBox</span><span class="sxs-lookup"><span data-stu-id="658b2-151">Microsoft.Common.InfoBox</span></span>](microsoft-common-infobox.md)
- [<span data-ttu-id="658b2-152">Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="658b2-152">Microsoft.Common.OptionsGroup</span></span>](microsoft-common-optionsgroup.md)
- [<span data-ttu-id="658b2-153">Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="658b2-153">Microsoft.Common.PasswordBox</span></span>](microsoft-common-passwordbox.md)
- [<span data-ttu-id="658b2-154">Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="658b2-154">Microsoft.Common.Section</span></span>](microsoft-common-section.md)
- [<span data-ttu-id="658b2-155">Microsoft.Common.TextBlock</span><span class="sxs-lookup"><span data-stu-id="658b2-155">Microsoft.Common.TextBlock</span></span>](microsoft-common-textblock.md)
- [<span data-ttu-id="658b2-156">Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="658b2-156">Microsoft.Common.TextBox</span></span>](microsoft-common-textbox.md)
- [<span data-ttu-id="658b2-157">Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="658b2-157">Microsoft.Compute.CredentialsCombo</span></span>](microsoft-compute-credentialscombo.md)
- [<span data-ttu-id="658b2-158">Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="658b2-158">Microsoft.Compute.SizeSelector</span></span>](microsoft-compute-sizeselector.md)
- [<span data-ttu-id="658b2-159">Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="658b2-159">Microsoft.Compute.UserNameTextBox</span></span>](microsoft-compute-usernametextbox.md)
- [<span data-ttu-id="658b2-160">Microsoft.Network.AvailabilityZoneDropDown</span><span class="sxs-lookup"><span data-stu-id="658b2-160">Microsoft.Network.AvailabilityZoneDropDown</span></span>](microsoft-network-availabilityzonedropdown.md)
- [<span data-ttu-id="658b2-161">Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="658b2-161">Microsoft.Network.PublicIpAddressCombo</span></span>](microsoft-network-publicipaddresscombo.md)
- [<span data-ttu-id="658b2-162">Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="658b2-162">Microsoft.Network.VirtualNetworkCombo</span></span>](microsoft-network-virtualnetworkcombo.md)
- [<span data-ttu-id="658b2-163">Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="658b2-163">Microsoft.Storage.MultiStorageAccountCombo</span></span>](microsoft-storage-multistorageaccountcombo.md)
- [<span data-ttu-id="658b2-164">Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="658b2-164">Microsoft.Storage.StorageAccountSelector</span></span>](microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a><span data-ttu-id="658b2-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="658b2-165">Next steps</span></span>
<span data-ttu-id="658b2-166">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="658b2-166">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
