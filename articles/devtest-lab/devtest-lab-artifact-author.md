---
title: Create custom artifacts for your DevTest Labs VM | Microsoft Docs
description: Learn how to author your own artifacts for use with DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: c05504de0351ffacb9f1649934cbdfe94e3af28b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548789"
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="3d05b-103">Create custom artifacts for your DevTest Labs VM</span><span class="sxs-lookup"><span data-stu-id="3d05b-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="3d05b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="3d05b-104">Overview</span></span>
<span data-ttu-id="3d05b-105">**Artifacts** are used to deploy and configure your application after a VM is provisioned.</span><span class="sxs-lookup"><span data-stu-id="3d05b-105">**Artifacts** are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="3d05b-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span><span class="sxs-lookup"><span data-stu-id="3d05b-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="3d05b-107">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span><span class="sxs-lookup"><span data-stu-id="3d05b-107">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span></span> <span data-ttu-id="3d05b-108">For example, you can define the name of artifact, command to run, and parameters that are made available when the command is run.</span><span class="sxs-lookup"><span data-stu-id="3d05b-108">For example, you can define the name of artifact, command to run, and parameters that are made available when the command is run.</span></span> <span data-ttu-id="3d05b-109">You can refer to other script files within the artifact definition file by name.</span><span class="sxs-lookup"><span data-stu-id="3d05b-109">You can refer to other script files within the artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="3d05b-110">Artifact definition file format</span><span class="sxs-lookup"><span data-stu-id="3d05b-110">Artifact definition file format</span></span>
<span data-ttu-id="3d05b-111">The following example shows the sections that make up the basic structure of a definition file.</span><span class="sxs-lookup"><span data-stu-id="3d05b-111">The following example shows the sections that make up the basic structure of a definition file.</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2015-01-01/dtlArtifacts.json",
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

