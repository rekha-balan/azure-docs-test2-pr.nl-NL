---
title: Create custom artifacts for your DevTest Labs virtual machine | Microsoft Docs
description: Learn how to author your own artifacts to use with Azure DevTest Labs.
services: devtest-lab,virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2018
ms.author: spelluru
ms.openlocfilehash: ad9e9e893dc831530b69a30cc3dd930e879e9d7b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868184"
---
# <a name="create-custom-artifacts-for-your-devtest-labs-virtual-machine"></a><span data-ttu-id="b23f6-103">Create custom artifacts for your DevTest Labs virtual machine</span><span class="sxs-lookup"><span data-stu-id="b23f6-103">Create custom artifacts for your DevTest Labs virtual machine</span></span>

<span data-ttu-id="b23f6-104">Watch the following video for an overview of the steps described in this article:</span><span class="sxs-lookup"><span data-stu-id="b23f6-104">Watch the following video for an overview of the steps described in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="b23f6-105">Overview</span><span class="sxs-lookup"><span data-stu-id="b23f6-105">Overview</span></span>
<span data-ttu-id="b23f6-106">You can use *artifacts* to deploy and set up your application after you provision a VM.</span><span class="sxs-lookup"><span data-stu-id="b23f6-106">You can use *artifacts* to deploy and set up your application after you provision a VM.</span></span> <span data-ttu-id="b23f6-107">An artifact consists of an artifact definition file and other script files that are stored in a folder in a Git repository.</span><span class="sxs-lookup"><span data-stu-id="b23f6-107">An artifact consists of an artifact definition file and other script files that are stored in a folder in a Git repository.</span></span> <span data-ttu-id="b23f6-108">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span><span class="sxs-lookup"><span data-stu-id="b23f6-108">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span></span> <span data-ttu-id="b23f6-109">For example, you can define the name of an artifact, a command to run, and parameters that are available when the command is run.</span><span class="sxs-lookup"><span data-stu-id="b23f6-109">For example, you can define the name of an artifact, a command to run, and parameters that are available when the command is run.</span></span> <span data-ttu-id="b23f6-110">You can refer to other script files within the artifact definition file by name.</span><span class="sxs-lookup"><span data-stu-id="b23f6-110">You can refer to other script files within the artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="b23f6-111">Artifact definition file format</span><span class="sxs-lookup"><span data-stu-id="b23f6-111">Artifact definition file format</span></span>
<span data-ttu-id="b23f6-112">The following example shows the sections that make up the basic structure of a definition file:</span><span class="sxs-lookup"><span data-stu-id="b23f6-112">The following example shows the sections that make up the basic structure of a definition file:</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| <span data-ttu-id="b23f6-113">Element name</span><span class="sxs-lookup"><span data-stu-id="b23f6-113">Element name</span></span> | <span data-ttu-id="b23f6-114">Required?</span><span class="sxs-lookup"><span data-stu-id="b23f6-114">Required?</span></span> | <span data-ttu-id="b23f6-115">Description</span><span class="sxs-lookup"><span data-stu-id="b23f6-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b23f6-116">$schema</span><span class="sxs-lookup"><span data-stu-id="b23f6-116">$schema</span></span> |<span data-ttu-id="b23f6-117">No</span><span class="sxs-lookup"><span data-stu-id="b23f6-117">No</span></span> |<span data-ttu-id="b23f6-118">Location of the JSON schema file.</span><span class="sxs-lookup"><span data-stu-id="b23f6-118">Location of the JSON schema file.</span></span> <span data-ttu-id="b23f6-119">The JSON schema file can help you test the validity of the definition file.</span><span class="sxs-lookup"><span data-stu-id="b23f6-119">The JSON schema file can help you test the validity of the definition file.</span></span> |
| <span data-ttu-id="b23f6-120">title</span><span class="sxs-lookup"><span data-stu-id="b23f6-120">title</span></span> |<span data-ttu-id="b23f6-121">Yes</span><span class="sxs-lookup"><span data-stu-id="b23f6-121">Yes</span></span> |<span data-ttu-id="b23f6-122">Name of the artifact displayed in the lab.</span><span class="sxs-lookup"><span data-stu-id="b23f6-122">Name of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="b23f6-123">description</span><span class="sxs-lookup"><span data-stu-id="b23f6-123">description</span></span> |<span data-ttu-id="b23f6-124">Yes</span><span class="sxs-lookup"><span data-stu-id="b23f6-124">Yes</span></span> |<span data-ttu-id="b23f6-125">Description of the artifact displayed in the lab.</span><span class="sxs-lookup"><span data-stu-id="b23f6-125">Description of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="b23f6-126">iconUri</span><span class="sxs-lookup"><span data-stu-id="b23f6-126">iconUri</span></span> |<span data-ttu-id="b23f6-127">No</span><span class="sxs-lookup"><span data-stu-id="b23f6-127">No</span></span> |<span data-ttu-id="b23f6-128">URI of the icon displayed in the lab.</span><span class="sxs-lookup"><span data-stu-id="b23f6-128">URI of the icon displayed in the lab.</span></span> |
| <span data-ttu-id="b23f6-129">targetOsType</span><span class="sxs-lookup"><span data-stu-id="b23f6-129">targetOsType</span></span> |<span data-ttu-id="b23f6-130">Yes</span><span class="sxs-lookup"><span data-stu-id="b23f6-130">Yes</span></span> |<span data-ttu-id="b23f6-131">Operating system of the VM where the artifact is installed.</span><span class="sxs-lookup"><span data-stu-id="b23f6-131">Operating system of the VM where the artifact is installed.</span></span> <span data-ttu-id="b23f6-132">Supported options are Windows and Linux.</span><span class="sxs-lookup"><span data-stu-id="b23f6-132">Supported options are Windows and Linux.</span></span> |
| <span data-ttu-id="b23f6-133">parameters</span><span class="sxs-lookup"><span data-stu-id="b23f6-133">parameters</span></span> |<span data-ttu-id="b23f6-134">No</span><span class="sxs-lookup"><span data-stu-id="b23f6-134">No</span></span> |<span data-ttu-id="b23f6-135">Values that are provided when the artifact install command is run on a machine.</span><span class="sxs-lookup"><span data-stu-id="b23f6-135">Values that are provided when the artifact install command is run on a machine.</span></span> <span data-ttu-id="b23f6-136">This helps you customize your artifact.</span><span class="sxs-lookup"><span data-stu-id="b23f6-136">This helps you customize your artifact.</span></span> |
| <span data-ttu-id="b23f6-137">runCommand</span><span class="sxs-lookup"><span data-stu-id="b23f6-137">runCommand</span></span> |<span data-ttu-id="b23f6-138">Yes</span><span class="sxs-lookup"><span data-stu-id="b23f6-138">Yes</span></span> |<span data-ttu-id="b23f6-139">Artifact install command that is executed on a VM.</span><span class="sxs-lookup"><span data-stu-id="b23f6-139">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="b23f6-140">Artifact parameters</span><span class="sxs-lookup"><span data-stu-id="b23f6-140">Artifact parameters</span></span>
<span data-ttu-id="b23f6-141">In the parameters section of the definition file, specify which values a user can input when they install an artifact.</span><span class="sxs-lookup"><span data-stu-id="b23f6-141">In the parameters section of the definition file, specify which values a user can input when they install an artifact.</span></span> <span data-ttu-id="b23f6-142">You can refer to these values in the artifact install command.</span><span class="sxs-lookup"><span data-stu-id="b23f6-142">You can refer to these values in the artifact install command.</span></span>

