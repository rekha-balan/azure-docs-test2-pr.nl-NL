---
title: Author Custom R Modules in Azure Machine Learning | Microsoft Docs
description: Quick start for authoring custom R modules in Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 821d403b35b7cd0ed7ceb6b757416bdd9efaf68b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554707"
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="76d8a-103">Author custom R modules in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="76d8a-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="76d8a-104">This topic describes how to author and deploy a custom R module in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="76d8a-104">This topic describes how to author and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="76d8a-105">It explains what custom R modules are and what files are used to define them.</span><span class="sxs-lookup"><span data-stu-id="76d8a-105">It explains what custom R modules are and what files are used to define them.</span></span> <span data-ttu-id="76d8a-106">It illustrates how to construct the files that define a module and how to register the module for deployment in a Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="76d8a-106">It illustrates how to construct the files that define a module and how to register the module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="76d8a-107">The elements and attributes used in the definition of the custom module are then described in more detail.</span><span class="sxs-lookup"><span data-stu-id="76d8a-107">The elements and attributes used in the definition of the custom module are then described in more detail.</span></span> <span data-ttu-id="76d8a-108">How to use auxiliary functionality and files and multiple outputs is also discussed.</span><span class="sxs-lookup"><span data-stu-id="76d8a-108">How to use auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="76d8a-109">What is a custom R module?</span><span class="sxs-lookup"><span data-stu-id="76d8a-109">What is a custom R module?</span></span>
<span data-ttu-id="76d8a-110">A **custom module** is a user-defined module that can be uploaded to your workspace and executed as part of an Azure Machine Learning experiment.</span><span class="sxs-lookup"><span data-stu-id="76d8a-110">A **custom module** is a user-defined module that can be uploaded to your workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="76d8a-111">A **custom R module** is a custom module that executes a user-defined R function.</span><span class="sxs-lookup"><span data-stu-id="76d8a-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="76d8a-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span><span class="sxs-lookup"><span data-stu-id="76d8a-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="76d8a-113">Currently, R is the only language supported in custom modules, but support for additional languages is scheduled for future releases.</span><span class="sxs-lookup"><span data-stu-id="76d8a-113">Currently, R is the only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="76d8a-114">Custom modules have **first-class status** in Azure Machine Learning in the sense that they can be used just like any other module.</span><span class="sxs-lookup"><span data-stu-id="76d8a-114">Custom modules have **first-class status** in Azure Machine Learning in the sense that they can be used just like any other module.</span></span> <span data-ttu-id="76d8a-115">They can be executed with other modules, included in published experiments or in visualizations.</span><span class="sxs-lookup"><span data-stu-id="76d8a-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="76d8a-116">You have control over the algorithm implemented by the module, the input and output ports to be used, the modeling parameters, and other various runtime behaviors.</span><span class="sxs-lookup"><span data-stu-id="76d8a-116">You have control over the algorithm implemented by the module, the input and output ports to be used, the modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="76d8a-117">An experiment that contains custom modules can also be published into the Cortana Intelligence Gallery for easy sharing.</span><span class="sxs-lookup"><span data-stu-id="76d8a-117">An experiment that contains custom modules can also be published into the Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="76d8a-118">Files in a custom R module</span><span class="sxs-lookup"><span data-stu-id="76d8a-118">Files in a custom R module</span></span>
<span data-ttu-id="76d8a-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span><span class="sxs-lookup"><span data-stu-id="76d8a-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="76d8a-120">A **source file** that implements the R function exposed by the module</span><span class="sxs-lookup"><span data-stu-id="76d8a-120">A **source file** that implements the R function exposed by the module</span></span>
* <span data-ttu-id="76d8a-121">An **XML definition file** that describes the custom module interface</span><span class="sxs-lookup"><span data-stu-id="76d8a-121">An **XML definition file** that describes the custom module interface</span></span>

