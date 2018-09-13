---
title: Use Python extensibility with Azure Machine Learning Data Preparations | Microsoft Docs
description: This document provides an overview and some detailed examples of how to use Python code to extend the functionality of data preparation
services: machine-learning
author: euangMS
ms.author: euang
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: ''
ms.devlang: ''
ms.topic: article
ms.date: 05/09/2018
ms.openlocfilehash: a713f5fcde31e0e25de080a65b71209011ef551d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866587"
---
# <a name="data-preparations-python-extensions"></a><span data-ttu-id="f8f24-103">Data Preparations Python extensions</span><span class="sxs-lookup"><span data-stu-id="f8f24-103">Data Preparations Python extensions</span></span>
<span data-ttu-id="f8f24-104">As a way of filling in functionality gaps between built-in features, Azure Machine Learning Data Preparations includes extensibility at multiple levels.</span><span class="sxs-lookup"><span data-stu-id="f8f24-104">As a way of filling in functionality gaps between built-in features, Azure Machine Learning Data Preparations includes extensibility at multiple levels.</span></span> <span data-ttu-id="f8f24-105">In this document, we outline the extensibility via Python script.</span><span class="sxs-lookup"><span data-stu-id="f8f24-105">In this document, we outline the extensibility via Python script.</span></span> 

## <a name="custom-code-steps"></a><span data-ttu-id="f8f24-106">Custom code steps</span><span class="sxs-lookup"><span data-stu-id="f8f24-106">Custom code steps</span></span> 
<span data-ttu-id="f8f24-107">Data Preparations has the following custom steps where users can write code:</span><span class="sxs-lookup"><span data-stu-id="f8f24-107">Data Preparations has the following custom steps where users can write code:</span></span>

* <span data-ttu-id="f8f24-108">Add Column</span><span class="sxs-lookup"><span data-stu-id="f8f24-108">Add Column</span></span>
* <span data-ttu-id="f8f24-109">Advanced Filter</span><span class="sxs-lookup"><span data-stu-id="f8f24-109">Advanced Filter</span></span>
* <span data-ttu-id="f8f24-110">Transform Dataflow</span><span class="sxs-lookup"><span data-stu-id="f8f24-110">Transform Dataflow</span></span>
* <span data-ttu-id="f8f24-111">Transform Partition</span><span class="sxs-lookup"><span data-stu-id="f8f24-111">Transform Partition</span></span>

## <a name="code-block-types"></a><span data-ttu-id="f8f24-112">Code block types</span><span class="sxs-lookup"><span data-stu-id="f8f24-112">Code block types</span></span> 
<span data-ttu-id="f8f24-113">For each of these steps, we support two code block types.</span><span class="sxs-lookup"><span data-stu-id="f8f24-113">For each of these steps, we support two code block types.</span></span> <span data-ttu-id="f8f24-114">First, we support a bare Python Expression that is executed as is.</span><span class="sxs-lookup"><span data-stu-id="f8f24-114">First, we support a bare Python Expression that is executed as is.</span></span> <span data-ttu-id="f8f24-115">Second, we support a Python Module where we call a particular function with a known signature in the code you supply.</span><span class="sxs-lookup"><span data-stu-id="f8f24-115">Second, we support a Python Module where we call a particular function with a known signature in the code you supply.</span></span>

<span data-ttu-id="f8f24-116">For example, you can add a new column that calculates the log of another column in the following two ways:</span><span class="sxs-lookup"><span data-stu-id="f8f24-116">For example, you can add a new column that calculates the log of another column in the following two ways:</span></span>

<span data-ttu-id="f8f24-117">Expression</span><span class="sxs-lookup"><span data-stu-id="f8f24-117">Expression</span></span> 

```python    
    math.log(row["Score"])
```

<span data-ttu-id="f8f24-118">Module</span><span class="sxs-lookup"><span data-stu-id="f8f24-118">Module</span></span> 
    
```python
def newvalue(row): 
        return math.log(row["Score"])
```


