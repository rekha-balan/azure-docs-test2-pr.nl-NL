---
title: Deep Learning and AI frameworks - Azure | Microsoft Docs
description: Deep Learning and AI frameworks
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
ms.openlocfilehash: 891059a440189112c834f3402725781a6b4a3960
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967734"
---
# <a name="deep-learning-and-ai-frameworks"></a><span data-ttu-id="734a5-104">Deep Learning and AI frameworks</span><span class="sxs-lookup"><span data-stu-id="734a5-104">Deep Learning and AI frameworks</span></span>
<span data-ttu-id="734a5-105">The [Data Science Virtual Machine](http://aka.ms/dsvm) (DSVM) and the [Deep Learning VM](http://aka.ms/dsvm/deeplearning) supports a number of deep learning frameworks to help build Artificial Intelligence (AI) applications with predictive analytics and cognitive capabilities like image and language understanding.</span><span class="sxs-lookup"><span data-stu-id="734a5-105">The [Data Science Virtual Machine](http://aka.ms/dsvm) (DSVM) and the [Deep Learning VM](http://aka.ms/dsvm/deeplearning) supports a number of deep learning frameworks to help build Artificial Intelligence (AI) applications with predictive analytics and cognitive capabilities like image and language understanding.</span></span> 

<span data-ttu-id="734a5-106">Here are the details on all the deep learning frameworks available on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="734a5-106">Here are the details on all the deep learning frameworks available on the DSVM.</span></span>

## <a name="microsoft-cognitive-toolkit"></a><span data-ttu-id="734a5-107">Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="734a5-107">Microsoft Cognitive Toolkit</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-108">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-108">What is it?</span></span>   | <span data-ttu-id="734a5-109">Deep learning framework</span><span class="sxs-lookup"><span data-stu-id="734a5-109">Deep learning framework</span></span>      |
| <span data-ttu-id="734a5-110">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-110">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-111">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="734a5-111">Windows, Linux</span></span>     |
| <span data-ttu-id="734a5-112">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-112">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-113">The Microsoft Cognitive Toolkit (CNTK) is installed in Python 3.5 on [Linux and Windows 2012](dsvm-languages.md#python-linux-and-windows-server-2012-edition) and Python 3.6 on [Windows 2016](dsvm-languages.md#python-windows-server-2016-edition).</span><span class="sxs-lookup"><span data-stu-id="734a5-113">The Microsoft Cognitive Toolkit (CNTK) is installed in Python 3.5 on [Linux and Windows 2012](dsvm-languages.md#python-linux-and-windows-server-2012-edition) and Python 3.6 on [Windows 2016](dsvm-languages.md#python-windows-server-2016-edition).</span></span>   |
| <span data-ttu-id="734a5-114">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-114">Links to Samples</span></span>      | <span data-ttu-id="734a5-115">Sample Jupyter notebooks are included.</span><span class="sxs-lookup"><span data-stu-id="734a5-115">Sample Jupyter notebooks are included.</span></span>     |
| <span data-ttu-id="734a5-116">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-116">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-117">Keras</span><span class="sxs-lookup"><span data-stu-id="734a5-117">Keras</span></span>      |
| <span data-ttu-id="734a5-118">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-118">How to use / run it?</span></span>    | <span data-ttu-id="734a5-119">\* At a terminal: activate the correct environment, then run Python.</span><span class="sxs-lookup"><span data-stu-id="734a5-119">\* At a terminal: activate the correct environment, then run Python.</span></span> <br/>
 <span data-ttu-id="734a5-120">\* In Jupyter: Connect to [Jupyter](provision-vm.md#tools-installed-on-the-microsoft-data-science-virtual-machine) or [JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then open the CNTK directory for samples.</span><span class="sxs-lookup"><span data-stu-id="734a5-120">\* In Jupyter: Connect to [Jupyter](provision-vm.md#tools-installed-on-the-microsoft-data-science-virtual-machine) or [JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then open the CNTK directory for samples.</span></span> |

## <a name="tensorflow"></a><span data-ttu-id="734a5-121">TensorFlow</span><span class="sxs-lookup"><span data-stu-id="734a5-121">TensorFlow</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-122">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-122">What is it?</span></span>   | <span data-ttu-id="734a5-123">Deep learning framework</span><span class="sxs-lookup"><span data-stu-id="734a5-123">Deep learning framework</span></span>      |
| <span data-ttu-id="734a5-124">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-124">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-125">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="734a5-125">Windows, Linux</span></span>     |
| <span data-ttu-id="734a5-126">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-126">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-127">TensorFlow is installed in Python 3.5 on [Linux and Windows 2012](dsvm-languages.md#python-linux-and-windows-server-2012-edition) and Python 3.6 on [Windows 2016](dsvm-languages.md#python-windows-server-2016-edition).</span><span class="sxs-lookup"><span data-stu-id="734a5-127">TensorFlow is installed in Python 3.5 on [Linux and Windows 2012](dsvm-languages.md#python-linux-and-windows-server-2012-edition) and Python 3.6 on [Windows 2016](dsvm-languages.md#python-windows-server-2016-edition).</span></span>  |
| <span data-ttu-id="734a5-128">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-128">Links to Samples</span></span>      | <span data-ttu-id="734a5-129">Sample Jupyter notebooks are included.</span><span class="sxs-lookup"><span data-stu-id="734a5-129">Sample Jupyter notebooks are included.</span></span>     |
| <span data-ttu-id="734a5-130">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-130">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-131">Keras</span><span class="sxs-lookup"><span data-stu-id="734a5-131">Keras</span></span>      |
| <span data-ttu-id="734a5-132">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-132">How to use / run it?</span></span>    | <span data-ttu-id="734a5-133">\* At a terminal: activate the correct environment, then run Python.</span><span class="sxs-lookup"><span data-stu-id="734a5-133">\* At a terminal: activate the correct environment, then run Python.</span></span> <br/>
 <span data-ttu-id="734a5-134">\* In Jupyter: Connect to [Jupyter](provision-vm.md#tools-installed-on-the-microsoft-data-science-virtual-machine) or [JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then open the TensorFlow directory for samples.</span><span class="sxs-lookup"><span data-stu-id="734a5-134">\* In Jupyter: Connect to [Jupyter](provision-vm.md#tools-installed-on-the-microsoft-data-science-virtual-machine) or [JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then open the TensorFlow directory for samples.</span></span>  |

## <a name="horovod"></a><span data-ttu-id="734a5-135">Horovod</span><span class="sxs-lookup"><span data-stu-id="734a5-135">Horovod</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-136">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-136">What is it?</span></span>   | <span data-ttu-id="734a5-137">Distribued deep learning framework for TensorFlow</span><span class="sxs-lookup"><span data-stu-id="734a5-137">Distribued deep learning framework for TensorFlow</span></span>      |
| <span data-ttu-id="734a5-138">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-138">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-139">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="734a5-139">Ubuntu</span></span>     |
| <span data-ttu-id="734a5-140">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-140">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-141">Horovod is installed in Python 3.5 on [Ubuntu](dsvm-languages.md#python-linux-and-windows-server-2012-edition).</span><span class="sxs-lookup"><span data-stu-id="734a5-141">Horovod is installed in Python 3.5 on [Ubuntu](dsvm-languages.md#python-linux-and-windows-server-2012-edition).</span></span>  |
| <span data-ttu-id="734a5-142">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-142">Links to Samples</span></span>      | [https://github.com/uber/horovod/tree/master/examples](https://github.com/uber/horovod/tree/master/examples)     |
| <span data-ttu-id="734a5-143">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-143">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-144">TensorFlow</span><span class="sxs-lookup"><span data-stu-id="734a5-144">TensorFlow</span></span>      |
| <span data-ttu-id="734a5-145">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-145">How to use / run it?</span></span>    | <span data-ttu-id="734a5-146">At a terminal: activate the correct environment, then run Python.</span><span class="sxs-lookup"><span data-stu-id="734a5-146">At a terminal: activate the correct environment, then run Python.</span></span> |

## <a name="keras"></a><span data-ttu-id="734a5-147">Keras</span><span class="sxs-lookup"><span data-stu-id="734a5-147">Keras</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-148">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-148">What is it?</span></span>   | <span data-ttu-id="734a5-149">High-level deep learning API</span><span class="sxs-lookup"><span data-stu-id="734a5-149">High-level deep learning API</span></span>      |
| <span data-ttu-id="734a5-150">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-150">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-151">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="734a5-151">Windows, Linux</span></span>     |
| <span data-ttu-id="734a5-152">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-152">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-153">TensorFlow is installed in Python 3.5 on [Linux and Windows 2012](dsvm-languages.md#python-linux-and-windows-server-2012-edition) and Python 3.6 on [Windows 2016](dsvm-languages.md#python-windows-server-2016-edition).</span><span class="sxs-lookup"><span data-stu-id="734a5-153">TensorFlow is installed in Python 3.5 on [Linux and Windows 2012](dsvm-languages.md#python-linux-and-windows-server-2012-edition) and Python 3.6 on [Windows 2016](dsvm-languages.md#python-windows-server-2016-edition).</span></span> |
| <span data-ttu-id="734a5-154">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-154">Links to Samples</span></span>      | https://github.com/fchollet/keras/tree/master/examples      |
| <span data-ttu-id="734a5-155">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-155">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-156">Microsoft Cognitive Toolkit, TensorFlow, Theano</span><span class="sxs-lookup"><span data-stu-id="734a5-156">Microsoft Cognitive Toolkit, TensorFlow, Theano</span></span>      |
| <span data-ttu-id="734a5-157">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-157">How to use / run it?</span></span>    | <span data-ttu-id="734a5-158">\* At a terminal: activate the correct environment, then run Python.</span><span class="sxs-lookup"><span data-stu-id="734a5-158">\* At a terminal: activate the correct environment, then run Python.</span></span> <br/>
 <span data-ttu-id="734a5-159">\* In Jupyter: Download the samples from the Github location, connect to [Jupyter](provision-vm.md#tools-installed-on-the-microsoft-data-science-virtual-machine) or [JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then open the sample directory.</span><span class="sxs-lookup"><span data-stu-id="734a5-159">\* In Jupyter: Download the samples from the Github location, connect to [Jupyter](provision-vm.md#tools-installed-on-the-microsoft-data-science-virtual-machine) or [JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then open the sample directory.</span></span> |

## <a name="caffe"></a><span data-ttu-id="734a5-160">Caffe</span><span class="sxs-lookup"><span data-stu-id="734a5-160">Caffe</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-161">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-161">What is it?</span></span>   | <span data-ttu-id="734a5-162">Deep learning framework</span><span class="sxs-lookup"><span data-stu-id="734a5-162">Deep learning framework</span></span>      |
| <span data-ttu-id="734a5-163">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-163">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-164">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="734a5-164">Ubuntu</span></span>     |
| <span data-ttu-id="734a5-165">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-165">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-166">Caffe is installed in `/opt/caffe`.</span><span class="sxs-lookup"><span data-stu-id="734a5-166">Caffe is installed in `/opt/caffe`.</span></span>    |
| <span data-ttu-id="734a5-167">How to switch to Python 2.7</span><span class="sxs-lookup"><span data-stu-id="734a5-167">How to switch to Python 2.7</span></span> | <span data-ttu-id="734a5-168">Run `source activate root`</span><span class="sxs-lookup"><span data-stu-id="734a5-168">Run `source activate root`</span></span> |
| <span data-ttu-id="734a5-169">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-169">Links to Samples</span></span>      | <span data-ttu-id="734a5-170">Samples are included in `/opt/caffe/examples`.</span><span class="sxs-lookup"><span data-stu-id="734a5-170">Samples are included in `/opt/caffe/examples`.</span></span>      |
| <span data-ttu-id="734a5-171">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-171">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-172">Caffe2</span><span class="sxs-lookup"><span data-stu-id="734a5-172">Caffe2</span></span>      |
### <a name="how-to-use--run-it"></a><span data-ttu-id="734a5-173">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-173">How to use / run it?</span></span>  

<span data-ttu-id="734a5-174">Use X2Go to log in to your VM, then start a new terminal and enter</span><span class="sxs-lookup"><span data-stu-id="734a5-174">Use X2Go to log in to your VM, then start a new terminal and enter</span></span>

```
cd /opt/caffe/examples
source activate root
jupyter notebook
```

<span data-ttu-id="734a5-175">A new browser window opens with sample notebooks.</span><span class="sxs-lookup"><span data-stu-id="734a5-175">A new browser window opens with sample notebooks.</span></span>

<span data-ttu-id="734a5-176">Binaries are installed in /opt/caffe/build/install/bin.</span><span class="sxs-lookup"><span data-stu-id="734a5-176">Binaries are installed in /opt/caffe/build/install/bin.</span></span>

<span data-ttu-id="734a5-177">Installed version of Caffe requires Python 2.7 and won't work with Python 3.5 activated by default.</span><span class="sxs-lookup"><span data-stu-id="734a5-177">Installed version of Caffe requires Python 2.7 and won't work with Python 3.5 activated by default.</span></span> <span data-ttu-id="734a5-178">Run `source activate root` to switch Anaconda environment.</span><span class="sxs-lookup"><span data-stu-id="734a5-178">Run `source activate root` to switch Anaconda environment.</span></span> 

## <a name="caffe2"></a><span data-ttu-id="734a5-179">Caffe2</span><span class="sxs-lookup"><span data-stu-id="734a5-179">Caffe2</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-180">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-180">What is it?</span></span>   | <span data-ttu-id="734a5-181">Deep learning framework</span><span class="sxs-lookup"><span data-stu-id="734a5-181">Deep learning framework</span></span>      |
| <span data-ttu-id="734a5-182">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-182">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-183">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="734a5-183">Ubuntu</span></span>     |
| <span data-ttu-id="734a5-184">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-184">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-185">Caffe2 is installed in the [Python 2.7 (root) conda environment](dsvm-languages.md#python-linux-and-windows-server-2012-edition).</span><span class="sxs-lookup"><span data-stu-id="734a5-185">Caffe2 is installed in the [Python 2.7 (root) conda environment](dsvm-languages.md#python-linux-and-windows-server-2012-edition).</span></span> <span data-ttu-id="734a5-186">The source is in `/opt/caffe2`.</span><span class="sxs-lookup"><span data-stu-id="734a5-186">The source is in `/opt/caffe2`.</span></span> |
| <span data-ttu-id="734a5-187">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-187">Links to Samples</span></span>      | <span data-ttu-id="734a5-188">Sample notebooks are included in JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="734a5-188">Sample notebooks are included in JupyterHub.</span></span> |
| <span data-ttu-id="734a5-189">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-189">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-190">Caffe</span><span class="sxs-lookup"><span data-stu-id="734a5-190">Caffe</span></span>      |
| <span data-ttu-id="734a5-191">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-191">How to use / run it?</span></span>    | <span data-ttu-id="734a5-192">\* At the terminal: activate the [root Python environment](dsvm-languages.md#python-linux-and-windows-server-2012-edition), start Python, and import caffe2.</span><span class="sxs-lookup"><span data-stu-id="734a5-192">\* At the terminal: activate the [root Python environment](dsvm-languages.md#python-linux-and-windows-server-2012-edition), start Python, and import caffe2.</span></span> <br/> <span data-ttu-id="734a5-193">\* In JupyterHub: [connect to JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then navigate to the Caffe2 directory to find sample notebooks.</span><span class="sxs-lookup"><span data-stu-id="734a5-193">\* In JupyterHub: [connect to JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then navigate to the Caffe2 directory to find sample notebooks.</span></span> <span data-ttu-id="734a5-194">Some notebooks require the Caffe2 root to be set in the Python code; enter /opt/caffe2.</span><span class="sxs-lookup"><span data-stu-id="734a5-194">Some notebooks require the Caffe2 root to be set in the Python code; enter /opt/caffe2.</span></span> |
| <span data-ttu-id="734a5-195">Build notes</span><span class="sxs-lookup"><span data-stu-id="734a5-195">Build notes</span></span> | <span data-ttu-id="734a5-196">Caffe2 is built from source on Linux and includes CUDA, cuDNN, and Intel MKL.</span><span class="sxs-lookup"><span data-stu-id="734a5-196">Caffe2 is built from source on Linux and includes CUDA, cuDNN, and Intel MKL.</span></span> <span data-ttu-id="734a5-197">The current commit is 0d9c0d48c6f20143d6404b99cc568efd29d5a4be, which was chosen for stability on all GPUs and samples tested.</span><span class="sxs-lookup"><span data-stu-id="734a5-197">The current commit is 0d9c0d48c6f20143d6404b99cc568efd29d5a4be, which was chosen for stability on all GPUs and samples tested.</span></span> |

## <a name="chainer"></a><span data-ttu-id="734a5-198">Chainer</span><span class="sxs-lookup"><span data-stu-id="734a5-198">Chainer</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-199">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-199">What is it?</span></span>   | <span data-ttu-id="734a5-200">Deep learning framework</span><span class="sxs-lookup"><span data-stu-id="734a5-200">Deep learning framework</span></span>      |
| <span data-ttu-id="734a5-201">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-201">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-202">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="734a5-202">Windows, Linux</span></span>     |
| <span data-ttu-id="734a5-203">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-203">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-204">Chainer is installed in [Python 3.5](dsvm-languages.md#python-linux-and-windows-server-2012-edition).</span><span class="sxs-lookup"><span data-stu-id="734a5-204">Chainer is installed in [Python 3.5](dsvm-languages.md#python-linux-and-windows-server-2012-edition).</span></span> <span data-ttu-id="734a5-205">ChainerRL and ChainerCV are also installed.</span><span class="sxs-lookup"><span data-stu-id="734a5-205">ChainerRL and ChainerCV are also installed.</span></span>   |
| <span data-ttu-id="734a5-206">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-206">Links to Samples</span></span>      | <span data-ttu-id="734a5-207">Sample notebooks are included in JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="734a5-207">Sample notebooks are included in JupyterHub.</span></span> |
| <span data-ttu-id="734a5-208">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-208">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-209">Caffe</span><span class="sxs-lookup"><span data-stu-id="734a5-209">Caffe</span></span>      |
| <span data-ttu-id="734a5-210">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-210">How to use / run it?</span></span>  | <span data-ttu-id="734a5-211">\* At the terminal: activate the [Python 3.5](dsvm-languages.md#python-linux-and-windows-server-2012-edition) environment, run _python_, then import chainer.</span><span class="sxs-lookup"><span data-stu-id="734a5-211">\* At the terminal: activate the [Python 3.5](dsvm-languages.md#python-linux-and-windows-server-2012-edition) environment, run _python_, then import chainer.</span></span> <br/>
* <span data-ttu-id="734a5-212">In JupyterHub: [connect to JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then navigate to the Chainer directory to find sample notebooks.</span><span class="sxs-lookup"><span data-stu-id="734a5-212">In JupyterHub: [connect to JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then navigate to the Chainer directory to find sample notebooks.</span></span>


## <a name="deep-water"></a><span data-ttu-id="734a5-213">Deep Water</span><span class="sxs-lookup"><span data-stu-id="734a5-213">Deep Water</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-214">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-214">What is it?</span></span>   | <span data-ttu-id="734a5-215">Deep learning framework for H2O</span><span class="sxs-lookup"><span data-stu-id="734a5-215">Deep learning framework for H2O</span></span>      |
| <span data-ttu-id="734a5-216">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-216">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="734a5-217">Ubuntu</span></span>     |
| <span data-ttu-id="734a5-218">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-218">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-219">Deep Water is installed in [Python 3.5](dsvm-languages.md#python-linux-and-windows-server-2012-edition) and is also available in `/dsvm/tools/deep_water`.</span><span class="sxs-lookup"><span data-stu-id="734a5-219">Deep Water is installed in [Python 3.5](dsvm-languages.md#python-linux-and-windows-server-2012-edition) and is also available in `/dsvm/tools/deep_water`.</span></span>   |
| <span data-ttu-id="734a5-220">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-220">Links to Samples</span></span>      | <span data-ttu-id="734a5-221">Sample notebooks are included in JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="734a5-221">Sample notebooks are included in JupyterHub.</span></span>      |
| <span data-ttu-id="734a5-222">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-222">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-223">H2O, Sparkling Water</span><span class="sxs-lookup"><span data-stu-id="734a5-223">H2O, Sparkling Water</span></span>      |

### <a name="how-to-use--run-it"></a><span data-ttu-id="734a5-224">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-224">How to use / run it?</span></span>  

<span data-ttu-id="734a5-225">Deep Water requires CUDA 8 with cuDNN 5.1.</span><span class="sxs-lookup"><span data-stu-id="734a5-225">Deep Water requires CUDA 8 with cuDNN 5.1.</span></span> <span data-ttu-id="734a5-226">This is not in the library path by default, as other deep learning frameworks use CUDA 9 and cuDNN 7.</span><span class="sxs-lookup"><span data-stu-id="734a5-226">This is not in the library path by default, as other deep learning frameworks use CUDA 9 and cuDNN 7.</span></span> <span data-ttu-id="734a5-227">To use CUDA 8 + cuDNN 5.1 for Deep Water:</span><span class="sxs-lookup"><span data-stu-id="734a5-227">To use CUDA 8 + cuDNN 5.1 for Deep Water:</span></span>

```
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:${LD_LIBRARY_PATH}
export CUDA_ROOT=/usr/local/cuda-8.0
```

<span data-ttu-id="734a5-228">To use Deep Water:</span><span class="sxs-lookup"><span data-stu-id="734a5-228">To use Deep Water:</span></span>
* <span data-ttu-id="734a5-229">At the terminal: activate the [Python 3.5](dsvm-languages.md#python-linux-and-windows-server-2012-edition) environment, then run _python_.</span><span class="sxs-lookup"><span data-stu-id="734a5-229">At the terminal: activate the [Python 3.5](dsvm-languages.md#python-linux-and-windows-server-2012-edition) environment, then run _python_.</span></span> <br/>
* <span data-ttu-id="734a5-230">In JupyterHub: [connect to JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then navigate to the deep_water directory to find sample notebooks.</span><span class="sxs-lookup"><span data-stu-id="734a5-230">In JupyterHub: [connect to JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then navigate to the deep_water directory to find sample notebooks.</span></span>

## <a name="mxnet"></a><span data-ttu-id="734a5-231">MXNet</span><span class="sxs-lookup"><span data-stu-id="734a5-231">MXNet</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-232">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-232">What is it?</span></span>   | <span data-ttu-id="734a5-233">Deep learning framework</span><span class="sxs-lookup"><span data-stu-id="734a5-233">Deep learning framework</span></span>      |
| <span data-ttu-id="734a5-234">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-234">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-235">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="734a5-235">Windows, Linux</span></span>     |
| <span data-ttu-id="734a5-236">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-236">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-237">MXNet is installed in `C:\dsvm\tools\mxnet` on Windows and `/dsvm/tools/mxnet` on Linux.</span><span class="sxs-lookup"><span data-stu-id="734a5-237">MXNet is installed in `C:\dsvm\tools\mxnet` on Windows and `/dsvm/tools/mxnet` on Linux.</span></span> <span data-ttu-id="734a5-238">Python bindings are installed in Python 3.5 on [Linux and Windows 2012](dsvm-languages.md#python-linux-and-windows-server-2012-edition) and Python 3.6 on [Windows 2016](dsvm-languages.md#python-windows-server-2016-edition).</span><span class="sxs-lookup"><span data-stu-id="734a5-238">Python bindings are installed in Python 3.5 on [Linux and Windows 2012](dsvm-languages.md#python-linux-and-windows-server-2012-edition) and Python 3.6 on [Windows 2016](dsvm-languages.md#python-windows-server-2016-edition).</span></span> <span data-ttu-id="734a5-239">R bindings are also installed on Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="734a5-239">R bindings are also installed on Ubuntu.</span></span>   |
| <span data-ttu-id="734a5-240">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-240">Links to Samples</span></span>      | <span data-ttu-id="734a5-241">Sample Jupyter notebooks are included.</span><span class="sxs-lookup"><span data-stu-id="734a5-241">Sample Jupyter notebooks are included.</span></span>    |
| <span data-ttu-id="734a5-242">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-242">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-243">Keras</span><span class="sxs-lookup"><span data-stu-id="734a5-243">Keras</span></span>      |
| <span data-ttu-id="734a5-244">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-244">How to use / run it?</span></span>    | <span data-ttu-id="734a5-245">\* At a terminal: activate the correct environment, then run Python.</span><span class="sxs-lookup"><span data-stu-id="734a5-245">\* At a terminal: activate the correct environment, then run Python.</span></span> <br/>
 <span data-ttu-id="734a5-246">\* In Jupyter: Connect to [Jupyter](provision-vm.md#tools-installed-on-the-microsoft-data-science-virtual-machine) or [JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then open the mxnet directory for samples.</span><span class="sxs-lookup"><span data-stu-id="734a5-246">\* In Jupyter: Connect to [Jupyter](provision-vm.md#tools-installed-on-the-microsoft-data-science-virtual-machine) or [JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then open the mxnet directory for samples.</span></span>  |
 | <span data-ttu-id="734a5-247">Build notes</span><span class="sxs-lookup"><span data-stu-id="734a5-247">Build notes</span></span> | <span data-ttu-id="734a5-248">MXNet is built from source on Linux.</span><span class="sxs-lookup"><span data-stu-id="734a5-248">MXNet is built from source on Linux.</span></span> <span data-ttu-id="734a5-249">This build includes CUDA, cuDNN, NCCL, and MKL.</span><span class="sxs-lookup"><span data-stu-id="734a5-249">This build includes CUDA, cuDNN, NCCL, and MKL.</span></span> |

## <a name="nvidia-digits"></a><span data-ttu-id="734a5-250">NVIDIA DIGITS</span><span class="sxs-lookup"><span data-stu-id="734a5-250">NVIDIA DIGITS</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-251">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-251">What is it?</span></span>   | <span data-ttu-id="734a5-252">Deep learning system from NVIDIA for rapidly training deep learning models</span><span class="sxs-lookup"><span data-stu-id="734a5-252">Deep learning system from NVIDIA for rapidly training deep learning models</span></span>      |
| <span data-ttu-id="734a5-253">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-253">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-254">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="734a5-254">Ubuntu</span></span>     |
| <span data-ttu-id="734a5-255">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-255">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-256">DIGITS is installed in `/dsvm/tools/DIGITS` and is available a service called _digits_.</span><span class="sxs-lookup"><span data-stu-id="734a5-256">DIGITS is installed in `/dsvm/tools/DIGITS` and is available a service called _digits_.</span></span>   |
### <a name="how-to-use--run-it"></a><span data-ttu-id="734a5-257">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-257">How to use / run it?</span></span>  

<span data-ttu-id="734a5-258">Log in to the VM with X2Go.</span><span class="sxs-lookup"><span data-stu-id="734a5-258">Log in to the VM with X2Go.</span></span> <span data-ttu-id="734a5-259">At a terminal, start the service:</span><span class="sxs-lookup"><span data-stu-id="734a5-259">At a terminal, start the service:</span></span>

    sudo systemctl start digits

<span data-ttu-id="734a5-260">The service takes about one minute to start.</span><span class="sxs-lookup"><span data-stu-id="734a5-260">The service takes about one minute to start.</span></span> <span data-ttu-id="734a5-261">Start a web browser and navigate to `http://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="734a5-261">Start a web browser and navigate to `http://localhost:5000`.</span></span>



## <a name="nvidia-smi"></a><span data-ttu-id="734a5-262">nvidia-smi</span><span class="sxs-lookup"><span data-stu-id="734a5-262">nvidia-smi</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-263">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-263">What is it?</span></span>   | <span data-ttu-id="734a5-264">NVIDIA tool for querying GPU activity</span><span class="sxs-lookup"><span data-stu-id="734a5-264">NVIDIA tool for querying GPU activity</span></span>      |
| <span data-ttu-id="734a5-265">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-265">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-266">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="734a5-266">Windows, Linux</span></span>     |
| <span data-ttu-id="734a5-267">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-267">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-268">_nvidia-smi_ is available on the system path.</span><span class="sxs-lookup"><span data-stu-id="734a5-268">_nvidia-smi_ is available on the system path.</span></span>   |
| <span data-ttu-id="734a5-269">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-269">How to use / run it?</span></span> | <span data-ttu-id="734a5-270">Start a command prompt (on Windows) or a terminal (on Linux), then run _nvidia-smi_.</span><span class="sxs-lookup"><span data-stu-id="734a5-270">Start a command prompt (on Windows) or a terminal (on Linux), then run _nvidia-smi_.</span></span>



## <a name="theano"></a><span data-ttu-id="734a5-271">Theano</span><span class="sxs-lookup"><span data-stu-id="734a5-271">Theano</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-272">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-272">What is it?</span></span>   | <span data-ttu-id="734a5-273">Deep learning framework</span><span class="sxs-lookup"><span data-stu-id="734a5-273">Deep learning framework</span></span>      |
| <span data-ttu-id="734a5-274">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-274">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-275">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="734a5-275">Ubuntu</span></span>     |
| <span data-ttu-id="734a5-276">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-276">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-277">Theano is installed in Python 2.7 (_root_), as well as Python 3.5 (_py35_) environment.</span><span class="sxs-lookup"><span data-stu-id="734a5-277">Theano is installed in Python 2.7 (_root_), as well as Python 3.5 (_py35_) environment.</span></span>   |
| <span data-ttu-id="734a5-278">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-278">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-279">Keras</span><span class="sxs-lookup"><span data-stu-id="734a5-279">Keras</span></span>      |
| <span data-ttu-id="734a5-280">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="734a5-280">How to use / run it?</span></span>    | <span data-ttu-id="734a5-281">\* At a terminal, activate the Python version you want (root or py35), run python, then import theano.</span><span class="sxs-lookup"><span data-stu-id="734a5-281">\* At a terminal, activate the Python version you want (root or py35), run python, then import theano.</span></span> <br/> 
* <span data-ttu-id="734a5-282">In Jupyter, select the Python 2.7 or 3.5 kernel, then import theano.</span><span class="sxs-lookup"><span data-stu-id="734a5-282">In Jupyter, select the Python 2.7 or 3.5 kernel, then import theano.</span></span>  
<br/>
<span data-ttu-id="734a5-283">To work around a recent MKL bug, you need to first set the MKL threading layer:</span><span class="sxs-lookup"><span data-stu-id="734a5-283">To work around a recent MKL bug, you need to first set the MKL threading layer:</span></span><br/><br/>
<span data-ttu-id="734a5-284">_export MKL_THREADING_LAYER=GNU_
|</span><span class="sxs-lookup"><span data-stu-id="734a5-284">_export MKL_THREADING_LAYER=GNU_
|</span></span>



## <a name="torch"></a><span data-ttu-id="734a5-285">Torch</span><span class="sxs-lookup"><span data-stu-id="734a5-285">Torch</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-286">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-286">What is it?</span></span>   | <span data-ttu-id="734a5-287">Deep learning framework</span><span class="sxs-lookup"><span data-stu-id="734a5-287">Deep learning framework</span></span>      |
| <span data-ttu-id="734a5-288">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-288">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-289">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="734a5-289">Ubuntu</span></span>     |
| <span data-ttu-id="734a5-290">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-290">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-291">Torch is installed in `/dsvm/tools/torch`.</span><span class="sxs-lookup"><span data-stu-id="734a5-291">Torch is installed in `/dsvm/tools/torch`.</span></span> <span data-ttu-id="734a5-292">PyTorch is installed in Python 2.7 (_root_), as well as Python 3.5 (_py35_) environment.</span><span class="sxs-lookup"><span data-stu-id="734a5-292">PyTorch is installed in Python 2.7 (_root_), as well as Python 3.5 (_py35_) environment.</span></span>   |
| <span data-ttu-id="734a5-293">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-293">Links to Samples</span></span>      | <span data-ttu-id="734a5-294">Torch samples are located at `/dsvm/samples/torch`.</span><span class="sxs-lookup"><span data-stu-id="734a5-294">Torch samples are located at `/dsvm/samples/torch`.</span></span> <span data-ttu-id="734a5-295">PyTorch samples are located at `/dsvm/samples/pytorch`.</span><span class="sxs-lookup"><span data-stu-id="734a5-295">PyTorch samples are located at `/dsvm/samples/pytorch`.</span></span>      |


## <a name="pytorch"></a><span data-ttu-id="734a5-296">PyTorch</span><span class="sxs-lookup"><span data-stu-id="734a5-296">PyTorch</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-297">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-297">What is it?</span></span>   | <span data-ttu-id="734a5-298">Deep learning framework</span><span class="sxs-lookup"><span data-stu-id="734a5-298">Deep learning framework</span></span>      |
| <span data-ttu-id="734a5-299">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-299">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-300">Linux</span><span class="sxs-lookup"><span data-stu-id="734a5-300">Linux</span></span>     |
| <span data-ttu-id="734a5-301">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-301">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-302">PyTorch is installed in [Python 3.5](dsvm-languages.md#python-linux-and-windows-server-2012-edition).</span><span class="sxs-lookup"><span data-stu-id="734a5-302">PyTorch is installed in [Python 3.5](dsvm-languages.md#python-linux-and-windows-server-2012-edition).</span></span>  |
| <span data-ttu-id="734a5-303">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-303">Links to Samples</span></span>      | <span data-ttu-id="734a5-304">Sample Jupyter notebooks are included, and samples can also be found in /dsvm/samples/pytorch.</span><span class="sxs-lookup"><span data-stu-id="734a5-304">Sample Jupyter notebooks are included, and samples can also be found in /dsvm/samples/pytorch.</span></span>      |
| <span data-ttu-id="734a5-305">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-305">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-306">Torch</span><span class="sxs-lookup"><span data-stu-id="734a5-306">Torch</span></span>      |
| <span data-ttu-id="734a5-307">How to use / run it</span><span class="sxs-lookup"><span data-stu-id="734a5-307">How to use / run it</span></span> | 
* <span data-ttu-id="734a5-308">At a terminal: activate the correct environment, then run Python.</span><span class="sxs-lookup"><span data-stu-id="734a5-308">At a terminal: activate the correct environment, then run Python.</span></span> <br/>
 * <span data-ttu-id="734a5-309">In Jupyter: Connect to [JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then open the PyTorch directory for samples.</span><span class="sxs-lookup"><span data-stu-id="734a5-309">In Jupyter: Connect to [JupyterHub](dsvm-ubuntu-intro.md#how-to-access-the-data-science-virtual-machine-for-linux), then open the PyTorch directory for samples.</span></span>  |

## <a name="mxnet-model-server"></a><span data-ttu-id="734a5-310">MXNet Model Server</span><span class="sxs-lookup"><span data-stu-id="734a5-310">MXNet Model Server</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-311">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-311">What is it?</span></span>   | <span data-ttu-id="734a5-312">A server to create HTTP endpoints for MXNet and ONNX models</span><span class="sxs-lookup"><span data-stu-id="734a5-312">A server to create HTTP endpoints for MXNet and ONNX models</span></span>      |
| <span data-ttu-id="734a5-313">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-313">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-314">Linux</span><span class="sxs-lookup"><span data-stu-id="734a5-314">Linux</span></span>     |
| <span data-ttu-id="734a5-315">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-315">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-316">_mxnet-model-server_ is available on at the terminal.</span><span class="sxs-lookup"><span data-stu-id="734a5-316">_mxnet-model-server_ is available on at the terminal.</span></span>   |
| <span data-ttu-id="734a5-317">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-317">Links to Samples</span></span>      | <span data-ttu-id="734a5-318">Look for up-to-date samples on the [MXNet Model Server page](https://github.com/awslabs/mxnet-model-server).</span><span class="sxs-lookup"><span data-stu-id="734a5-318">Look for up-to-date samples on the [MXNet Model Server page](https://github.com/awslabs/mxnet-model-server).</span></span>    |
| <span data-ttu-id="734a5-319">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-319">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-320">MXNet</span><span class="sxs-lookup"><span data-stu-id="734a5-320">MXNet</span></span>      |

## <a name="tensorflow-serving"></a><span data-ttu-id="734a5-321">TensorFlow Serving</span><span class="sxs-lookup"><span data-stu-id="734a5-321">TensorFlow Serving</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-322">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-322">What is it?</span></span>   | <span data-ttu-id="734a5-323">A server to run inferencing on a TensorFlow model</span><span class="sxs-lookup"><span data-stu-id="734a5-323">A server to run inferencing on a TensorFlow model</span></span>      |
| <span data-ttu-id="734a5-324">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-324">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-325">Linux</span><span class="sxs-lookup"><span data-stu-id="734a5-325">Linux</span></span>     |
| <span data-ttu-id="734a5-326">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-326">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-327">_tensorflow_model_server_ is available at the terminal.</span><span class="sxs-lookup"><span data-stu-id="734a5-327">_tensorflow_model_server_ is available at the terminal.</span></span>   |
| <span data-ttu-id="734a5-328">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-328">Links to Samples</span></span>      | <span data-ttu-id="734a5-329">Samples are available [online](https://www.tensorflow.org/serving/).</span><span class="sxs-lookup"><span data-stu-id="734a5-329">Samples are available [online](https://www.tensorflow.org/serving/).</span></span>      |
| <span data-ttu-id="734a5-330">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-330">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-331">TensorFlow</span><span class="sxs-lookup"><span data-stu-id="734a5-331">TensorFlow</span></span>      |

## <a name="tensorrt"></a><span data-ttu-id="734a5-332">TensorRT</span><span class="sxs-lookup"><span data-stu-id="734a5-332">TensorRT</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="734a5-333">What is it?</span><span class="sxs-lookup"><span data-stu-id="734a5-333">What is it?</span></span>   | <span data-ttu-id="734a5-334">A deep learning inference server from NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="734a5-334">A deep learning inference server from NVIDIA.</span></span> |
| <span data-ttu-id="734a5-335">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="734a5-335">Supported DSVM Editions</span></span>      | <span data-ttu-id="734a5-336">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="734a5-336">Ubuntu</span></span>     |
| <span data-ttu-id="734a5-337">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="734a5-337">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="734a5-338">TensorRT is installed as an _apt_ package.</span><span class="sxs-lookup"><span data-stu-id="734a5-338">TensorRT is installed as an _apt_ package.</span></span>   |
| <span data-ttu-id="734a5-339">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="734a5-339">Links to Samples</span></span>      | <span data-ttu-id="734a5-340">Samples are available [online](https://docs.nvidia.com/deeplearning/sdk/tensorrt-developer-guide/index.html#samples).</span><span class="sxs-lookup"><span data-stu-id="734a5-340">Samples are available [online](https://docs.nvidia.com/deeplearning/sdk/tensorrt-developer-guide/index.html#samples).</span></span>      |
| <span data-ttu-id="734a5-341">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="734a5-341">Related Tools on the DSVM</span></span>      | <span data-ttu-id="734a5-342">TensorFlow Serving, MXNet Model Server</span><span class="sxs-lookup"><span data-stu-id="734a5-342">TensorFlow Serving, MXNet Model Server</span></span>  |



