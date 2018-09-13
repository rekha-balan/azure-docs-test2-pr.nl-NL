---
title: Test the UI definition for Azure Managed Applications | Microsoft Docs
description: Describes how to test the user experience for creating your Azure Managed Application through the portal.
services: managed-applications
documentationcenter: na
author: tfitzmac
ms.service: managed-applications
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2018
ms.author: tomfitz
ms.openlocfilehash: c88bdce64e88f8639da2c4ebb01f4594fccff8a0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864556"
---
# <a name="test-azure-portal-interface-for-your-managed-application"></a><span data-ttu-id="1c806-103">Test Azure portal interface for your managed application</span><span class="sxs-lookup"><span data-stu-id="1c806-103">Test Azure portal interface for your managed application</span></span>
<span data-ttu-id="1c806-104">After [creating the createUiDefinition.json file](create-uidefinition-overview.md) for your Azure Managed Application, you need to test the user experience.</span><span class="sxs-lookup"><span data-stu-id="1c806-104">After [creating the createUiDefinition.json file](create-uidefinition-overview.md) for your Azure Managed Application, you need to test the user experience.</span></span> <span data-ttu-id="1c806-105">To simplify testing, use a script that loads your file in the portal.</span><span class="sxs-lookup"><span data-stu-id="1c806-105">To simplify testing, use a script that loads your file in the portal.</span></span> <span data-ttu-id="1c806-106">You don't need to actually deploy your managed application.</span><span class="sxs-lookup"><span data-stu-id="1c806-106">You don't need to actually deploy your managed application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c806-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1c806-107">Prerequisites</span></span>