<span data-ttu-id="f8f24-119">The Add Column transform in Module mode expects to find a function called `newvalue` that accepts a row variable and returns the value for the column.</span><span class="sxs-lookup"><span data-stu-id="f8f24-119">The Add Column transform in Module mode expects to find a function called `newvalue` that accepts a row variable and returns the value for the column.</span></span> <span data-ttu-id="f8f24-120">This module can include any quantity of Python code with other functions, imports, etc.</span><span class="sxs-lookup"><span data-stu-id="f8f24-120">This module can include any quantity of Python code with other functions, imports, etc.</span></span>

<span data-ttu-id="f8f24-121">The details of each extension point are discussed in the following sections.</span><span class="sxs-lookup"><span data-stu-id="f8f24-121">The details of each extension point are discussed in the following sections.</span></span> 

## <a name="imports"></a><span data-ttu-id="f8f24-122">Imports</span><span class="sxs-lookup"><span data-stu-id="f8f24-122">Imports</span></span> 
<span data-ttu-id="f8f24-123">If you use the Expression block type, you can still add **import** statements to your code.</span><span class="sxs-lookup"><span data-stu-id="f8f24-123">If you use the Expression block type, you can still add **import** statements to your code.</span></span> <span data-ttu-id="f8f24-124">They all must be grouped on the top lines of your code.</span><span class="sxs-lookup"><span data-stu-id="f8f24-124">They all must be grouped on the top lines of your code.</span></span>

<span data-ttu-id="f8f24-125">Correct</span><span class="sxs-lookup"><span data-stu-id="f8f24-125">Correct</span></span> 

```python
import math 
import numpy 
math.log(row["Score"])
```
 

<span data-ttu-id="f8f24-126">Error</span><span class="sxs-lookup"><span data-stu-id="f8f24-126">Error</span></span>  

```python
import math  
math.log(row["Score"])  
import numpy
```
 
 
<span data-ttu-id="f8f24-127">If you use the Module block type, you can follow all the normal Python rules for using the **import** statement.</span><span class="sxs-lookup"><span data-stu-id="f8f24-127">If you use the Module block type, you can follow all the normal Python rules for using the **import** statement.</span></span> 

## <a name="default-imports"></a><span data-ttu-id="f8f24-128">Default imports</span><span class="sxs-lookup"><span data-stu-id="f8f24-128">Default imports</span></span>
<span data-ttu-id="f8f24-129">The following imports are always included and usable in your code.</span><span class="sxs-lookup"><span data-stu-id="f8f24-129">The following imports are always included and usable in your code.</span></span> <span data-ttu-id="f8f24-130">You don't need to reimport them.</span><span class="sxs-lookup"><span data-stu-id="f8f24-130">You don't need to reimport them.</span></span> 

```python
import math  
import numbers  
import datetime  
import re  
import pandas as pd  
import numpy as np  
import scipy as sp
```
  

## <a name="install-new-packages"></a><span data-ttu-id="f8f24-131">Install new packages</span><span class="sxs-lookup"><span data-stu-id="f8f24-131">Install new packages</span></span>
<span data-ttu-id="f8f24-132">To use a package that's not installed by default, you first need to install it into the environments that Data Preparations uses.</span><span class="sxs-lookup"><span data-stu-id="f8f24-132">To use a package that's not installed by default, you first need to install it into the environments that Data Preparations uses.</span></span> <span data-ttu-id="f8f24-133">This installation needs to be done both on your local machine and on any compute targets you want to run on.</span><span class="sxs-lookup"><span data-stu-id="f8f24-133">This installation needs to be done both on your local machine and on any compute targets you want to run on.</span></span>

<span data-ttu-id="f8f24-134">To install your packages in a compute target, you have to modify the conda_dependencies.yml file located in the aml_config folder under the root of your project.</span><span class="sxs-lookup"><span data-stu-id="f8f24-134">To install your packages in a compute target, you have to modify the conda_dependencies.yml file located in the aml_config folder under the root of your project.</span></span>