<span data-ttu-id="b23f6-143">To define parameters, use the following structure:</span><span class="sxs-lookup"><span data-stu-id="b23f6-143">To define parameters, use the following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="b23f6-144">Element name</span><span class="sxs-lookup"><span data-stu-id="b23f6-144">Element name</span></span> | <span data-ttu-id="b23f6-145">Required?</span><span class="sxs-lookup"><span data-stu-id="b23f6-145">Required?</span></span> | <span data-ttu-id="b23f6-146">Description</span><span class="sxs-lookup"><span data-stu-id="b23f6-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b23f6-147">type</span><span class="sxs-lookup"><span data-stu-id="b23f6-147">type</span></span> |<span data-ttu-id="b23f6-148">Yes</span><span class="sxs-lookup"><span data-stu-id="b23f6-148">Yes</span></span> |<span data-ttu-id="b23f6-149">Type of parameter value.</span><span class="sxs-lookup"><span data-stu-id="b23f6-149">Type of parameter value.</span></span> <span data-ttu-id="b23f6-150">See the following list for the allowed types.</span><span class="sxs-lookup"><span data-stu-id="b23f6-150">See the following list for the allowed types.</span></span> |
| <span data-ttu-id="b23f6-151">displayName</span><span class="sxs-lookup"><span data-stu-id="b23f6-151">displayName</span></span> |<span data-ttu-id="b23f6-152">Yes</span><span class="sxs-lookup"><span data-stu-id="b23f6-152">Yes</span></span> |<span data-ttu-id="b23f6-153">Name of the parameter that is displayed to a user in the lab.</span><span class="sxs-lookup"><span data-stu-id="b23f6-153">Name of the parameter that is displayed to a user in the lab.</span></span> | |
| <span data-ttu-id="b23f6-154">description</span><span class="sxs-lookup"><span data-stu-id="b23f6-154">description</span></span> |<span data-ttu-id="b23f6-155">Yes</span><span class="sxs-lookup"><span data-stu-id="b23f6-155">Yes</span></span> |<span data-ttu-id="b23f6-156">Description of the parameter that is displayed in the lab.</span><span class="sxs-lookup"><span data-stu-id="b23f6-156">Description of the parameter that is displayed in the lab.</span></span> |