| <span data-ttu-id="3d05b-112">Element name</span><span class="sxs-lookup"><span data-stu-id="3d05b-112">Element name</span></span> | <span data-ttu-id="3d05b-113">Required?</span><span class="sxs-lookup"><span data-stu-id="3d05b-113">Required?</span></span> | <span data-ttu-id="3d05b-114">Description</span><span class="sxs-lookup"><span data-stu-id="3d05b-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3d05b-115">$schema</span><span class="sxs-lookup"><span data-stu-id="3d05b-115">$schema</span></span> |<span data-ttu-id="3d05b-116">No</span><span class="sxs-lookup"><span data-stu-id="3d05b-116">No</span></span> |<span data-ttu-id="3d05b-117">Location of the JSON schema file that helps in testing the validity of the definition file.</span><span class="sxs-lookup"><span data-stu-id="3d05b-117">Location of the JSON schema file that helps in testing the validity of the definition file.</span></span> |
| <span data-ttu-id="3d05b-118">title</span><span class="sxs-lookup"><span data-stu-id="3d05b-118">title</span></span> |<span data-ttu-id="3d05b-119">Yes</span><span class="sxs-lookup"><span data-stu-id="3d05b-119">Yes</span></span> |<span data-ttu-id="3d05b-120">Name of the artifact displayed in the lab.</span><span class="sxs-lookup"><span data-stu-id="3d05b-120">Name of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="3d05b-121">description</span><span class="sxs-lookup"><span data-stu-id="3d05b-121">description</span></span> |<span data-ttu-id="3d05b-122">Yes</span><span class="sxs-lookup"><span data-stu-id="3d05b-122">Yes</span></span> |<span data-ttu-id="3d05b-123">Description of the artifact displayed in the lab.</span><span class="sxs-lookup"><span data-stu-id="3d05b-123">Description of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="3d05b-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="3d05b-124">iconUri</span></span> |<span data-ttu-id="3d05b-125">No</span><span class="sxs-lookup"><span data-stu-id="3d05b-125">No</span></span> |<span data-ttu-id="3d05b-126">Uri of the icon displayed in the lab.</span><span class="sxs-lookup"><span data-stu-id="3d05b-126">Uri of the icon displayed in the lab.</span></span> |
| <span data-ttu-id="3d05b-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="3d05b-127">targetOsType</span></span> |<span data-ttu-id="3d05b-128">Yes</span><span class="sxs-lookup"><span data-stu-id="3d05b-128">Yes</span></span> |<span data-ttu-id="3d05b-129">Operating system of the VM where artifact will be installed.</span><span class="sxs-lookup"><span data-stu-id="3d05b-129">Operating system of the VM where artifact will be installed.</span></span> <span data-ttu-id="3d05b-130">Supported options are: Windows and Linux.</span><span class="sxs-lookup"><span data-stu-id="3d05b-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="3d05b-131">parameters</span><span class="sxs-lookup"><span data-stu-id="3d05b-131">parameters</span></span> |<span data-ttu-id="3d05b-132">No</span><span class="sxs-lookup"><span data-stu-id="3d05b-132">No</span></span> |<span data-ttu-id="3d05b-133">Values that are provided when artifact install command is run on a machine.</span><span class="sxs-lookup"><span data-stu-id="3d05b-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="3d05b-134">This helps in customizing your artifact.</span><span class="sxs-lookup"><span data-stu-id="3d05b-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="3d05b-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="3d05b-135">runCommand</span></span> |<span data-ttu-id="3d05b-136">Yes</span><span class="sxs-lookup"><span data-stu-id="3d05b-136">Yes</span></span> |<span data-ttu-id="3d05b-137">Artifact install command that is executed on a VM.</span><span class="sxs-lookup"><span data-stu-id="3d05b-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="3d05b-138">Artifact parameters</span><span class="sxs-lookup"><span data-stu-id="3d05b-138">Artifact parameters</span></span>
<span data-ttu-id="3d05b-139">In the parameters section of the definition file, you specify which values a user can input when installing an artifact.</span><span class="sxs-lookup"><span data-stu-id="3d05b-139">In the parameters section of the definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="3d05b-140">You can refer to these values in the artifact install command.</span><span class="sxs-lookup"><span data-stu-id="3d05b-140">You can refer to these values in the artifact install command.</span></span>

<span data-ttu-id="3d05b-141">You define parameters will the following structure.</span><span class="sxs-lookup"><span data-stu-id="3d05b-141">You define parameters will the following structure.</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="3d05b-142">Element name</span><span class="sxs-lookup"><span data-stu-id="3d05b-142">Element name</span></span> | <span data-ttu-id="3d05b-143">Required?</span><span class="sxs-lookup"><span data-stu-id="3d05b-143">Required?</span></span> | <span data-ttu-id="3d05b-144">Description</span><span class="sxs-lookup"><span data-stu-id="3d05b-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3d05b-145">type</span><span class="sxs-lookup"><span data-stu-id="3d05b-145">type</span></span> |<span data-ttu-id="3d05b-146">Yes</span><span class="sxs-lookup"><span data-stu-id="3d05b-146">Yes</span></span> |<span data-ttu-id="3d05b-147">Type of parameter value.</span><span class="sxs-lookup"><span data-stu-id="3d05b-147">Type of parameter value.</span></span> <span data-ttu-id="3d05b-148">See the list below for the allowed types:</span><span class="sxs-lookup"><span data-stu-id="3d05b-148">See the list below for the allowed types:</span></span> |
| <span data-ttu-id="3d05b-149">displayName</span><span class="sxs-lookup"><span data-stu-id="3d05b-149">displayName</span></span> |<span data-ttu-id="3d05b-150">Yes</span><span class="sxs-lookup"><span data-stu-id="3d05b-150">Yes</span></span> |<span data-ttu-id="3d05b-151">Name of the parameter that is displayed to a user in the lab.</span><span class="sxs-lookup"><span data-stu-id="3d05b-151">Name of the parameter that is displayed to a user in the lab.</span></span> | |
| <span data-ttu-id="3d05b-152">description</span><span class="sxs-lookup"><span data-stu-id="3d05b-152">description</span></span> |<span data-ttu-id="3d05b-153">Yes</span><span class="sxs-lookup"><span data-stu-id="3d05b-153">Yes</span></span> |<span data-ttu-id="3d05b-154">Description of the parameter that is displayed in the lab.</span><span class="sxs-lookup"><span data-stu-id="3d05b-154">Description of the parameter that is displayed in the lab.</span></span> |