### <a name="windows"></a><span data-ttu-id="f8f24-135">Windows</span><span class="sxs-lookup"><span data-stu-id="f8f24-135">Windows</span></span> 
<span data-ttu-id="f8f24-136">To find the location on Windows, find the app-specific installation of Python and its scripts directory.</span><span class="sxs-lookup"><span data-stu-id="f8f24-136">To find the location on Windows, find the app-specific installation of Python and its scripts directory.</span></span> <span data-ttu-id="f8f24-137">The default location is:</span><span class="sxs-lookup"><span data-stu-id="f8f24-137">The default location is:</span></span>  

`C:\Users\<user>\AppData\Local\AmlWorkbench\Python\Scripts` 

<span data-ttu-id="f8f24-138">Then run either of the following commands:</span><span class="sxs-lookup"><span data-stu-id="f8f24-138">Then run either of the following commands:</span></span> 

`conda install <libraryname>` 

<span data-ttu-id="f8f24-139">or</span><span class="sxs-lookup"><span data-stu-id="f8f24-139">or</span></span> 

`pip install <libraryname> `

### <a name="mac"></a><span data-ttu-id="f8f24-140">Mac</span><span class="sxs-lookup"><span data-stu-id="f8f24-140">Mac</span></span> 
<span data-ttu-id="f8f24-141">To find the location on a Mac, find the app-specific installation of Python and its scripts directory.</span><span class="sxs-lookup"><span data-stu-id="f8f24-141">To find the location on a Mac, find the app-specific installation of Python and its scripts directory.</span></span> <span data-ttu-id="f8f24-142">The default location is:</span><span class="sxs-lookup"><span data-stu-id="f8f24-142">The default location is:</span></span> 

`/Users/<user>/Library/Caches/AmlWorkbench/Python/bin` 

<span data-ttu-id="f8f24-143">Then run either of the following commands:</span><span class="sxs-lookup"><span data-stu-id="f8f24-143">Then run either of the following commands:</span></span> 

`./conda install <libraryname>`

<span data-ttu-id="f8f24-144">or</span><span class="sxs-lookup"><span data-stu-id="f8f24-144">or</span></span> 

`./pip install <libraryname>`

## <a name="use-custom-modules"></a><span data-ttu-id="f8f24-145">Use custom modules</span><span class="sxs-lookup"><span data-stu-id="f8f24-145">Use custom modules</span></span>
<span data-ttu-id="f8f24-146">In Transform Dataflow (Script), write the following Python code</span><span class="sxs-lookup"><span data-stu-id="f8f24-146">In Transform Dataflow (Script), write the following Python code</span></span>

```python
import sys
sys.path.append(*<absolute path to the directory containing UserModule.py>*)

from UserModule import ExtensionFunction1
df = ExtensionFunction1(df)
```

<span data-ttu-id="f8f24-147">In Add Column (Script), set Code Block Type = Module, and write the following Python code</span><span class="sxs-lookup"><span data-stu-id="f8f24-147">In Add Column (Script), set Code Block Type = Module, and write the following Python code</span></span>

```python 
import sys
sys.path.append(*<absolute path to the directory containing UserModule.py>*)

from UserModule import ExtensionFunction2

def newvalue(row):
    return ExtensionFunction2(row)
```
<span data-ttu-id="f8f24-148">For different execution contexts (local, Docker, Spark), point absolute path to the right place.</span><span class="sxs-lookup"><span data-stu-id="f8f24-148">For different execution contexts (local, Docker, Spark), point absolute path to the right place.</span></span> <span data-ttu-id="f8f24-149">You may want to use “os.getcwd() + relativePath” to locate it.</span><span class="sxs-lookup"><span data-stu-id="f8f24-149">You may want to use “os.getcwd() + relativePath” to locate it.</span></span>


## <a name="column-data"></a><span data-ttu-id="f8f24-150">Column data</span><span class="sxs-lookup"><span data-stu-id="f8f24-150">Column data</span></span> 
<span data-ttu-id="f8f24-151">Column data can be accessed from a row by using dot notation or key-value notation.</span><span class="sxs-lookup"><span data-stu-id="f8f24-151">Column data can be accessed from a row by using dot notation or key-value notation.</span></span> <span data-ttu-id="f8f24-152">Column names that contain spaces or special characters can't be accessed by using dot notation.</span><span class="sxs-lookup"><span data-stu-id="f8f24-152">Column names that contain spaces or special characters can't be accessed by using dot notation.</span></span> <span data-ttu-id="f8f24-153">The `row` variable should always be defined in both modes of Python extensions (Module and Expression).</span><span class="sxs-lookup"><span data-stu-id="f8f24-153">The `row` variable should always be defined in both modes of Python extensions (Module and Expression).</span></span> 