<span data-ttu-id="b23f6-157">Allowed types are:</span><span class="sxs-lookup"><span data-stu-id="b23f6-157">Allowed types are:</span></span>

* <span data-ttu-id="b23f6-158">string (any valid JSON string)</span><span class="sxs-lookup"><span data-stu-id="b23f6-158">string (any valid JSON string)</span></span>
* <span data-ttu-id="b23f6-159">int (any valid JSON integer)</span><span class="sxs-lookup"><span data-stu-id="b23f6-159">int (any valid JSON integer)</span></span>
* <span data-ttu-id="b23f6-160">bool (any valid JSON Boolean)</span><span class="sxs-lookup"><span data-stu-id="b23f6-160">bool (any valid JSON Boolean)</span></span>
* <span data-ttu-id="b23f6-161">array (any valid JSON array)</span><span class="sxs-lookup"><span data-stu-id="b23f6-161">array (any valid JSON array)</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="b23f6-162">Artifact expressions and functions</span><span class="sxs-lookup"><span data-stu-id="b23f6-162">Artifact expressions and functions</span></span>
<span data-ttu-id="b23f6-163">You can use expressions and functions to construct the artifact install command.</span><span class="sxs-lookup"><span data-stu-id="b23f6-163">You can use expressions and functions to construct the artifact install command.</span></span>
<span data-ttu-id="b23f6-164">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span><span class="sxs-lookup"><span data-stu-id="b23f6-164">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span></span> <span data-ttu-id="b23f6-165">Expressions can appear anywhere in a JSON string value.</span><span class="sxs-lookup"><span data-stu-id="b23f6-165">Expressions can appear anywhere in a JSON string value.</span></span> <span data-ttu-id="b23f6-166">Expressions always return another JSON value.</span><span class="sxs-lookup"><span data-stu-id="b23f6-166">Expressions always return another JSON value.</span></span> <span data-ttu-id="b23f6-167">If you need to use a literal string that starts with a bracket ([), you must use two brackets ([[).</span><span class="sxs-lookup"><span data-stu-id="b23f6-167">If you need to use a literal string that starts with a bracket ([), you must use two brackets ([[).</span></span>
<span data-ttu-id="b23f6-168">Typically, you use expressions with functions to construct a value.</span><span class="sxs-lookup"><span data-stu-id="b23f6-168">Typically, you use expressions with functions to construct a value.</span></span> <span data-ttu-id="b23f6-169">Just like in JavaScript, function calls are formatted as **functionName(arg1, arg2, arg3)**.</span><span class="sxs-lookup"><span data-stu-id="b23f6-169">Just like in JavaScript, function calls are formatted as **functionName(arg1, arg2, arg3)**.</span></span>

<span data-ttu-id="b23f6-170">The following list shows common functions:</span><span class="sxs-lookup"><span data-stu-id="b23f6-170">The following list shows common functions:</span></span>

* <span data-ttu-id="b23f6-171">**parameters(parameterName)**: Returns a parameter value that is provided when the artifact command is run.</span><span class="sxs-lookup"><span data-stu-id="b23f6-171">**parameters(parameterName)**: Returns a parameter value that is provided when the artifact command is run.</span></span>
* <span data-ttu-id="b23f6-172">**concat(arg1, arg2, arg3,….. )**: Combines multiple string values.</span><span class="sxs-lookup"><span data-stu-id="b23f6-172">**concat(arg1, arg2, arg3,….. )**: Combines multiple string values.</span></span> <span data-ttu-id="b23f6-173">This function can take a variety of arguments.</span><span class="sxs-lookup"><span data-stu-id="b23f6-173">This function can take a variety of arguments.</span></span>

<span data-ttu-id="b23f6-174">The following example shows how to use expressions and functions to construct a value:</span><span class="sxs-lookup"><span data-stu-id="b23f6-174">The following example shows how to use expressions and functions to construct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="b23f6-175">Create a custom artifact</span><span class="sxs-lookup"><span data-stu-id="b23f6-175">Create a custom artifact</span></span>

1. <span data-ttu-id="b23f6-176">Install a JSON editor.</span><span class="sxs-lookup"><span data-stu-id="b23f6-176">Install a JSON editor.</span></span> <span data-ttu-id="b23f6-177">You need a JSON editor to work with artifact definition files.</span><span class="sxs-lookup"><span data-stu-id="b23f6-177">You need a JSON editor to work with artifact definition files.</span></span> <span data-ttu-id="b23f6-178">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux, and OS X.</span><span class="sxs-lookup"><span data-stu-id="b23f6-178">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux, and OS X.</span></span>
2. <span data-ttu-id="b23f6-179">Get a sample artifactfile.json definition file.</span><span class="sxs-lookup"><span data-stu-id="b23f6-179">Get a sample artifactfile.json definition file.</span></span> <span data-ttu-id="b23f6-180">Check out the artifacts created by the DevTest Labs team in our [GitHub repository](https://github.com/Azure/azure-devtestlab).</span><span class="sxs-lookup"><span data-stu-id="b23f6-180">Check out the artifacts created by the DevTest Labs team in our [GitHub repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="b23f6-181">We have created a rich library of artifacts that can help you create your own artifacts.</span><span class="sxs-lookup"><span data-stu-id="b23f6-181">We have created a rich library of artifacts that can help you create your own artifacts.</span></span> <span data-ttu-id="b23f6-182">Download an artifact definition file and make changes to it to create your own artifacts.</span><span class="sxs-lookup"><span data-stu-id="b23f6-182">Download an artifact definition file and make changes to it to create your own artifacts.</span></span>
3. <span data-ttu-id="b23f6-183">Make use of IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="b23f6-183">Make use of IntelliSense.</span></span> <span data-ttu-id="b23f6-184">Use IntelliSense to see valid elements that you can use to construct an artifact definition file.</span><span class="sxs-lookup"><span data-stu-id="b23f6-184">Use IntelliSense to see valid elements that you can use to construct an artifact definition file.</span></span> <span data-ttu-id="b23f6-185">You also can see the different options for values of an element.</span><span class="sxs-lookup"><span data-stu-id="b23f6-185">You also can see the different options for values of an element.</span></span> <span data-ttu-id="b23f6-186">For example, when you edit the **targetOsType** element, IntelliSense shows you two choices, for Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="b23f6-186">For example, when you edit the **targetOsType** element, IntelliSense shows you two choices, for Windows or Linux.</span></span>
4. <span data-ttu-id="b23f6-187">Store the artifact in the [public Git repository for DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) or [your own Git repository](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="b23f6-187">Store the artifact in the [public Git repository for DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) or [your own Git repository](devtest-lab-add-artifact-repo.md).</span></span> <span data-ttu-id="b23f6-188">In the public repository, you can view artifacts shared by others that you can use directly or customize them to suit your needs.</span><span class="sxs-lookup"><span data-stu-id="b23f6-188">In the public repository, you can view artifacts shared by others that you can use directly or customize them to suit your needs.</span></span> 
   
   1. <span data-ttu-id="b23f6-189">Create a separate directory for each artifact.</span><span class="sxs-lookup"><span data-stu-id="b23f6-189">Create a separate directory for each artifact.</span></span> <span data-ttu-id="b23f6-190">The directory name should be the same as the artifact name.</span><span class="sxs-lookup"><span data-stu-id="b23f6-190">The directory name should be the same as the artifact name.</span></span>
   2. <span data-ttu-id="b23f6-191">Store the artifact definition file (artifactfile.json) in the directory that you created.</span><span class="sxs-lookup"><span data-stu-id="b23f6-191">Store the artifact definition file (artifactfile.json) in the directory that you created.</span></span>
   3. <span data-ttu-id="b23f6-192">Store the scripts that are referenced from the artifact install command.</span><span class="sxs-lookup"><span data-stu-id="b23f6-192">Store the scripts that are referenced from the artifact install command.</span></span>
      
      <span data-ttu-id="b23f6-193">Here is an example of how an artifact folder might look:</span><span class="sxs-lookup"><span data-stu-id="b23f6-193">Here is an example of how an artifact folder might look:</span></span>
      
      ![Artifact folder example](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="b23f6-195">If you are using your own repository to store artifacts, add the repository to the lab by following instructions in the article: [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="b23f6-195">If you are using your own repository to store artifacts, add the repository to the lab by following instructions in the article: [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>


## <a name="related-articles"></a><span data-ttu-id="b23f6-196">Related articles</span><span class="sxs-lookup"><span data-stu-id="b23f6-196">Related articles</span></span>
* [<span data-ttu-id="b23f6-197">How to diagnose artifact failures in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b23f6-197">How to diagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="b23f6-198">Join a VM to an existing Active Directory domain by using a Resource Manager template in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b23f6-198">Join a VM to an existing Active Directory domain by using a Resource Manager template in DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="b23f6-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="b23f6-199">Next steps</span></span>
* <span data-ttu-id="b23f6-200">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="b23f6-200">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