<span data-ttu-id="76d8a-122">Additional auxiliary files can also be included in the .zip file that provides functionality that can be accessed from the custom module.</span><span class="sxs-lookup"><span data-stu-id="76d8a-122">Additional auxiliary files can also be included in the .zip file that provides functionality that can be accessed from the custom module.</span></span> <span data-ttu-id="76d8a-123">This option is discussed in the **Arguments** part of the reference section **Elements in the XML definition file** following the quickstart example.</span><span class="sxs-lookup"><span data-stu-id="76d8a-123">This option is discussed in the **Arguments** part of the reference section **Elements in the XML definition file** following the quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="76d8a-124">Quickstart example: define, package, and register a custom R module</span><span class="sxs-lookup"><span data-stu-id="76d8a-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="76d8a-125">This example illustrates how to construct the files required by a custom R module, package them into a zip file, and then register the module in your Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="76d8a-125">This example illustrates how to construct the files required by a custom R module, package them into a zip file, and then register the module in your Machine Learning workspace.</span></span> <span data-ttu-id="76d8a-126">The example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="76d8a-126">The example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="the-source-file"></a><span data-ttu-id="76d8a-127">The source file</span><span class="sxs-lookup"><span data-stu-id="76d8a-127">The source file</span></span>
<span data-ttu-id="76d8a-128">Consider the example of a **Custom Add Rows** module that modifies the standard implementation of the **Add Rows** module used to concatenate rows (observations) from two datasets (data frames).</span><span class="sxs-lookup"><span data-stu-id="76d8a-128">Consider the example of a **Custom Add Rows** module that modifies the standard implementation of the **Add Rows** module used to concatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="76d8a-129">The standard **Add Rows** module appends the rows of the second input dataset to the end of the first input dataset using the `rbind` algorithm.</span><span class="sxs-lookup"><span data-stu-id="76d8a-129">The standard **Add Rows** module appends the rows of the second input dataset to the end of the first input dataset using the `rbind` algorithm.</span></span> <span data-ttu-id="76d8a-130">The customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span><span class="sxs-lookup"><span data-stu-id="76d8a-130">The customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="76d8a-131">If the swap parameter is set to **FALSE**, it returns the same data set as the standard implementation.</span><span class="sxs-lookup"><span data-stu-id="76d8a-131">If the swap parameter is set to **FALSE**, it returns the same data set as the standard implementation.</span></span> <span data-ttu-id="76d8a-132">But if the swap parameter is **TRUE**, the function appends rows of first input dataset to the end of the second dataset instead.</span><span class="sxs-lookup"><span data-stu-id="76d8a-132">But if the swap parameter is **TRUE**, the function appends rows of first input dataset to the end of the second dataset instead.</span></span> <span data-ttu-id="76d8a-133">The CustomAddRows.R file that contains the implementation of the R `CustomAddRows` function exposed by the **Custom Add Rows** module has the following R code.</span><span class="sxs-lookup"><span data-stu-id="76d8a-133">The CustomAddRows.R file that contains the implementation of the R `CustomAddRows` function exposed by the **Custom Add Rows** module has the following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="the-xml-definition-file"></a><span data-ttu-id="76d8a-134">The XML definition file</span><span class="sxs-lookup"><span data-stu-id="76d8a-134">The XML definition file</span></span>
<span data-ttu-id="76d8a-135">To expose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created to specify how the **Custom Add Rows** module should look and behave.</span><span class="sxs-lookup"><span data-stu-id="76d8a-135">To expose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created to specify how the **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another. Dataset 2 is concatenated to Dataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify the base language, script file and R function to use for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: The values of the id attributes in the Input and Arg elements must match the parameter names in the R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>The combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="76d8a-136">It is critical to note that the value of the **id** attributes of the **Input** and **Arg** elements in the XML file must match the function parameter names of the R code in the CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in the example).</span><span class="sxs-lookup"><span data-stu-id="76d8a-136">It is critical to note that the value of the **id** attributes of the **Input** and **Arg** elements in the XML file must match the function parameter names of the R code in the CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in the example).</span></span> <span data-ttu-id="76d8a-137">Similarly, the value of the **entryPoint** attribute of the **Language** element must match the name of the function in the R script EXACTLY: (*CustomAddRows* in the example).</span><span class="sxs-lookup"><span data-stu-id="76d8a-137">Similarly, the value of the **entryPoint** attribute of the **Language** element must match the name of the function in the R script EXACTLY: (*CustomAddRows* in the example).</span></span> 

<span data-ttu-id="76d8a-138">In contrast, the **id** attribute for the **Output** element does not correspond to any variables in the R script.</span><span class="sxs-lookup"><span data-stu-id="76d8a-138">In contrast, the **id** attribute for the **Output** element does not correspond to any variables in the R script.</span></span> <span data-ttu-id="76d8a-139">When more than one output is required, simply return a list from the R function with results placed *in the same order* as **Outputs** elements are declared in the XML file.</span><span class="sxs-lookup"><span data-stu-id="76d8a-139">When more than one output is required, simply return a list from the R function with results placed *in the same order* as **Outputs** elements are declared in the XML file.</span></span>

### <a name="package-and-register-the-module"></a><span data-ttu-id="76d8a-140">Package and register the module</span><span class="sxs-lookup"><span data-stu-id="76d8a-140">Package and register the module</span></span>
<span data-ttu-id="76d8a-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip the two files together into a *CustomAddRows.zip* file.</span><span class="sxs-lookup"><span data-stu-id="76d8a-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip the two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="76d8a-142">To register them in your Machine Learning workspace, go to your workspace in the Machine Learning Studio, click the **+NEW** button on the bottom and choose **MODULE -> FROM ZIP PACKAGE** to upload the new **Custom Add Rows** module.</span><span class="sxs-lookup"><span data-stu-id="76d8a-142">To register them in your Machine Learning workspace, go to your workspace in the Machine Learning Studio, click the **+NEW** button on the bottom and choose **MODULE -> FROM ZIP PACKAGE** to upload the new **Custom Add Rows** module.</span></span>

