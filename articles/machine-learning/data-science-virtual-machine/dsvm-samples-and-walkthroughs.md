---
title: Samples and walkthroughs for the Data Science Virtual Machine - Azure | Microsoft Docs
description: Samples and walkthroughs for the Data Science Virtual Machine.
keywords: data science tools, data science virtual machine, tools for data science, linux data science
services: machine-learning
documentationcenter: ''
author: gopitk
manager: cgronlun
ms.assetid: ''
ms.service: machine-learning
ms.component: data-science-vm
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/11/2017
ms.author: gokuma
ms.openlocfilehash: 3e3ee232b6342601e44d728148d32e70e6f3f00b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871402"
---
# <a name="samples-on-the-data-science-virtual-machines-dsvm"></a><span data-ttu-id="39380-104">Samples on the Data Science Virtual Machines (DSVM)</span><span class="sxs-lookup"><span data-stu-id="39380-104">Samples on the Data Science Virtual Machines (DSVM)</span></span>

<span data-ttu-id="39380-105">The DSVMs come with included fully worked-out samples in the form of Jupyter Notebooks and some that are not based on Jupyter.</span><span class="sxs-lookup"><span data-stu-id="39380-105">The DSVMs come with included fully worked-out samples in the form of Jupyter Notebooks and some that are not based on Jupyter.</span></span> <span data-ttu-id="39380-106">You can access Jupyter by clicking on the `Jupyter` icon on the desktop or application menu.</span><span class="sxs-lookup"><span data-stu-id="39380-106">You can access Jupyter by clicking on the `Jupyter` icon on the desktop or application menu.</span></span>  
> [!NOTE]
> <span data-ttu-id="39380-107">Refer to [Access Jupyter](#access-jupyter) section to enable Jupyter Notebooks on your DSVM.</span><span class="sxs-lookup"><span data-stu-id="39380-107">Refer to [Access Jupyter](#access-jupyter) section to enable Jupyter Notebooks on your DSVM.</span></span>

## <a name="quick-reference-of-samples"></a><span data-ttu-id="39380-108">Quick Reference of Samples</span><span class="sxs-lookup"><span data-stu-id="39380-108">Quick Reference of Samples</span></span>
| <span data-ttu-id="39380-109">Samples Category</span><span class="sxs-lookup"><span data-stu-id="39380-109">Samples Category</span></span> | <span data-ttu-id="39380-110">Description</span><span class="sxs-lookup"><span data-stu-id="39380-110">Description</span></span> | <span data-ttu-id="39380-111">Locations</span><span class="sxs-lookup"><span data-stu-id="39380-111">Locations</span></span> |
| ------------- | ------------- | ------------- |
| <span data-ttu-id="39380-112">**R** Language</span><span class="sxs-lookup"><span data-stu-id="39380-112">**R** Language</span></span>  | <span data-ttu-id="39380-113">Samples in **R** explaining scenarios like connecting with Azure cloud data stores, Comparing Open Source R and Microsoft R & operationalizing Models on Microsoft R Server or SQL Server.</span><span class="sxs-lookup"><span data-stu-id="39380-113">Samples in **R** explaining scenarios like connecting with Azure cloud data stores, Comparing Open Source R and Microsoft R & operationalizing Models on Microsoft R Server or SQL Server.</span></span> <br/> [<span data-ttu-id="39380-114">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-114">Screenshot</span></span>](#r-language) | <br/>`~notebooks` <br/> <br/> `~samples/MicrosoftR` <br/> <br/> `~samples/RSqlDemo` <br/> <br/> `~samples/SQLRServices`<br/> <br/>|
| <span data-ttu-id="39380-115">**Python** Language</span><span class="sxs-lookup"><span data-stu-id="39380-115">**Python** Language</span></span>  | <span data-ttu-id="39380-116">Samples in **Python** explaining scenarios like connecting with Azure cloud data stores and working with **Azure Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="39380-116">Samples in **Python** explaining scenarios like connecting with Azure cloud data stores and working with **Azure Machine Learning**.</span></span>  <br/> [<span data-ttu-id="39380-117">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-117">Screenshot</span></span>](#python-language) | <br/>`~notebooks` <br/><br/>|
| <span data-ttu-id="39380-118">**Julia** Language</span><span class="sxs-lookup"><span data-stu-id="39380-118">**Julia** Language</span></span>  | <span data-ttu-id="39380-119">Sample in **Julia** that detail Plotting in Julia, deep learning in Julia, calling C and Python from Julia etc.</span><span class="sxs-lookup"><span data-stu-id="39380-119">Sample in **Julia** that detail Plotting in Julia, deep learning in Julia, calling C and Python from Julia etc.</span></span> <br/> [<span data-ttu-id="39380-120">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-120">Screenshot</span></span>](#julia-language) |<br/> <span data-ttu-id="39380-121">**Windows**:</span><span class="sxs-lookup"><span data-stu-id="39380-121">**Windows**:</span></span><br/> `~notebooks/Julia_notebooks`<br/><br/>`~notebooks`<br/><br/> <span data-ttu-id="39380-122">**Linux**:</span><span class="sxs-lookup"><span data-stu-id="39380-122">**Linux**:</span></span><br/> `~notebooks/julia`<br/><br/> |
| <span data-ttu-id="39380-123">**CNTK**</span><span class="sxs-lookup"><span data-stu-id="39380-123">**CNTK**</span></span> <br/> <span data-ttu-id="39380-124">(Microsoft Cognitive Toolkit)</span><span class="sxs-lookup"><span data-stu-id="39380-124">(Microsoft Cognitive Toolkit)</span></span>  | <span data-ttu-id="39380-125">Deep learning samples published by the Cognitive Toolkit team at Microsoft.</span><span class="sxs-lookup"><span data-stu-id="39380-125">Deep learning samples published by the Cognitive Toolkit team at Microsoft.</span></span>  <br/> [<span data-ttu-id="39380-126">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-126">Screenshot</span></span>](#cntk) | <br/><span data-ttu-id="39380-127">**Windows**:</span><span class="sxs-lookup"><span data-stu-id="39380-127">**Windows**:</span></span><br/> `~notebooks/CNTK/Tutorials`<br/><br/>`~/samples/CNTK-Samples-2-0/Examples`<br/><br/> <span data-ttu-id="39380-128">**Linux**:</span><span class="sxs-lookup"><span data-stu-id="39380-128">**Linux**:</span></span><br/> `~notebooks/CNTK`<br/> <br/>|
| <span data-ttu-id="39380-129">**MXNet** Notebooks</span><span class="sxs-lookup"><span data-stu-id="39380-129">**MXNet** Notebooks</span></span>  | <span data-ttu-id="39380-130">Deep Learning samples utilizing **MXNet** based neural networks.</span><span class="sxs-lookup"><span data-stu-id="39380-130">Deep Learning samples utilizing **MXNet** based neural networks.</span></span> <span data-ttu-id="39380-131">There are a variety of notebooks ranging from beginner to advanced scenarios.</span><span class="sxs-lookup"><span data-stu-id="39380-131">There are a variety of notebooks ranging from beginner to advanced scenarios.</span></span>  <br/> [<span data-ttu-id="39380-132">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-132">Screenshot</span></span>](#mxnet) | <br/>`~notebooks/mxnet`<br/> <br/>|
| <span data-ttu-id="39380-133">**Azure Machine Learning** AzureML</span><span class="sxs-lookup"><span data-stu-id="39380-133">**Azure Machine Learning** AzureML</span></span>  | <span data-ttu-id="39380-134">Interacting with **Azure Machine Learning** Studio and creating web-service endpoints from locally trained models, for cloud-based scoring workflows.</span><span class="sxs-lookup"><span data-stu-id="39380-134">Interacting with **Azure Machine Learning** Studio and creating web-service endpoints from locally trained models, for cloud-based scoring workflows.</span></span> <br/> [<span data-ttu-id="39380-135">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-135">Screenshot</span></span>](#azureml) | <br/>`~notebooks/azureml`<br/> <br/>|
| <span data-ttu-id="39380-136">**caffe2**</span><span class="sxs-lookup"><span data-stu-id="39380-136">**caffe2**</span></span> | <span data-ttu-id="39380-137">Deep Learning samples utilizing **caffe2** based neural networks.</span><span class="sxs-lookup"><span data-stu-id="39380-137">Deep Learning samples utilizing **caffe2** based neural networks.</span></span> <span data-ttu-id="39380-138">There are several notebooks designed to familiarize users with caffe2 and how to use it effectively, including examples like image pre-processing, dataset creation, Regression, and using pre-trained models.</span><span class="sxs-lookup"><span data-stu-id="39380-138">There are several notebooks designed to familiarize users with caffe2 and how to use it effectively, including examples like image pre-processing, dataset creation, Regression, and using pre-trained models.</span></span> <br/> [<span data-ttu-id="39380-139">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-139">Screenshot</span></span>](#caffe2) | <br/>`~notebooks/caffe2`<br/><br/> |
| <span data-ttu-id="39380-140">**H2O**</span><span class="sxs-lookup"><span data-stu-id="39380-140">**H2O**</span></span>   | <span data-ttu-id="39380-141">Python-based samples utilizing **H2O** for numerous real-world scenario problems.</span><span class="sxs-lookup"><span data-stu-id="39380-141">Python-based samples utilizing **H2O** for numerous real-world scenario problems.</span></span> <br/> [<span data-ttu-id="39380-142">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-142">Screenshot</span></span>](#h2o) | <br/>`~notebooks/h2o`<br/><br/> |
| <span data-ttu-id="39380-143">**SparkML** Language</span><span class="sxs-lookup"><span data-stu-id="39380-143">**SparkML** Language</span></span>  | <span data-ttu-id="39380-144">Sample utilizing features and capabilities of Spark's **MLlib** toolkit through **pySpark 2.0** on **Apache Spark 2.0**.</span><span class="sxs-lookup"><span data-stu-id="39380-144">Sample utilizing features and capabilities of Spark's **MLlib** toolkit through **pySpark 2.0** on **Apache Spark 2.0**.</span></span>  <br/> [<span data-ttu-id="39380-145">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-145">Screenshot</span></span>](#sparkml) | <br/>`~notebooks/SparkML/pySpark`<br/><br/> |
| <span data-ttu-id="39380-146">**MMLSpark** Language</span><span class="sxs-lookup"><span data-stu-id="39380-146">**MMLSpark** Language</span></span>  | <span data-ttu-id="39380-147">A variety of samples utilizing **MMLSpark - Microsoft Machine Learning for Apache Spark**, which is a framework that provides a number of deep learning and data science tools for **Apache Spark**.</span><span class="sxs-lookup"><span data-stu-id="39380-147">A variety of samples utilizing **MMLSpark - Microsoft Machine Learning for Apache Spark**, which is a framework that provides a number of deep learning and data science tools for **Apache Spark**.</span></span> <br/> [<span data-ttu-id="39380-148">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-148">Screenshot</span></span>](#sparkml) | <br/>`~notebooks/MMLSpark`<br/><br/> |
| <span data-ttu-id="39380-149">**TensorFlow**</span><span class="sxs-lookup"><span data-stu-id="39380-149">**TensorFlow**</span></span>  | <span data-ttu-id="39380-150">Multiple different Neural Network Samples and techniques implemented using the **TensorFlow** framework.</span><span class="sxs-lookup"><span data-stu-id="39380-150">Multiple different Neural Network Samples and techniques implemented using the **TensorFlow** framework.</span></span> <br/> [<span data-ttu-id="39380-151">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-151">Screenshot</span></span>](#tensorflow) | <br/>`~notebooks/tensorflow`<br/><br/> |
| <span data-ttu-id="39380-152">**XGBoost**</span><span class="sxs-lookup"><span data-stu-id="39380-152">**XGBoost**</span></span> | <span data-ttu-id="39380-153">Standard Machine Learning samples in **XGBoost** for scenarios like classification, regression etc.</span><span class="sxs-lookup"><span data-stu-id="39380-153">Standard Machine Learning samples in **XGBoost** for scenarios like classification, regression etc.</span></span> <br/> [<span data-ttu-id="39380-154">Screenshot</span><span class="sxs-lookup"><span data-stu-id="39380-154">Screenshot</span></span>](#xgboost) | <br/>`~samples/xgboost/demo`<br/><br/> |

<br/>

## <a name="access-jupyter"></a><span data-ttu-id="39380-155">Access Jupyter</span><span class="sxs-lookup"><span data-stu-id="39380-155">Access Jupyter</span></span> 

<span data-ttu-id="39380-156">Visit Jupyter Home by going to **`https://localhost:9999`** on Windows or **`https://localhost:8000`** on Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="39380-156">Visit Jupyter Home by going to **`https://localhost:9999`** on Windows or **`https://localhost:8000`** on Ubuntu.</span></span>


### <a name="enabling-jupyter-access-from-browser"></a><span data-ttu-id="39380-157">Enabling Jupyter access from Browser</span><span class="sxs-lookup"><span data-stu-id="39380-157">Enabling Jupyter access from Browser</span></span>

<span data-ttu-id="39380-158">**Windows DSVM**</span><span class="sxs-lookup"><span data-stu-id="39380-158">**Windows DSVM**</span></span>

<span data-ttu-id="39380-159">Run **`Jupyter SetPassword`** from the desktop shortcut and follow the prompt to set/reset your password for Jupyter and start the Jupyter process.</span><span class="sxs-lookup"><span data-stu-id="39380-159">Run **`Jupyter SetPassword`** from the desktop shortcut and follow the prompt to set/reset your password for Jupyter and start the Jupyter process.</span></span> 
<br/><span data-ttu-id="39380-160">![Enable Jupyter Exception](./media/jupyter-setpassword.png)</span><span class="sxs-lookup"><span data-stu-id="39380-160">![Enable Jupyter Exception](./media/jupyter-setpassword.png)</span></span><br/>
<span data-ttu-id="39380-161">You can access Jupyter Home once the Jupyter process has successfully started on your VM by visiting **`https://localhost:9999`** on your browser.</span><span class="sxs-lookup"><span data-stu-id="39380-161">You can access Jupyter Home once the Jupyter process has successfully started on your VM by visiting **`https://localhost:9999`** on your browser.</span></span> <span data-ttu-id="39380-162">See screenshot to add exception and enable Jupyter access over the browser</span><span class="sxs-lookup"><span data-stu-id="39380-162">See screenshot to add exception and enable Jupyter access over the browser</span></span>
<br/><span data-ttu-id="39380-163">![Enable Jupyter Exception](./media/windows-jupyter-exception.png)</span><span class="sxs-lookup"><span data-stu-id="39380-163">![Enable Jupyter Exception](./media/windows-jupyter-exception.png)</span></span><br/>
<span data-ttu-id="39380-164">Sign in with the new password you had just set.</span><span class="sxs-lookup"><span data-stu-id="39380-164">Sign in with the new password you had just set.</span></span>
<br/>
<span data-ttu-id="39380-165">**Linux DSVM**</span><span class="sxs-lookup"><span data-stu-id="39380-165">**Linux DSVM**</span></span>

<span data-ttu-id="39380-166">You can access Jupyter Home on your VM by visiting **`https://localhost:8000`** on your browser.</span><span class="sxs-lookup"><span data-stu-id="39380-166">You can access Jupyter Home on your VM by visiting **`https://localhost:8000`** on your browser.</span></span> <span data-ttu-id="39380-167">See screenshot to add exception and enable Jupyter access over the browser.</span><span class="sxs-lookup"><span data-stu-id="39380-167">See screenshot to add exception and enable Jupyter access over the browser.</span></span>
<br/><span data-ttu-id="39380-168">![Enable Jupyter Exception](./media/ubuntu-jupyter-exception.png)</span><span class="sxs-lookup"><span data-stu-id="39380-168">![Enable Jupyter Exception](./media/ubuntu-jupyter-exception.png)</span></span><br/>
<span data-ttu-id="39380-169">Sign in with the same password as your login for the DSVM.</span><span class="sxs-lookup"><span data-stu-id="39380-169">Sign in with the same password as your login for the DSVM.</span></span>
<br/>

<span data-ttu-id="39380-170">**Jupyter Home**</span><span class="sxs-lookup"><span data-stu-id="39380-170">**Jupyter Home**</span></span>
<br/><span data-ttu-id="39380-171">![Jupyter Home](./media/jupyter-home.png)</span><span class="sxs-lookup"><span data-stu-id="39380-171">![Jupyter Home](./media/jupyter-home.png)</span></span><br/>

## <a name="r-language"></a><span data-ttu-id="39380-172">R Language</span><span class="sxs-lookup"><span data-stu-id="39380-172">R Language</span></span> 
<br/>![R Samples](./media/r-language-samples.png)<br/>

## <a name="python-language"></a><span data-ttu-id="39380-174">Python Language</span><span class="sxs-lookup"><span data-stu-id="39380-174">Python Language</span></span>
<br/>![Python Samples](./media/python-language-samples.png)<br/>

## <a name="julia-language"></a><span data-ttu-id="39380-176">Julia Language</span><span class="sxs-lookup"><span data-stu-id="39380-176">Julia Language</span></span> 
<br/>![Julia Samples](./media/julia-samples.png)<br/>

## <a name="cntk"></a><span data-ttu-id="39380-178">CNTK</span><span class="sxs-lookup"><span data-stu-id="39380-178">CNTK</span></span> 
<br/><span data-ttu-id="39380-179">![CNTK Samples](./media/cntk-samples2.png)</span><span class="sxs-lookup"><span data-stu-id="39380-179">![CNTK Samples](./media/cntk-samples2.png)</span></span><br/>
<br/><span data-ttu-id="39380-180">![CNTK Samples](./media/cntk-samples.png)</span><span class="sxs-lookup"><span data-stu-id="39380-180">![CNTK Samples](./media/cntk-samples.png)</span></span><br/>

## <a name="mxnet"></a><span data-ttu-id="39380-181">MXNet</span><span class="sxs-lookup"><span data-stu-id="39380-181">MXNet</span></span>
<br/>![MXnet Samples](./media/mxnet-samples.png)<br/>

## <a name="azureml"></a><span data-ttu-id="39380-183">AzureML</span><span class="sxs-lookup"><span data-stu-id="39380-183">AzureML</span></span> 
<br/>![AzurekML Samples](./media/azureml-samples.png)<br/>

## <a name="caffe2"></a><span data-ttu-id="39380-185">caffe2</span><span class="sxs-lookup"><span data-stu-id="39380-185">caffe2</span></span> 
<br/>![caffe2 Samples](./media/caffe2-samples.png)<br/>

## <a name="h2o"></a><span data-ttu-id="39380-187">H2O</span><span class="sxs-lookup"><span data-stu-id="39380-187">H2O</span></span> 
<br/>![H2O Samples](./media/h2o-samples.png)<br/>

## <a name="sparkml"></a><span data-ttu-id="39380-189">SparkML</span><span class="sxs-lookup"><span data-stu-id="39380-189">SparkML</span></span> 
<br/>![SparkML Samples](./media/sparkml-samples.png)<br/>

## <a name="tensorflow"></a><span data-ttu-id="39380-191">TensorFlow</span><span class="sxs-lookup"><span data-stu-id="39380-191">TensorFlow</span></span> 
<br/>![TensorFlow Samples](./media/tensorflow-samples.png)<br/>

## <a name="xgboost"></a><span data-ttu-id="39380-193">XGBoost</span><span class="sxs-lookup"><span data-stu-id="39380-193">XGBoost</span></span> 
<br/>![XGBoost Samples](./media/xgboost-samples.png)<br/>