<span data-ttu-id="f8f24-154">Examples</span><span class="sxs-lookup"><span data-stu-id="f8f24-154">Examples</span></span> 

```python
    row.ColumnA + row.ColumnB  
    row["ColumnA"] + row["ColumnB"]
```

## <a name="add-column"></a><span data-ttu-id="f8f24-155">Add Column</span><span class="sxs-lookup"><span data-stu-id="f8f24-155">Add Column</span></span> 
### <a name="purpose"></a><span data-ttu-id="f8f24-156">Purpose</span><span class="sxs-lookup"><span data-stu-id="f8f24-156">Purpose</span></span>
<span data-ttu-id="f8f24-157">The Add Column extension point lets you write Python to calculate a new column.</span><span class="sxs-lookup"><span data-stu-id="f8f24-157">The Add Column extension point lets you write Python to calculate a new column.</span></span> <span data-ttu-id="f8f24-158">The code you write has access to the full row.</span><span class="sxs-lookup"><span data-stu-id="f8f24-158">The code you write has access to the full row.</span></span> <span data-ttu-id="f8f24-159">It needs to return a new column value for each row.</span><span class="sxs-lookup"><span data-stu-id="f8f24-159">It needs to return a new column value for each row.</span></span> 

### <a name="how-to-use"></a><span data-ttu-id="f8f24-160">How to use</span><span class="sxs-lookup"><span data-stu-id="f8f24-160">How to use</span></span>
<span data-ttu-id="f8f24-161">You can add this extension point by using the Add Column (Script) block.</span><span class="sxs-lookup"><span data-stu-id="f8f24-161">You can add this extension point by using the Add Column (Script) block.</span></span> <span data-ttu-id="f8f24-162">It's available on the top-level **Transformations** menu, as well as on the **Column** context menu.</span><span class="sxs-lookup"><span data-stu-id="f8f24-162">It's available on the top-level **Transformations** menu, as well as on the **Column** context menu.</span></span> 

### <a name="syntax"></a><span data-ttu-id="f8f24-163">Syntax</span><span class="sxs-lookup"><span data-stu-id="f8f24-163">Syntax</span></span>
<span data-ttu-id="f8f24-164">Expression</span><span class="sxs-lookup"><span data-stu-id="f8f24-164">Expression</span></span>

```python
    math.log(row["Score"])
```

<span data-ttu-id="f8f24-165">Module</span><span class="sxs-lookup"><span data-stu-id="f8f24-165">Module</span></span> 

```python
def newvalue(row):  
     return math.log(row["Score"])
```
 

## <a name="advanced-filter"></a><span data-ttu-id="f8f24-166">Advanced Filter</span><span class="sxs-lookup"><span data-stu-id="f8f24-166">Advanced Filter</span></span>
### <a name="purpose"></a><span data-ttu-id="f8f24-167">Purpose</span><span class="sxs-lookup"><span data-stu-id="f8f24-167">Purpose</span></span> 
<span data-ttu-id="f8f24-168">The Advanced Filter extension point lets you write a custom filter.</span><span class="sxs-lookup"><span data-stu-id="f8f24-168">The Advanced Filter extension point lets you write a custom filter.</span></span> <span data-ttu-id="f8f24-169">You have access to the entire row, and your code must return True (include the row) or False (exclude the row).</span><span class="sxs-lookup"><span data-stu-id="f8f24-169">You have access to the entire row, and your code must return True (include the row) or False (exclude the row).</span></span> 

### <a name="how-to-use"></a><span data-ttu-id="f8f24-170">How to use</span><span class="sxs-lookup"><span data-stu-id="f8f24-170">How to use</span></span>
<span data-ttu-id="f8f24-171">You can add this extension point by using the Advanced Filter (Script) block.</span><span class="sxs-lookup"><span data-stu-id="f8f24-171">You can add this extension point by using the Advanced Filter (Script) block.</span></span> <span data-ttu-id="f8f24-172">It's available on the top-level **Transformations** menu.</span><span class="sxs-lookup"><span data-stu-id="f8f24-172">It's available on the top-level **Transformations** menu.</span></span> 