![Upload Zip](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="76d8a-144">The **Custom Add Rows** module is now ready to be accessed by your Machine Learning experiments.</span><span class="sxs-lookup"><span data-stu-id="76d8a-144">The **Custom Add Rows** module is now ready to be accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-the-xml-definition-file"></a><span data-ttu-id="76d8a-145">Elements in the XML definition file</span><span class="sxs-lookup"><span data-stu-id="76d8a-145">Elements in the XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="76d8a-146">Module elements</span><span class="sxs-lookup"><span data-stu-id="76d8a-146">Module elements</span></span>
<span data-ttu-id="76d8a-147">The **Module** element is used to define a custom module in the XML file.</span><span class="sxs-lookup"><span data-stu-id="76d8a-147">The **Module** element is used to define a custom module in the XML file.</span></span> <span data-ttu-id="76d8a-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span><span class="sxs-lookup"><span data-stu-id="76d8a-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="76d8a-149">Each module in your workspace must have a unique name.</span><span class="sxs-lookup"><span data-stu-id="76d8a-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="76d8a-150">Register a custom module with the same name as an existing custom module and it replaces the existing module with the new one.</span><span class="sxs-lookup"><span data-stu-id="76d8a-150">Register a custom module with the same name as an existing custom module and it replaces the existing module with the new one.</span></span> <span data-ttu-id="76d8a-151">Custom modules can, however, be registered with the same name as an existing Azure Machine Learning module.</span><span class="sxs-lookup"><span data-stu-id="76d8a-151">Custom modules can, however, be registered with the same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="76d8a-152">If so, they appear in the **Custom** category of the module palette.</span><span class="sxs-lookup"><span data-stu-id="76d8a-152">If so, they appear in the **Custom** category of the module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another...</Description>/> 


<span data-ttu-id="76d8a-153">Within the **Module** element, you can specify two additional optional elements:</span><span class="sxs-lookup"><span data-stu-id="76d8a-153">Within the **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="76d8a-154">an **Owner** element that is embedded into the module</span><span class="sxs-lookup"><span data-stu-id="76d8a-154">an **Owner** element that is embedded into the module</span></span>  
* <span data-ttu-id="76d8a-155">a **Description** element that contains text that is displayed in quick help for the module and when you hover over the module in the Machine Learning UI.</span><span class="sxs-lookup"><span data-stu-id="76d8a-155">a **Description** element that contains text that is displayed in quick help for the module and when you hover over the module in the Machine Learning UI.</span></span>

<span data-ttu-id="76d8a-156">Rules for characters limits in the Module elements:</span><span class="sxs-lookup"><span data-stu-id="76d8a-156">Rules for characters limits in the Module elements:</span></span>

* <span data-ttu-id="76d8a-157">The value of the **name** attribute in the **Module** element must not exceed 64 characters in length.</span><span class="sxs-lookup"><span data-stu-id="76d8a-157">The value of the **name** attribute in the **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="76d8a-158">The content of the **Description** element must not exceed 128 characters in length.</span><span class="sxs-lookup"><span data-stu-id="76d8a-158">The content of the **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="76d8a-159">The content of the **Owner** element must not exceed 32 characters in length.</span><span class="sxs-lookup"><span data-stu-id="76d8a-159">The content of the **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="76d8a-160">A module's results can be deterministic or nondeterministic.\*\* By default, all modules are considered to be deterministic.</span><span class="sxs-lookup"><span data-stu-id="76d8a-160">A module's results can be deterministic or nondeterministic.\*\* By default, all modules are considered to be deterministic.</span></span> <span data-ttu-id="76d8a-161">That is, given an unchanging set of input parameters and data, the module should return the same results eacRAND or a functionh time it is run.</span><span class="sxs-lookup"><span data-stu-id="76d8a-161">That is, given an unchanging set of input parameters and data, the module should return the same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="76d8a-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or the input data has changed.</span><span class="sxs-lookup"><span data-stu-id="76d8a-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or the input data has changed.</span></span> <span data-ttu-id="76d8a-163">Returning the cached results also provides much faster execution of experiments.</span><span class="sxs-lookup"><span data-stu-id="76d8a-163">Returning the cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="76d8a-164">There are functions that are nondeterministic, such as RAND or a function that returns the current date or time.</span><span class="sxs-lookup"><span data-stu-id="76d8a-164">There are functions that are nondeterministic, such as RAND or a function that returns the current date or time.</span></span> <span data-ttu-id="76d8a-165">If your module uses a nondeterministic function, you can specify that the module is non-deterministic by setting the optional **isDeterministic** attribute to **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="76d8a-165">If your module uses a nondeterministic function, you can specify that the module is non-deterministic by setting the optional **isDeterministic** attribute to **FALSE**.</span></span> <span data-ttu-id="76d8a-166">This insures that the module is rerun whenever the experiment is run, even if the module input and parameters have not changed.</span><span class="sxs-lookup"><span data-stu-id="76d8a-166">This insures that the module is rerun whenever the experiment is run, even if the module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="76d8a-167">Language Definition</span><span class="sxs-lookup"><span data-stu-id="76d8a-167">Language Definition</span></span>
<span data-ttu-id="76d8a-168">The **Language** element in your XML definition file is used to specify the custom module language.</span><span class="sxs-lookup"><span data-stu-id="76d8a-168">The **Language** element in your XML definition file is used to specify the custom module language.</span></span> <span data-ttu-id="76d8a-169">Currently, R is the only supported language.</span><span class="sxs-lookup"><span data-stu-id="76d8a-169">Currently, R is the only supported language.</span></span> <span data-ttu-id="76d8a-170">The value of the **sourceFile** attribute must be the name of the R file that contains the function to call when the module is run.</span><span class="sxs-lookup"><span data-stu-id="76d8a-170">The value of the **sourceFile** attribute must be the name of the R file that contains the function to call when the module is run.</span></span> <span data-ttu-id="76d8a-171">This file must be part of the zip package.</span><span class="sxs-lookup"><span data-stu-id="76d8a-171">This file must be part of the zip package.</span></span> <span data-ttu-id="76d8a-172">The value of the **entryPoint** attribute is the name of the function being called and must match a valid function defined with in the source file.</span><span class="sxs-lookup"><span data-stu-id="76d8a-172">The value of the **entryPoint** attribute is the name of the function being called and must match a valid function defined with in the source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="76d8a-173">Ports</span><span class="sxs-lookup"><span data-stu-id="76d8a-173">Ports</span></span>
<span data-ttu-id="76d8a-174">The input and output ports for a custom module are specified in child elements of the **Ports** section of the XML definition file.</span><span class="sxs-lookup"><span data-stu-id="76d8a-174">The input and output ports for a custom module are specified in child elements of the **Ports** section of the XML definition file.</span></span> <span data-ttu-id="76d8a-175">The order of these elements determines the layout experienced (UX) by users.</span><span class="sxs-lookup"><span data-stu-id="76d8a-175">The order of these elements determines the layout experienced (UX) by users.</span></span> <span data-ttu-id="76d8a-176">The first child **input** or **output** listed in the **Ports** element of the XML file becomes the left-most input port in the Machine Learning UX.</span><span class="sxs-lookup"><span data-stu-id="76d8a-176">The first child **input** or **output** listed in the **Ports** element of the XML file becomes the left-most input port in the Machine Learning UX.</span></span>
<span data-ttu-id="76d8a-177">Each input and output port may have an optional **Description** child element that specifies the text shown when you hover the mouse cursor over the port in the Machine Learning UI.</span><span class="sxs-lookup"><span data-stu-id="76d8a-177">Each input and output port may have an optional **Description** child element that specifies the text shown when you hover the mouse cursor over the port in the Machine Learning UI.</span></span>

<span data-ttu-id="76d8a-178">**Ports Rules**:</span><span class="sxs-lookup"><span data-stu-id="76d8a-178">**Ports Rules**:</span></span>

* <span data-ttu-id="76d8a-179">Maximum number of **input and output ports** is 8 for each.</span><span class="sxs-lookup"><span data-stu-id="76d8a-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="76d8a-180">Input elements</span><span class="sxs-lookup"><span data-stu-id="76d8a-180">Input elements</span></span>
<span data-ttu-id="76d8a-181">Input ports allow you to pass data to your R function and workspace.</span><span class="sxs-lookup"><span data-stu-id="76d8a-181">Input ports allow you to pass data to your R function and workspace.</span></span> <span data-ttu-id="76d8a-182">The **data types** that are supported for input ports are as follows:</span><span class="sxs-lookup"><span data-stu-id="76d8a-182">The **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="76d8a-183">**DataTable:** This type is passed to your R function as a data.frame.</span><span class="sxs-lookup"><span data-stu-id="76d8a-183">**DataTable:** This type is passed to your R function as a data.frame.</span></span> <span data-ttu-id="76d8a-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted to a data.frame automatically.</span><span class="sxs-lookup"><span data-stu-id="76d8a-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted to a data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="76d8a-185">The **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span><span class="sxs-lookup"><span data-stu-id="76d8a-185">The **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="76d8a-186">Optional **DataTable** ports that are not passed as input in an experiment have the value **NULL** passed to the R function and optional zip ports are ignored if the input is not connected.</span><span class="sxs-lookup"><span data-stu-id="76d8a-186">Optional **DataTable** ports that are not passed as input in an experiment have the value **NULL** passed to the R function and optional zip ports are ignored if the input is not connected.</span></span> <span data-ttu-id="76d8a-187">The **isOptional** attribute is optional for both the **DataTable** and **Zip** types and is *false* by default.</span><span class="sxs-lookup"><span data-stu-id="76d8a-187">The **isOptional** attribute is optional for both the **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="76d8a-188">**Zip:** Custom modules can accept a zip file as input.</span><span class="sxs-lookup"><span data-stu-id="76d8a-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="76d8a-189">This input is unpacked into the R working directory of your function</span><span class="sxs-lookup"><span data-stu-id="76d8a-189">This input is unpacked into the R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files to be extracted to the R working directory.</Description>
           </Input>

<span data-ttu-id="76d8a-190">For custom R modules, the id for a Zip port does not have to match any parameters of the R function.</span><span class="sxs-lookup"><span data-stu-id="76d8a-190">For custom R modules, the id for a Zip port does not have to match any parameters of the R function.</span></span> <span data-ttu-id="76d8a-191">This is because the zip file is automatically extracted to the R working directory.</span><span class="sxs-lookup"><span data-stu-id="76d8a-191">This is because the zip file is automatically extracted to the R working directory.</span></span>

<span data-ttu-id="76d8a-192">**Input Rules:**</span><span class="sxs-lookup"><span data-stu-id="76d8a-192">**Input Rules:**</span></span>

* <span data-ttu-id="76d8a-193">The value of the **id** attribute of the **Input** element must be a valid R variable name.</span><span class="sxs-lookup"><span data-stu-id="76d8a-193">The value of the **id** attribute of the **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="76d8a-194">The value of the **id** attribute of the **Input** element must not be longer than 64 characters.</span><span class="sxs-lookup"><span data-stu-id="76d8a-194">The value of the **id** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="76d8a-195">The value of the **name** attribute of the **Input** element must not be longer than 64 characters.</span><span class="sxs-lookup"><span data-stu-id="76d8a-195">The value of the **name** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="76d8a-196">The content of the **Description** element must not be longer than 128 characters</span><span class="sxs-lookup"><span data-stu-id="76d8a-196">The content of the **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="76d8a-197">The value of the **type** attribute of the **Input** element must be *Zip* or *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="76d8a-197">The value of the **type** attribute of the **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="76d8a-198">The value of the **isOptional** attribute of the **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span><span class="sxs-lookup"><span data-stu-id="76d8a-198">The value of the **isOptional** attribute of the **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="76d8a-199">Output elements</span><span class="sxs-lookup"><span data-stu-id="76d8a-199">Output elements</span></span>
<span data-ttu-id="76d8a-200">**Standard output ports:** Output ports are mapped to the return values from your R function, which can then be used by subsequent modules.</span><span class="sxs-lookup"><span data-stu-id="76d8a-200">**Standard output ports:** Output ports are mapped to the return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="76d8a-201">*DataTable* is the only standard output port type supported currently.</span><span class="sxs-lookup"><span data-stu-id="76d8a-201">*DataTable* is the only standard output port type supported currently.</span></span> <span data-ttu-id="76d8a-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span><span class="sxs-lookup"><span data-stu-id="76d8a-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="76d8a-203">For outputs in custom R modules, the value of the **id** attribute does not have to correspond with anything in the R script, but it must be unique.</span><span class="sxs-lookup"><span data-stu-id="76d8a-203">For outputs in custom R modules, the value of the **id** attribute does not have to correspond with anything in the R script, but it must be unique.</span></span> <span data-ttu-id="76d8a-204">For a single module output, the return value from the R function must be a *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="76d8a-204">For a single module output, the return value from the R function must be a *data.frame*.</span></span> <span data-ttu-id="76d8a-205">In order to output more than one object of a supported data type, the appropriate output ports need to be specified in the XML definition file and the objects need to be returned as a list.</span><span class="sxs-lookup"><span data-stu-id="76d8a-205">In order to output more than one object of a supported data type, the appropriate output ports need to be specified in the XML definition file and the objects need to be returned as a list.</span></span> <span data-ttu-id="76d8a-206">The output objects are assigned to output ports from left to right, reflecting the order in which the objects are placed in the returned list.</span><span class="sxs-lookup"><span data-stu-id="76d8a-206">The output objects are assigned to output ports from left to right, reflecting the order in which the objects are placed in the returned list.</span></span>

<span data-ttu-id="76d8a-207">For example, if you want to modify the **Custom Add Rows** module to output the original two datasets, *dataset1* and *dataset2*, in addition to the new joined dataset, *dataset*, (in an order, from left to right, as: *dataset*, *dataset1*, *dataset2*), then define the output ports in the CustomAddRows.xml file as follows:</span><span class="sxs-lookup"><span data-stu-id="76d8a-207">For example, if you want to modify the **Custom Add Rows** module to output the original two datasets, *dataset1* and *dataset2*, in addition to the new joined dataset, *dataset*, (in an order, from left to right, as: *dataset*, *dataset1*, *dataset2*), then define the output ports in the CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="76d8a-208">And return the list of objects in a list in the correct order in ‘CustomAddRows.R’:</span><span class="sxs-lookup"><span data-stu-id="76d8a-208">And return the list of objects in a list in the correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="76d8a-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays the output from the R graphics device and console output.</span><span class="sxs-lookup"><span data-stu-id="76d8a-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays the output from the R graphics device and console output.</span></span> <span data-ttu-id="76d8a-210">This port is not part of the R function output and does not interfere with the order of the other output port types.</span><span class="sxs-lookup"><span data-stu-id="76d8a-210">This port is not part of the R function output and does not interfere with the order of the other output port types.</span></span> <span data-ttu-id="76d8a-211">To add a visualization port to the custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span><span class="sxs-lookup"><span data-stu-id="76d8a-211">To add a visualization port to the custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View the R console graphics device output.</Description>
    </Output>

<span data-ttu-id="76d8a-212">**Output Rules:**</span><span class="sxs-lookup"><span data-stu-id="76d8a-212">**Output Rules:**</span></span>

* <span data-ttu-id="76d8a-213">The value of the **id** attribute of the **Output** element must be a valid R variable name.</span><span class="sxs-lookup"><span data-stu-id="76d8a-213">The value of the **id** attribute of the **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="76d8a-214">The value of the **id** attribute of the **Output** element must not be longer than 32 characters.</span><span class="sxs-lookup"><span data-stu-id="76d8a-214">The value of the **id** attribute of the **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="76d8a-215">The value of the **name** attribute of the **Output** element must not be longer than 64 characters.</span><span class="sxs-lookup"><span data-stu-id="76d8a-215">The value of the **name** attribute of the **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="76d8a-216">The value of the **type** attribute of the **Output** element must be *Visualization*.</span><span class="sxs-lookup"><span data-stu-id="76d8a-216">The value of the **type** attribute of the **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="76d8a-217">Arguments</span><span class="sxs-lookup"><span data-stu-id="76d8a-217">Arguments</span></span>
<span data-ttu-id="76d8a-218">Additional data can be passed to the R function via module parameters which are defined in the **Arguments** element.</span><span class="sxs-lookup"><span data-stu-id="76d8a-218">Additional data can be passed to the R function via module parameters which are defined in the **Arguments** element.</span></span> <span data-ttu-id="76d8a-219">These parameters appear in the rightmost properties pane of the Machine Learning UI when the module is selected.</span><span class="sxs-lookup"><span data-stu-id="76d8a-219">These parameters appear in the rightmost properties pane of the Machine Learning UI when the module is selected.</span></span> <span data-ttu-id="76d8a-220">Arguments can be any of the supported types or you can create a custom enumeration when needed.</span><span class="sxs-lookup"><span data-stu-id="76d8a-220">Arguments can be any of the supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="76d8a-221">Similar to the **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies the text that appears when you hover the mouse over the parameter name.</span><span class="sxs-lookup"><span data-stu-id="76d8a-221">Similar to the **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies the text that appears when you hover the mouse over the parameter name.</span></span>
<span data-ttu-id="76d8a-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added to any argument as attributes to a **Properties** element.</span><span class="sxs-lookup"><span data-stu-id="76d8a-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added to any argument as attributes to a **Properties** element.</span></span> <span data-ttu-id="76d8a-223">Valid properties for the **Properties** element depend on the argument type and are described with the supported argument types in the next section.</span><span class="sxs-lookup"><span data-stu-id="76d8a-223">Valid properties for the **Properties** element depend on the argument type and are described with the supported argument types in the next section.</span></span> <span data-ttu-id="76d8a-224">Arguments with the **isOptional** property set to **"true"** do not require the user to enter a value.</span><span class="sxs-lookup"><span data-stu-id="76d8a-224">Arguments with the **isOptional** property set to **"true"** do not require the user to enter a value.</span></span> <span data-ttu-id="76d8a-225">If a value is not provided to the argument, then the argument is not passed to the entry point function.</span><span class="sxs-lookup"><span data-stu-id="76d8a-225">If a value is not provided to the argument, then the argument is not passed to the entry point function.</span></span> <span data-ttu-id="76d8a-226">Arguments of the entry point function that are optional need to be explicitly handled by the function, e.g. assigned a default value of NULL in the entry point function definition.</span><span class="sxs-lookup"><span data-stu-id="76d8a-226">Arguments of the entry point function that are optional need to be explicitly handled by the function, e.g. assigned a default value of NULL in the entry point function definition.</span></span> <span data-ttu-id="76d8a-227">An optional argument will only enforce the other argument constraints, i.e. min or max, if a value is provided by the user.</span><span class="sxs-lookup"><span data-stu-id="76d8a-227">An optional argument will only enforce the other argument constraints, i.e. min or max, if a value is provided by the user.</span></span>
<span data-ttu-id="76d8a-228">As with inputs and outputs, it is critical that each of the parameters have unique id values associated with them.</span><span class="sxs-lookup"><span data-stu-id="76d8a-228">As with inputs and outputs, it is critical that each of the parameters have unique id values associated with them.</span></span> <span data-ttu-id="76d8a-229">In our quick start example the associated id/parameter was *swap*.</span><span class="sxs-lookup"><span data-stu-id="76d8a-229">In our quick start example the associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="76d8a-230">Arg element</span><span class="sxs-lookup"><span data-stu-id="76d8a-230">Arg element</span></span>
<span data-ttu-id="76d8a-231">A module parameter is defined using the **Arg** child element of the **Arguments** section of the XML definition file.</span><span class="sxs-lookup"><span data-stu-id="76d8a-231">A module parameter is defined using the **Arg** child element of the **Arguments** section of the XML definition file.</span></span> <span data-ttu-id="76d8a-232">As with the child elements in the **Ports** section, the ordering of parameters in the **Arguments** section defines the layout encountered in the UX.</span><span class="sxs-lookup"><span data-stu-id="76d8a-232">As with the child elements in the **Ports** section, the ordering of parameters in the **Arguments** section defines the layout encountered in the UX.</span></span> <span data-ttu-id="76d8a-233">The parameters appear from top down in the UI in the same order in which they are defined in the XML file.</span><span class="sxs-lookup"><span data-stu-id="76d8a-233">The parameters appear from top down in the UI in the same order in which they are defined in the XML file.</span></span> <span data-ttu-id="76d8a-234">The types supported by Machine Learning for parameters are listed here.</span><span class="sxs-lookup"><span data-stu-id="76d8a-234">The types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="76d8a-235">**int** – an Integer (32-bit) type parameter.</span><span class="sxs-lookup"><span data-stu-id="76d8a-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="76d8a-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span><span class="sxs-lookup"><span data-stu-id="76d8a-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="76d8a-237">**double** – a double type parameter.</span><span class="sxs-lookup"><span data-stu-id="76d8a-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="76d8a-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span><span class="sxs-lookup"><span data-stu-id="76d8a-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="76d8a-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span><span class="sxs-lookup"><span data-stu-id="76d8a-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="76d8a-240">*Optional Properties*: **default** - false if not set</span><span class="sxs-lookup"><span data-stu-id="76d8a-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="76d8a-241">**string**: a standard string</span><span class="sxs-lookup"><span data-stu-id="76d8a-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="76d8a-242">*Optional Properties*: **default** and **isOptional**</span><span class="sxs-lookup"><span data-stu-id="76d8a-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="76d8a-243">**ColumnPicker**: a column selection parameter.</span><span class="sxs-lookup"><span data-stu-id="76d8a-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="76d8a-244">This type renders in the UX as a column chooser.</span><span class="sxs-lookup"><span data-stu-id="76d8a-244">This type renders in the UX as a column chooser.</span></span> <span data-ttu-id="76d8a-245">The **Property** element is used here to specify the id of the port from which columns are selected, where the target port type must be *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="76d8a-245">The **Property** element is used here to specify the id of the port from which columns are selected, where the target port type must be *DataTable*.</span></span> <span data-ttu-id="76d8a-246">The result of the column selection is passed to the R function as a list of strings containing the selected column names.</span><span class="sxs-lookup"><span data-stu-id="76d8a-246">The result of the column selection is passed to the R function as a list of strings containing the selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="76d8a-247">*Required Properties*: **portId** - matches the id of an Input element with type *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="76d8a-247">*Required Properties*: **portId** - matches the id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="76d8a-248">*Optional Properties*:</span><span class="sxs-lookup"><span data-stu-id="76d8a-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="76d8a-249">**allowedTypes** - Filters the column types from which you can pick.</span><span class="sxs-lookup"><span data-stu-id="76d8a-249">**allowedTypes** - Filters the column types from which you can pick.</span></span> <span data-ttu-id="76d8a-250">Valid values include:</span><span class="sxs-lookup"><span data-stu-id="76d8a-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="76d8a-251">Numeric</span><span class="sxs-lookup"><span data-stu-id="76d8a-251">Numeric</span></span>
    * <span data-ttu-id="76d8a-252">Boolean</span><span class="sxs-lookup"><span data-stu-id="76d8a-252">Boolean</span></span>
    * <span data-ttu-id="76d8a-253">Categorical</span><span class="sxs-lookup"><span data-stu-id="76d8a-253">Categorical</span></span>
    * <span data-ttu-id="76d8a-254">String</span><span class="sxs-lookup"><span data-stu-id="76d8a-254">String</span></span>
    * <span data-ttu-id="76d8a-255">Label</span><span class="sxs-lookup"><span data-stu-id="76d8a-255">Label</span></span>
    * <span data-ttu-id="76d8a-256">Feature</span><span class="sxs-lookup"><span data-stu-id="76d8a-256">Feature</span></span>
    * <span data-ttu-id="76d8a-257">Score</span><span class="sxs-lookup"><span data-stu-id="76d8a-257">Score</span></span>
    * <span data-ttu-id="76d8a-258">All</span><span class="sxs-lookup"><span data-stu-id="76d8a-258">All</span></span>
  * <span data-ttu-id="76d8a-259">**default** - Valid default selections for the column picker include:</span><span class="sxs-lookup"><span data-stu-id="76d8a-259">**default** - Valid default selections for the column picker include:</span></span> 
    
    * <span data-ttu-id="76d8a-260">None</span><span class="sxs-lookup"><span data-stu-id="76d8a-260">None</span></span>
    * <span data-ttu-id="76d8a-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="76d8a-261">NumericFeature</span></span>
    * <span data-ttu-id="76d8a-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="76d8a-262">NumericLabel</span></span>
    * <span data-ttu-id="76d8a-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="76d8a-263">NumericScore</span></span>
    * <span data-ttu-id="76d8a-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="76d8a-264">NumericAll</span></span>
    * <span data-ttu-id="76d8a-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="76d8a-265">BooleanFeature</span></span>
    * <span data-ttu-id="76d8a-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="76d8a-266">BooleanLabel</span></span>
    * <span data-ttu-id="76d8a-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="76d8a-267">BooleanScore</span></span>
    * <span data-ttu-id="76d8a-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="76d8a-268">BooleanAll</span></span>
    * <span data-ttu-id="76d8a-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="76d8a-269">CategoricalFeature</span></span>
    * <span data-ttu-id="76d8a-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="76d8a-270">CategoricalLabel</span></span>
    * <span data-ttu-id="76d8a-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="76d8a-271">CategoricalScore</span></span>
    * <span data-ttu-id="76d8a-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="76d8a-272">CategoricalAll</span></span>
    * <span data-ttu-id="76d8a-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="76d8a-273">StringFeature</span></span>
    * <span data-ttu-id="76d8a-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="76d8a-274">StringLabel</span></span>
    * <span data-ttu-id="76d8a-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="76d8a-275">StringScore</span></span>
    * <span data-ttu-id="76d8a-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="76d8a-276">StringAll</span></span>
    * <span data-ttu-id="76d8a-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="76d8a-277">AllLabel</span></span>
    * <span data-ttu-id="76d8a-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="76d8a-278">AllFeature</span></span>
    * <span data-ttu-id="76d8a-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="76d8a-279">AllScore</span></span>
    * <span data-ttu-id="76d8a-280">All</span><span class="sxs-lookup"><span data-stu-id="76d8a-280">All</span></span>

<span data-ttu-id="76d8a-281">**DropDown**: a user-specified enumerated (dropdown) list.</span><span class="sxs-lookup"><span data-stu-id="76d8a-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="76d8a-282">The dropdown items are specified within the **Properties** element using an **Item** element.</span><span class="sxs-lookup"><span data-stu-id="76d8a-282">The dropdown items are specified within the **Properties** element using an **Item** element.</span></span> <span data-ttu-id="76d8a-283">The **id** for each **Item** must be unique and a valid R variable.</span><span class="sxs-lookup"><span data-stu-id="76d8a-283">The **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="76d8a-284">The value of the **name** of an **Item** serves as both the text that you see and the value that is passed to the R function.</span><span class="sxs-lookup"><span data-stu-id="76d8a-284">The value of the **name** of an **Item** serves as both the text that you see and the value that is passed to the R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="76d8a-285">*Optional Properties*:</span><span class="sxs-lookup"><span data-stu-id="76d8a-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="76d8a-286">**default** - The value for the default property must correspond with an id value from one of the **Item** elements.</span><span class="sxs-lookup"><span data-stu-id="76d8a-286">**default** - The value for the default property must correspond with an id value from one of the **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="76d8a-287">Auxiliary Files</span><span class="sxs-lookup"><span data-stu-id="76d8a-287">Auxiliary Files</span></span>
<span data-ttu-id="76d8a-288">Any file that is placed in your custom module ZIP file is going to be available for use during execution time.</span><span class="sxs-lookup"><span data-stu-id="76d8a-288">Any file that is placed in your custom module ZIP file is going to be available for use during execution time.</span></span> <span data-ttu-id="76d8a-289">Any directory structures present are preserved.</span><span class="sxs-lookup"><span data-stu-id="76d8a-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="76d8a-290">This means that file sourcing works the same locally and in Azure Machine Learning execution.</span><span class="sxs-lookup"><span data-stu-id="76d8a-290">This means that file sourcing works the same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="76d8a-291">Notice that all files are extracted to ‘src’ directory so all paths should have ‘src/’ prefix.</span><span class="sxs-lookup"><span data-stu-id="76d8a-291">Notice that all files are extracted to ‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="76d8a-292">For example, say you want to remove any rows with NAs from the dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span><span class="sxs-lookup"><span data-stu-id="76d8a-292">For example, say you want to remove any rows with NAs from the dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="76d8a-293">You can source the auxiliary file RemoveDupNARows.R in the CustomAddRows function:</span><span class="sxs-lookup"><span data-stu-id="76d8a-293">You can source the auxiliary file RemoveDupNARows.R in the CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="76d8a-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span><span class="sxs-lookup"><span data-stu-id="76d8a-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="76d8a-295">Execution Environment</span><span class="sxs-lookup"><span data-stu-id="76d8a-295">Execution Environment</span></span>
<span data-ttu-id="76d8a-296">The execution environment for the R script uses the same version of R as the **Execute R Script** module and can use the same default packages.</span><span class="sxs-lookup"><span data-stu-id="76d8a-296">The execution environment for the R script uses the same version of R as the **Execute R Script** module and can use the same default packages.</span></span> <span data-ttu-id="76d8a-297">You can also add additional R packages to your custom module by including them in the custom module zip package.</span><span class="sxs-lookup"><span data-stu-id="76d8a-297">You can also add additional R packages to your custom module by including them in the custom module zip package.</span></span> <span data-ttu-id="76d8a-298">Just load them in your R script as you would in your own R environment.</span><span class="sxs-lookup"><span data-stu-id="76d8a-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="76d8a-299">**Limitations of the execution environment** include:</span><span class="sxs-lookup"><span data-stu-id="76d8a-299">**Limitations of the execution environment** include:</span></span>

* <span data-ttu-id="76d8a-300">Non-persistent file system: Files written when the custom module is run are not persisted across multiple runs of the same module.</span><span class="sxs-lookup"><span data-stu-id="76d8a-300">Non-persistent file system: Files written when the custom module is run are not persisted across multiple runs of the same module.</span></span>
* <span data-ttu-id="76d8a-301">No network access</span><span class="sxs-lookup"><span data-stu-id="76d8a-301">No network access</span></span>