<span data-ttu-id="3d05b-155">The allowed types are:</span><span class="sxs-lookup"><span data-stu-id="3d05b-155">The allowed types are:</span></span>

* <span data-ttu-id="3d05b-156">string – any valid JSON string</span><span class="sxs-lookup"><span data-stu-id="3d05b-156">string – any valid JSON string</span></span>
* <span data-ttu-id="3d05b-157">int – any valid JSON integer</span><span class="sxs-lookup"><span data-stu-id="3d05b-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="3d05b-158">bool – any valid JSON Boolean</span><span class="sxs-lookup"><span data-stu-id="3d05b-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="3d05b-159">array – any valid JSON array</span><span class="sxs-lookup"><span data-stu-id="3d05b-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="3d05b-160">Artifact expressions and functions</span><span class="sxs-lookup"><span data-stu-id="3d05b-160">Artifact expressions and functions</span></span>
<span data-ttu-id="3d05b-161">You can use expression and functions to construct the artifact install command.</span><span class="sxs-lookup"><span data-stu-id="3d05b-161">You can use expression and functions to construct the artifact install command.</span></span>
<span data-ttu-id="3d05b-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span><span class="sxs-lookup"><span data-stu-id="3d05b-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span></span> <span data-ttu-id="3d05b-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span><span class="sxs-lookup"><span data-stu-id="3d05b-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="3d05b-164">If you need to use a literal string that starts with a bracket [, you must use two brackets [[.</span><span class="sxs-lookup"><span data-stu-id="3d05b-164">If you need to use a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="3d05b-165">Typically, you use expressions with functions to construct a value.</span><span class="sxs-lookup"><span data-stu-id="3d05b-165">Typically, you use expressions with functions to construct a value.</span></span> <span data-ttu-id="3d05b-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3)</span><span class="sxs-lookup"><span data-stu-id="3d05b-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3)</span></span>

<span data-ttu-id="3d05b-167">The following list shows common functions.</span><span class="sxs-lookup"><span data-stu-id="3d05b-167">The following list shows common functions.</span></span>

* <span data-ttu-id="3d05b-168">parameters(parameterName) - Returns a parameter value that is provided when the artifact command is run.</span><span class="sxs-lookup"><span data-stu-id="3d05b-168">parameters(parameterName) - Returns a parameter value that is provided when the artifact command is run.</span></span>
* <span data-ttu-id="3d05b-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span><span class="sxs-lookup"><span data-stu-id="3d05b-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="3d05b-170">This function can take any number of arguments.</span><span class="sxs-lookup"><span data-stu-id="3d05b-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="3d05b-171">The following example shows how to use expression and functions to construct a value.</span><span class="sxs-lookup"><span data-stu-id="3d05b-171">The following example shows how to use expression and functions to construct a value.</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -File startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="3d05b-172">Create a custom artifact</span><span class="sxs-lookup"><span data-stu-id="3d05b-172">Create a custom artifact</span></span>
<span data-ttu-id="3d05b-173">Create your custom artifact by following steps below:</span><span class="sxs-lookup"><span data-stu-id="3d05b-173">Create your custom artifact by following steps below:</span></span>

1. <span data-ttu-id="3d05b-174">Install a JSON editor - You will need a JSON editor to work with artifact definition files.</span><span class="sxs-lookup"><span data-stu-id="3d05b-174">Install a JSON editor - You will need a JSON editor to work with artifact definition files.</span></span> <span data-ttu-id="3d05b-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span><span class="sxs-lookup"><span data-stu-id="3d05b-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="3d05b-176">Get a sample artifactfile.json - Check out the artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab) where we have created a rich library of artifacts that will help you create your own artifacts.</span><span class="sxs-lookup"><span data-stu-id="3d05b-176">Get a sample artifactfile.json - Check out the artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab) where we have created a rich library of artifacts that will help you create your own artifacts.</span></span> <span data-ttu-id="3d05b-177">Download an artifact definition file and make changes to it to create your own artifacts.</span><span class="sxs-lookup"><span data-stu-id="3d05b-177">Download an artifact definition file and make changes to it to create your own artifacts.</span></span>
3. <span data-ttu-id="3d05b-178">Make use of IntelliSense - Leverage IntelliSense to see valid elements that can be used to construct an artifact definition file.</span><span class="sxs-lookup"><span data-stu-id="3d05b-178">Make use of IntelliSense - Leverage IntelliSense to see valid elements that can be used to construct an artifact definition file.</span></span> <span data-ttu-id="3d05b-179">You can also see the different options for values of an element.</span><span class="sxs-lookup"><span data-stu-id="3d05b-179">You can also see the different options for values of an element.</span></span> <span data-ttu-id="3d05b-180">For example, IntelliSense show you the two choices of Windows or Linux when editing the **targetOsType** element.</span><span class="sxs-lookup"><span data-stu-id="3d05b-180">For example, IntelliSense show you the two choices of Windows or Linux when editing the **targetOsType** element.</span></span>
4. <span data-ttu-id="3d05b-181">Store the artifact in a git repository</span><span class="sxs-lookup"><span data-stu-id="3d05b-181">Store the artifact in a git repository</span></span>
   
   1. <span data-ttu-id="3d05b-182">Create a separate directory for each artifact where the directory name is the same as the artifact name.</span><span class="sxs-lookup"><span data-stu-id="3d05b-182">Create a separate directory for each artifact where the directory name is the same as the artifact name.</span></span>
   2. <span data-ttu-id="3d05b-183">Store the artifact definition file (artifactfile.json) in the directory you created.</span><span class="sxs-lookup"><span data-stu-id="3d05b-183">Store the artifact definition file (artifactfile.json) in the directory you created.</span></span>
   3. <span data-ttu-id="3d05b-184">Store the scripts that are referenced from the artifact install command.</span><span class="sxs-lookup"><span data-stu-id="3d05b-184">Store the scripts that are referenced from the artifact install command.</span></span>
      
      <span data-ttu-id="3d05b-185">Here is an example of how an artifact folder might look:</span><span class="sxs-lookup"><span data-stu-id="3d05b-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Artifact git repo example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="3d05b-187">Add the artifacts repository to the lab - Refer to the article, [Add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="3d05b-187">Add the artifacts repository to the lab - Refer to the article, [Add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="3d05b-188">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="3d05b-188">Related blog posts</span></span>
* [<span data-ttu-id="3d05b-189">How to troubleshoot failing Artifacts in AzureDevTestLabs</span><span class="sxs-lookup"><span data-stu-id="3d05b-189">How to troubleshoot failing Artifacts in AzureDevTestLabs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-to-troubleshoot-failing-artifacts-in-AzureDevTestLabs)
* [<span data-ttu-id="3d05b-190">Join a VM to existing AD Domain using ARM template in Azure Dev Test Lab</span><span class="sxs-lookup"><span data-stu-id="3d05b-190">Join a VM to existing AD Domain using ARM template in Azure Dev Test Lab</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="3d05b-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="3d05b-191">Next steps</span></span>
* <span data-ttu-id="3d05b-192">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="3d05b-192">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>