* <span data-ttu-id="1c806-108">A **createUiDefinition.json** file.</span><span class="sxs-lookup"><span data-stu-id="1c806-108">A **createUiDefinition.json** file.</span></span> <span data-ttu-id="1c806-109">If you don't have this file, copy the [sample file](https://github.com/Azure/azure-quickstart-templates/blob/master/100-marketplace-sample/createUiDefinition.json) and save it locally.</span><span class="sxs-lookup"><span data-stu-id="1c806-109">If you don't have this file, copy the [sample file](https://github.com/Azure/azure-quickstart-templates/blob/master/100-marketplace-sample/createUiDefinition.json) and save it locally.</span></span>

* <span data-ttu-id="1c806-110">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1c806-110">An Azure subscription.</span></span> <span data-ttu-id="1c806-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="1c806-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="download-test-script"></a><span data-ttu-id="1c806-112">Download test script</span><span class="sxs-lookup"><span data-stu-id="1c806-112">Download test script</span></span>

<span data-ttu-id="1c806-113">To test your interface in the portal, copy one of the following scripts to your local machine:</span><span class="sxs-lookup"><span data-stu-id="1c806-113">To test your interface in the portal, copy one of the following scripts to your local machine:</span></span>

* [<span data-ttu-id="1c806-114">PowerShell side-load script</span><span class="sxs-lookup"><span data-stu-id="1c806-114">PowerShell side-load script</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/SideLoad-CreateUIDefinition.ps1)
* [<span data-ttu-id="1c806-115">Azure CLI side-load script</span><span class="sxs-lookup"><span data-stu-id="1c806-115">Azure CLI side-load script</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/sideload-createuidef.sh)

## <a name="run-script"></a><span data-ttu-id="1c806-116">Run script</span><span class="sxs-lookup"><span data-stu-id="1c806-116">Run script</span></span>

<span data-ttu-id="1c806-117">To see your interface file in the portal, run your downloaded script.</span><span class="sxs-lookup"><span data-stu-id="1c806-117">To see your interface file in the portal, run your downloaded script.</span></span> <span data-ttu-id="1c806-118">The script creates a storage account in your Azure subscription, and uploads your createUiDefinition.json file to the storage account.</span><span class="sxs-lookup"><span data-stu-id="1c806-118">The script creates a storage account in your Azure subscription, and uploads your createUiDefinition.json file to the storage account.</span></span> <span data-ttu-id="1c806-119">The storage account is created the first time you run the script or if the storage account has been deleted.</span><span class="sxs-lookup"><span data-stu-id="1c806-119">The storage account is created the first time you run the script or if the storage account has been deleted.</span></span> <span data-ttu-id="1c806-120">If the storage account already exists in your Azure subscription, the script reuses it.</span><span class="sxs-lookup"><span data-stu-id="1c806-120">If the storage account already exists in your Azure subscription, the script reuses it.</span></span> <span data-ttu-id="1c806-121">The script opens the portal and loads your file from the storage account.</span><span class="sxs-lookup"><span data-stu-id="1c806-121">The script opens the portal and loads your file from the storage account.</span></span>

<span data-ttu-id="1c806-122">Provide a location for the storage account, and specify the folder that has your createUiDefinition.json file.</span><span class="sxs-lookup"><span data-stu-id="1c806-122">Provide a location for the storage account, and specify the folder that has your createUiDefinition.json file.</span></span>

<span data-ttu-id="1c806-123">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="1c806-123">For PowerShell, use:</span></span>

```powershell
.\SideLoad-CreateUIDefinition.ps1 `
  -StorageResourceGroupLocation southcentralus `
  -ArtifactsStagingDirectory .\100-Marketplace-Sample
```

<span data-ttu-id="1c806-124">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="1c806-124">For Azure CLI, use:</span></span>

```azurecli
./sideload-createuidef.sh \
  -l southcentralus \
  -a .\100-Marketplace-Sample
```

<span data-ttu-id="1c806-125">If your createUiDefinition.json file is in the same folder as the script, and you've already created the storage account, you don't need to provide those parameters.</span><span class="sxs-lookup"><span data-stu-id="1c806-125">If your createUiDefinition.json file is in the same folder as the script, and you've already created the storage account, you don't need to provide those parameters.</span></span>

<span data-ttu-id="1c806-126">For PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="1c806-126">For PowerShell, use:</span></span>

```powershell
.\SideLoad-CreateUIDefinition.ps1
```

<span data-ttu-id="1c806-127">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="1c806-127">For Azure CLI, use:</span></span>

```azurecli
./sideload-createuidef.sh
```

## <a name="test-your-interface"></a><span data-ttu-id="1c806-128">Test your interface</span><span class="sxs-lookup"><span data-stu-id="1c806-128">Test your interface</span></span>

<span data-ttu-id="1c806-129">The script opens a new tab in your browser.</span><span class="sxs-lookup"><span data-stu-id="1c806-129">The script opens a new tab in your browser.</span></span> <span data-ttu-id="1c806-130">It displays the portal with your interface for creating the managed application.</span><span class="sxs-lookup"><span data-stu-id="1c806-130">It displays the portal with your interface for creating the managed application.</span></span>

![View portal](./media/test-createuidefinition/view-portal.png)

<span data-ttu-id="1c806-132">Before filling out the fields, open the Web Developer Tools in your browser.</span><span class="sxs-lookup"><span data-stu-id="1c806-132">Before filling out the fields, open the Web Developer Tools in your browser.</span></span> <span data-ttu-id="1c806-133">The **Console** displays important messages about your interface.</span><span class="sxs-lookup"><span data-stu-id="1c806-133">The **Console** displays important messages about your interface.</span></span>

![Select console](./media/test-createuidefinition/select-console.png)

<span data-ttu-id="1c806-135">If your interface definition has an error, you see the description in the console.</span><span class="sxs-lookup"><span data-stu-id="1c806-135">If your interface definition has an error, you see the description in the console.</span></span>

![Show error](./media/test-createuidefinition/show-error.png)

<span data-ttu-id="1c806-137">Provide values for the fields.</span><span class="sxs-lookup"><span data-stu-id="1c806-137">Provide values for the fields.</span></span> <span data-ttu-id="1c806-138">When finished, you see the values that are passed to the template.</span><span class="sxs-lookup"><span data-stu-id="1c806-138">When finished, you see the values that are passed to the template.</span></span>

![Show values](./media/test-createuidefinition/show-json.png)

<span data-ttu-id="1c806-140">You can use these values as the parameter file for testing your deployment template.</span><span class="sxs-lookup"><span data-stu-id="1c806-140">You can use these values as the parameter file for testing your deployment template.</span></span>

## <a name="troubleshooting-the-interface"></a><span data-ttu-id="1c806-141">Troubleshooting the interface</span><span class="sxs-lookup"><span data-stu-id="1c806-141">Troubleshooting the interface</span></span>

<span data-ttu-id="1c806-142">Some common errors you might see are:</span><span class="sxs-lookup"><span data-stu-id="1c806-142">Some common errors you might see are:</span></span>

* <span data-ttu-id="1c806-143">The portal doesn't load your interface.</span><span class="sxs-lookup"><span data-stu-id="1c806-143">The portal doesn't load your interface.</span></span> <span data-ttu-id="1c806-144">Instead, it shows an icon of a cloud with tear drop.</span><span class="sxs-lookup"><span data-stu-id="1c806-144">Instead, it shows an icon of a cloud with tear drop.</span></span> <span data-ttu-id="1c806-145">Usually, you see this icon when there's a syntax error in your file.</span><span class="sxs-lookup"><span data-stu-id="1c806-145">Usually, you see this icon when there's a syntax error in your file.</span></span> <span data-ttu-id="1c806-146">Open the file in VS Code (or other JSON editor that has schema validation) and look for syntax errors.</span><span class="sxs-lookup"><span data-stu-id="1c806-146">Open the file in VS Code (or other JSON editor that has schema validation) and look for syntax errors.</span></span>

* <span data-ttu-id="1c806-147">The portal hangs at the summary screen.</span><span class="sxs-lookup"><span data-stu-id="1c806-147">The portal hangs at the summary screen.</span></span> <span data-ttu-id="1c806-148">Usually, this interruption happens when there's a bug in the output section.</span><span class="sxs-lookup"><span data-stu-id="1c806-148">Usually, this interruption happens when there's a bug in the output section.</span></span> <span data-ttu-id="1c806-149">For example, you may have referenced a control that doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="1c806-149">For example, you may have referenced a control that doesn't exist.</span></span>

* <span data-ttu-id="1c806-150">A parameter in the output is empty.</span><span class="sxs-lookup"><span data-stu-id="1c806-150">A parameter in the output is empty.</span></span> <span data-ttu-id="1c806-151">The parameter might be referencing a property that doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="1c806-151">The parameter might be referencing a property that doesn't exist.</span></span> <span data-ttu-id="1c806-152">For example, the reference to the control is valid, but the property reference isn't valid.</span><span class="sxs-lookup"><span data-stu-id="1c806-152">For example, the reference to the control is valid, but the property reference isn't valid.</span></span>

## <a name="test-your-solution-files"></a><span data-ttu-id="1c806-153">Test your solution files</span><span class="sxs-lookup"><span data-stu-id="1c806-153">Test your solution files</span></span>

<span data-ttu-id="1c806-154">Now that you've verified your portal interface is working as expected, it's time to validate that your createUiDefinition file is properly integrated with your mainTemplate.json file.</span><span class="sxs-lookup"><span data-stu-id="1c806-154">Now that you've verified your portal interface is working as expected, it's time to validate that your createUiDefinition file is properly integrated with your mainTemplate.json file.</span></span> <span data-ttu-id="1c806-155">You can run a validation script test to test the content of your solution files, including the createUiDefinition file.</span><span class="sxs-lookup"><span data-stu-id="1c806-155">You can run a validation script test to test the content of your solution files, including the createUiDefinition file.</span></span> <span data-ttu-id="1c806-156">The script validates the JSON syntax, checks for regex expressions on text fields, and makes sure the output values of the portal interface match the parameters of your template.</span><span class="sxs-lookup"><span data-stu-id="1c806-156">The script validates the JSON syntax, checks for regex expressions on text fields, and makes sure the output values of the portal interface match the parameters of your template.</span></span> <span data-ttu-id="1c806-157">For information on running this script, see [Run static validation checks for templates](https://github.com/Azure/azure-quickstart-templates/tree/master/test/template-validation-tests).</span><span class="sxs-lookup"><span data-stu-id="1c806-157">For information on running this script, see [Run static validation checks for templates](https://github.com/Azure/azure-quickstart-templates/tree/master/test/template-validation-tests).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c806-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c806-158">Next steps</span></span>

<span data-ttu-id="1c806-159">After validating your portal interface, learn about making your [Azure managed application available in the Marketplace](publish-marketplace-app.md).</span><span class="sxs-lookup"><span data-stu-id="1c806-159">After validating your portal interface, learn about making your [Azure managed application available in the Marketplace](publish-marketplace-app.md).</span></span>