### <a name="syntax"></a><span data-ttu-id="f8f24-173">Syntax</span><span class="sxs-lookup"><span data-stu-id="f8f24-173">Syntax</span></span>

<span data-ttu-id="f8f24-174">Expression</span><span class="sxs-lookup"><span data-stu-id="f8f24-174">Expression</span></span>

```python
    row["Score"] > 95
```

<span data-ttu-id="f8f24-175">Module</span><span class="sxs-lookup"><span data-stu-id="f8f24-175">Module</span></span>  

```python
def includerow(row):  
    return row["Score"] > 95
```
 

## <a name="transform-dataflow"></a><span data-ttu-id="f8f24-176">Transform Dataflow</span><span class="sxs-lookup"><span data-stu-id="f8f24-176">Transform Dataflow</span></span>
### <a name="purpose"></a><span data-ttu-id="f8f24-177">Purpose</span><span class="sxs-lookup"><span data-stu-id="f8f24-177">Purpose</span></span> 
<span data-ttu-id="f8f24-178">The Transform Dataflow extension point lets you completely transform the data flow.</span><span class="sxs-lookup"><span data-stu-id="f8f24-178">The Transform Dataflow extension point lets you completely transform the data flow.</span></span> <span data-ttu-id="f8f24-179">You have access to a Pandas dataframe that contains all the columns and rows that you're processing.</span><span class="sxs-lookup"><span data-stu-id="f8f24-179">You have access to a Pandas dataframe that contains all the columns and rows that you're processing.</span></span> <span data-ttu-id="f8f24-180">Your code must return a Pandas dataframe with the new data.</span><span class="sxs-lookup"><span data-stu-id="f8f24-180">Your code must return a Pandas dataframe with the new data.</span></span> 

>[!NOTE]
><span data-ttu-id="f8f24-181">In Python, all the data to be loaded into memory is in a Pandas dataframe if this extension is used.</span><span class="sxs-lookup"><span data-stu-id="f8f24-181">In Python, all the data to be loaded into memory is in a Pandas dataframe if this extension is used.</span></span> 
>
><span data-ttu-id="f8f24-182">In Spark, all the data is collected onto a single worker node.</span><span class="sxs-lookup"><span data-stu-id="f8f24-182">In Spark, all the data is collected onto a single worker node.</span></span> <span data-ttu-id="f8f24-183">If the data is very large, a worker might run out of memory.</span><span class="sxs-lookup"><span data-stu-id="f8f24-183">If the data is very large, a worker might run out of memory.</span></span> <span data-ttu-id="f8f24-184">Use it carefully.</span><span class="sxs-lookup"><span data-stu-id="f8f24-184">Use it carefully.</span></span>

### <a name="how-to-use"></a><span data-ttu-id="f8f24-185">How to use</span><span class="sxs-lookup"><span data-stu-id="f8f24-185">How to use</span></span> 
<span data-ttu-id="f8f24-186">You can add this extension point by using the Transform Dataflow (Script) block.</span><span class="sxs-lookup"><span data-stu-id="f8f24-186">You can add this extension point by using the Transform Dataflow (Script) block.</span></span> <span data-ttu-id="f8f24-187">It's available on the top-level **Transformations** menu.</span><span class="sxs-lookup"><span data-stu-id="f8f24-187">It's available on the top-level **Transformations** menu.</span></span> 
### <a name="syntax"></a><span data-ttu-id="f8f24-188">Syntax</span><span class="sxs-lookup"><span data-stu-id="f8f24-188">Syntax</span></span> 

<span data-ttu-id="f8f24-189">Expression</span><span class="sxs-lookup"><span data-stu-id="f8f24-189">Expression</span></span>

```python
    df['index-column'] = range(1, len(df) + 1)  
    df = df.reset_index()
```
 

<span data-ttu-id="f8f24-190">Module</span><span class="sxs-lookup"><span data-stu-id="f8f24-190">Module</span></span> 

```python
def transform(df):  
    df['index-column'] = range(1, len(df) + 1)  
    df = df.reset_index()  
    return df
```
  

## <a name="transform-partition"></a><span data-ttu-id="f8f24-191">Transform Partition</span><span class="sxs-lookup"><span data-stu-id="f8f24-191">Transform Partition</span></span>  
### <a name="purpose"></a><span data-ttu-id="f8f24-192">Purpose</span><span class="sxs-lookup"><span data-stu-id="f8f24-192">Purpose</span></span> 
<span data-ttu-id="f8f24-193">The Transform Partition extension point lets you transform a partition of the data flow.</span><span class="sxs-lookup"><span data-stu-id="f8f24-193">The Transform Partition extension point lets you transform a partition of the data flow.</span></span> <span data-ttu-id="f8f24-194">You have access to a Pandas dataframe that contains all the columns and rows for that partition.</span><span class="sxs-lookup"><span data-stu-id="f8f24-194">You have access to a Pandas dataframe that contains all the columns and rows for that partition.</span></span> <span data-ttu-id="f8f24-195">Your code must return a Pandas dataframe with the new data.</span><span class="sxs-lookup"><span data-stu-id="f8f24-195">Your code must return a Pandas dataframe with the new data.</span></span> 

>[!NOTE]
><span data-ttu-id="f8f24-196">In Python, you might end up with a single partition or multiple partitions, depending on the size of your data.</span><span class="sxs-lookup"><span data-stu-id="f8f24-196">In Python, you might end up with a single partition or multiple partitions, depending on the size of your data.</span></span> <span data-ttu-id="f8f24-197">In Spark, you're working with a dataframe that holds the data for a partition on a given worker node.</span><span class="sxs-lookup"><span data-stu-id="f8f24-197">In Spark, you're working with a dataframe that holds the data for a partition on a given worker node.</span></span> <span data-ttu-id="f8f24-198">In both cases, you can't assume that you have access to the entire data set.</span><span class="sxs-lookup"><span data-stu-id="f8f24-198">In both cases, you can't assume that you have access to the entire data set.</span></span> 


### <a name="how-to-use"></a><span data-ttu-id="f8f24-199">How to use</span><span class="sxs-lookup"><span data-stu-id="f8f24-199">How to use</span></span>
<span data-ttu-id="f8f24-200">You can add this extension point by using the Transform Partition (Script) block.</span><span class="sxs-lookup"><span data-stu-id="f8f24-200">You can add this extension point by using the Transform Partition (Script) block.</span></span> <span data-ttu-id="f8f24-201">It's available on the top-level **Transformations** menu.</span><span class="sxs-lookup"><span data-stu-id="f8f24-201">It's available on the top-level **Transformations** menu.</span></span> 

### <a name="syntax"></a><span data-ttu-id="f8f24-202">Syntax</span><span class="sxs-lookup"><span data-stu-id="f8f24-202">Syntax</span></span> 

<span data-ttu-id="f8f24-203">Expression</span><span class="sxs-lookup"><span data-stu-id="f8f24-203">Expression</span></span> 

```python
    df['partition-id'] = index  
    df['index-column'] = range(1, len(df) + 1)  
    df = df.reset_index()
```
 

<span data-ttu-id="f8f24-204">Module</span><span class="sxs-lookup"><span data-stu-id="f8f24-204">Module</span></span> 

```python
def transform(df, index):
    df['partition-id'] = index
    df['index-column'] = range(1, len(df) + 1)
    df = df.reset_index()
    return df
```


## <a name="datapreperror"></a><span data-ttu-id="f8f24-205">DataPrepError</span><span class="sxs-lookup"><span data-stu-id="f8f24-205">DataPrepError</span></span>  
### <a name="error-values"></a><span data-ttu-id="f8f24-206">Error values</span><span class="sxs-lookup"><span data-stu-id="f8f24-206">Error values</span></span>  
<span data-ttu-id="f8f24-207">In Data Preparations, the concept of error values exists.</span><span class="sxs-lookup"><span data-stu-id="f8f24-207">In Data Preparations, the concept of error values exists.</span></span> 

<span data-ttu-id="f8f24-208">It's possible to encounter error values in custom Python code.</span><span class="sxs-lookup"><span data-stu-id="f8f24-208">It's possible to encounter error values in custom Python code.</span></span> <span data-ttu-id="f8f24-209">They are instances of a Python class called `DataPrepError`.</span><span class="sxs-lookup"><span data-stu-id="f8f24-209">They are instances of a Python class called `DataPrepError`.</span></span> <span data-ttu-id="f8f24-210">This class wraps a Python exception and has a couple of properties.</span><span class="sxs-lookup"><span data-stu-id="f8f24-210">This class wraps a Python exception and has a couple of properties.</span></span> <span data-ttu-id="f8f24-211">The properties contain information about the error that occurred when the original value was processed, as well as the original value.</span><span class="sxs-lookup"><span data-stu-id="f8f24-211">The properties contain information about the error that occurred when the original value was processed, as well as the original value.</span></span> 


### <a name="datapreperror-class-definition"></a><span data-ttu-id="f8f24-212">DataPrepError class definition</span><span class="sxs-lookup"><span data-stu-id="f8f24-212">DataPrepError class definition</span></span>
```python 
class DataPrepError(Exception): 
    def __bool__(self): 
        return False 
``` 
<span data-ttu-id="f8f24-213">The creation of a DataPrepError in the Data Preparations Python framework generally looks like this:</span><span class="sxs-lookup"><span data-stu-id="f8f24-213">The creation of a DataPrepError in the Data Preparations Python framework generally looks like this:</span></span> 
```python 
DataPrepError({ 
   'message':'Cannot convert to numeric value', 
   'originalValue': value, 
   'exceptionMessage': e.args[0], 
   '__errorCode__':'Microsoft.DPrep.ErrorValues.InvalidNumericType' 
}) 
``` 
#### <a name="how-to-use"></a><span data-ttu-id="f8f24-214">How to use</span><span class="sxs-lookup"><span data-stu-id="f8f24-214">How to use</span></span> 
<span data-ttu-id="f8f24-215">It's possible when Python runs at an extension point to generate DataPrepErrors as return values by using the previous creation method.</span><span class="sxs-lookup"><span data-stu-id="f8f24-215">It's possible when Python runs at an extension point to generate DataPrepErrors as return values by using the previous creation method.</span></span> <span data-ttu-id="f8f24-216">It's much more likely that DataPrepErrors are encountered when data is processed at an extension point.</span><span class="sxs-lookup"><span data-stu-id="f8f24-216">It's much more likely that DataPrepErrors are encountered when data is processed at an extension point.</span></span> <span data-ttu-id="f8f24-217">At this point, the custom Python code needs to handle a DataPrepError as a valid data type.</span><span class="sxs-lookup"><span data-stu-id="f8f24-217">At this point, the custom Python code needs to handle a DataPrepError as a valid data type.</span></span>

#### <a name="syntax"></a><span data-ttu-id="f8f24-218">Syntax</span><span class="sxs-lookup"><span data-stu-id="f8f24-218">Syntax</span></span> 
<span data-ttu-id="f8f24-219">Expression</span><span class="sxs-lookup"><span data-stu-id="f8f24-219">Expression</span></span> 
```python 
    if (isinstance(row["Score"], DataPrepError)): 
        row["Score"].originalValue 
    else: 
        row["Score"] 
``` 
```python 
    if (hasattr(row["Score"], "originalValue")): 
        row["Score"].originalValue 
    else: 
        row["Score"] 
``` 
<span data-ttu-id="f8f24-220">Module</span><span class="sxs-lookup"><span data-stu-id="f8f24-220">Module</span></span> 
```python 
def newvalue(row): 
    if (isinstance(row["Score"], DataPrepError)): 
        return row["Score"].originalValue 
    else: 
        return row["Score"] 
``` 
```python 
def newvalue(row): 
    if (hasattr(row["Score"], "originalValue")): 
        return row["Score"].originalValue 
    else: 
        return row["Score"] 
```  
