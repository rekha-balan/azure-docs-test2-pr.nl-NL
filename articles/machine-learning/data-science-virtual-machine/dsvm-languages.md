---
title: Languages for the Data Science Virtual Machine on Azure | Microsoft Docs
description: Languages for the Data Science Virtual Machine on Azure
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
ms.openlocfilehash: 411729155f5135c7e45588b69995274c9cac1315
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865694"
---
# <a name="languages-supported-on-the-data-science-virtual-machine"></a><span data-ttu-id="521d5-104">Languages supported on the Data Science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="521d5-104">Languages supported on the Data Science Virtual Machine</span></span> 

<span data-ttu-id="521d5-105">The Data Science Virtual Machine (DSVM) comes with several pre-built languages and development tools for building your AI applications.</span><span class="sxs-lookup"><span data-stu-id="521d5-105">The Data Science Virtual Machine (DSVM) comes with several pre-built languages and development tools for building your AI applications.</span></span> <span data-ttu-id="521d5-106">Here are some of the salient ones.</span><span class="sxs-lookup"><span data-stu-id="521d5-106">Here are some of the salient ones.</span></span> 

## <a name="python-windows-server-2016-edition"></a><span data-ttu-id="521d5-107">Python (Windows Server 2016 Edition)</span><span class="sxs-lookup"><span data-stu-id="521d5-107">Python (Windows Server 2016 Edition)</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="521d5-108">Language versions Supported</span><span class="sxs-lookup"><span data-stu-id="521d5-108">Language versions Supported</span></span> | <span data-ttu-id="521d5-109">2.7 and 3.6</span><span class="sxs-lookup"><span data-stu-id="521d5-109">2.7 and 3.6</span></span> |
| <span data-ttu-id="521d5-110">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="521d5-110">Supported DSVM Editions</span></span>      | <span data-ttu-id="521d5-111">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="521d5-111">Windows Server 2016</span></span>     |
| <span data-ttu-id="521d5-112">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="521d5-112">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="521d5-113">Two global `conda` environments are created.</span><span class="sxs-lookup"><span data-stu-id="521d5-113">Two global `conda` environments are created.</span></span> <br /> <span data-ttu-id="521d5-114">\* `root` environment located at `/anaconda/` is Python 3.6 .</span><span class="sxs-lookup"><span data-stu-id="521d5-114">\* `root` environment located at `/anaconda/` is Python 3.6 .</span></span> <br/> <span data-ttu-id="521d5-115">\* `python2` environment located at `/anaconda/envs/python2`is Python 2.7</span><span class="sxs-lookup"><span data-stu-id="521d5-115">\* `python2` environment located at `/anaconda/envs/python2`is Python 2.7</span></span>       |
| <span data-ttu-id="521d5-116">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="521d5-116">Links to Samples</span></span>      | <span data-ttu-id="521d5-117">Sample Jupyter notebooks for Python are included</span><span class="sxs-lookup"><span data-stu-id="521d5-117">Sample Jupyter notebooks for Python are included</span></span>     |
| <span data-ttu-id="521d5-118">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="521d5-118">Related Tools on the DSVM</span></span>      | <span data-ttu-id="521d5-119">PySpark, R, Julia</span><span class="sxs-lookup"><span data-stu-id="521d5-119">PySpark, R, Julia</span></span>      |

> [!NOTE]
> <span data-ttu-id="521d5-120">Windows Server 2016 created before March 2018 contains Python 3.5 and Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="521d5-120">Windows Server 2016 created before March 2018 contains Python 3.5 and Python 2.7.</span></span> <span data-ttu-id="521d5-121">Also Python 2.7 is the conda **root** environment and **py35** is the Python 3.5 environment.</span><span class="sxs-lookup"><span data-stu-id="521d5-121">Also Python 2.7 is the conda **root** environment and **py35** is the Python 3.5 environment.</span></span> 

### <a name="how-to-use--run-it"></a><span data-ttu-id="521d5-122">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="521d5-122">How to use / run it?</span></span>    

* <span data-ttu-id="521d5-123">Running in command prompt</span><span class="sxs-lookup"><span data-stu-id="521d5-123">Running in command prompt</span></span>

<span data-ttu-id="521d5-124">Open command prompt and do the following depending on the version of Python you want to run.</span><span class="sxs-lookup"><span data-stu-id="521d5-124">Open command prompt and do the following depending on the version of Python you want to run.</span></span> 

```
# To run Python 2.7
activate python2
python --version

# To run Python 3.6
activate 
python --version

```
* <span data-ttu-id="521d5-125">Using in an IDE</span><span class="sxs-lookup"><span data-stu-id="521d5-125">Using in an IDE</span></span>

<span data-ttu-id="521d5-126">Use Python Tools for Visual Studio (PTVS) installed in the Visual Studio Community edition.</span><span class="sxs-lookup"><span data-stu-id="521d5-126">Use Python Tools for Visual Studio (PTVS) installed in the Visual Studio Community edition.</span></span> <span data-ttu-id="521d5-127">The only environment setup automatically in PTVS by default is Python 3.6.</span><span class="sxs-lookup"><span data-stu-id="521d5-127">The only environment setup automatically in PTVS by default is Python 3.6.</span></span> 

> [!NOTE]
> <span data-ttu-id="521d5-128">To point the PTVS at Python 2.7, you need to create a  custom environment in PTVS.</span><span class="sxs-lookup"><span data-stu-id="521d5-128">To point the PTVS at Python 2.7, you need to create a  custom environment in PTVS.</span></span> <span data-ttu-id="521d5-129">To set this environment paths in the Visual Studio  Community Edition, navigate to **Tools** -> **Python Tools** -> **Python Environments** and then click **+ Custom**.</span><span class="sxs-lookup"><span data-stu-id="521d5-129">To set this environment paths in the Visual Studio  Community Edition, navigate to **Tools** -> **Python Tools** -> **Python Environments** and then click **+ Custom**.</span></span> <span data-ttu-id="521d5-130">Then set the location to `c:\anaconda\envs\python2` and then click _Auto Detect_.</span><span class="sxs-lookup"><span data-stu-id="521d5-130">Then set the location to `c:\anaconda\envs\python2` and then click _Auto Detect_.</span></span> 

* <span data-ttu-id="521d5-131">Using in Jupyter</span><span class="sxs-lookup"><span data-stu-id="521d5-131">Using in Jupyter</span></span>

<span data-ttu-id="521d5-132">Open Jupyter and click on the `New` button to create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="521d5-132">Open Jupyter and click on the `New` button to create a new notebook.</span></span> <span data-ttu-id="521d5-133">At this point, you can choose the kernel type as _Python [Conda Root]_ for Python 3.6 and _Python [Conda env:python2]_ for Python 2.7 environment.</span><span class="sxs-lookup"><span data-stu-id="521d5-133">At this point, you can choose the kernel type as _Python [Conda Root]_ for Python 3.6 and _Python [Conda env:python2]_ for Python 2.7 environment.</span></span> 

* <span data-ttu-id="521d5-134">Installing Python packages</span><span class="sxs-lookup"><span data-stu-id="521d5-134">Installing Python packages</span></span>

<span data-ttu-id="521d5-135">The default Python environments on the DSVM are global environment readable by all users.</span><span class="sxs-lookup"><span data-stu-id="521d5-135">The default Python environments on the DSVM are global environment readable by all users.</span></span> <span data-ttu-id="521d5-136">But only administrators can write / install global packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-136">But only administrators can write / install global packages.</span></span> <span data-ttu-id="521d5-137">In order to install package to the global environment, activate to the root or python2 environment using the `activate` command as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="521d5-137">In order to install package to the global environment, activate to the root or python2 environment using the `activate` command as an Administrator.</span></span> <span data-ttu-id="521d5-138">Then you can use the package manager like `conda` or `pip` to install or update packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-138">Then you can use the package manager like `conda` or `pip` to install or update packages.</span></span> 

## <a name="python-linux-and-windows-server-2012-edition"></a><span data-ttu-id="521d5-139">Python (Linux and Windows Server 2012 Edition)</span><span class="sxs-lookup"><span data-stu-id="521d5-139">Python (Linux and Windows Server 2012 Edition)</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="521d5-140">Language versions Supported</span><span class="sxs-lookup"><span data-stu-id="521d5-140">Language versions Supported</span></span> | <span data-ttu-id="521d5-141">2.7 and 3.5</span><span class="sxs-lookup"><span data-stu-id="521d5-141">2.7 and 3.5</span></span> |
| <span data-ttu-id="521d5-142">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="521d5-142">Supported DSVM Editions</span></span>      | <span data-ttu-id="521d5-143">Linux, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="521d5-143">Linux, Windows Server 2012</span></span>    |
| <span data-ttu-id="521d5-144">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="521d5-144">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="521d5-145">Two global `conda` environments are created.</span><span class="sxs-lookup"><span data-stu-id="521d5-145">Two global `conda` environments are created.</span></span> <br /> <span data-ttu-id="521d5-146">\* `root` environment located at `/anaconda/` is Python 2.7 .</span><span class="sxs-lookup"><span data-stu-id="521d5-146">\* `root` environment located at `/anaconda/` is Python 2.7 .</span></span> <br/> <span data-ttu-id="521d5-147">\* `py35` environment located at `/anaconda/envs/py35`is Python 3.5</span><span class="sxs-lookup"><span data-stu-id="521d5-147">\* `py35` environment located at `/anaconda/envs/py35`is Python 3.5</span></span>       |
| <span data-ttu-id="521d5-148">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="521d5-148">Links to Samples</span></span>      | <span data-ttu-id="521d5-149">Sample Jupyter notebooks for Python are included</span><span class="sxs-lookup"><span data-stu-id="521d5-149">Sample Jupyter notebooks for Python are included</span></span>     |
| <span data-ttu-id="521d5-150">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="521d5-150">Related Tools on the DSVM</span></span>      | <span data-ttu-id="521d5-151">PySpark, R, Julia</span><span class="sxs-lookup"><span data-stu-id="521d5-151">PySpark, R, Julia</span></span>      |
### <a name="how-to-use--run-it"></a><span data-ttu-id="521d5-152">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="521d5-152">How to use / run it?</span></span>    

<span data-ttu-id="521d5-153">**Linux**</span><span class="sxs-lookup"><span data-stu-id="521d5-153">**Linux**</span></span>
* <span data-ttu-id="521d5-154">Running in terminal</span><span class="sxs-lookup"><span data-stu-id="521d5-154">Running in terminal</span></span>

<span data-ttu-id="521d5-155">Open terminal and do the following depending on the version of Python you want to run.</span><span class="sxs-lookup"><span data-stu-id="521d5-155">Open terminal and do the following depending on the version of Python you want to run.</span></span> 

```
# To run Python 2.7
source activate 
python --version

# To run Python 3.5
source activate py35
python --version

```
* <span data-ttu-id="521d5-156">Using in an IDE</span><span class="sxs-lookup"><span data-stu-id="521d5-156">Using in an IDE</span></span>

<span data-ttu-id="521d5-157">Use PyCharm installed in the Visual Studio Community edition.</span><span class="sxs-lookup"><span data-stu-id="521d5-157">Use PyCharm installed in the Visual Studio Community edition.</span></span> 

* <span data-ttu-id="521d5-158">Using in Jupyter</span><span class="sxs-lookup"><span data-stu-id="521d5-158">Using in Jupyter</span></span>

<span data-ttu-id="521d5-159">Open Jupyter and click on the `New` button to create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="521d5-159">Open Jupyter and click on the `New` button to create a new notebook.</span></span> <span data-ttu-id="521d5-160">At this point, you can choose the kernel type as _Python [Conda Root]_ for Python 2.7 and _Python [Conda env:py35]_ for Python 3.5 environment.</span><span class="sxs-lookup"><span data-stu-id="521d5-160">At this point, you can choose the kernel type as _Python [Conda Root]_ for Python 2.7 and _Python [Conda env:py35]_ for Python 3.5 environment.</span></span> 

* <span data-ttu-id="521d5-161">Installing Python packages</span><span class="sxs-lookup"><span data-stu-id="521d5-161">Installing Python packages</span></span>

<span data-ttu-id="521d5-162">The default Python environments on the DSVM are global environments readable by all users.</span><span class="sxs-lookup"><span data-stu-id="521d5-162">The default Python environments on the DSVM are global environments readable by all users.</span></span> <span data-ttu-id="521d5-163">But only administrators can write / install global packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-163">But only administrators can write / install global packages.</span></span> <span data-ttu-id="521d5-164">In order to install package to the global environment, activate to the root or py35 environment using the `source activate` command as an Administrator or a user with sudo permission.</span><span class="sxs-lookup"><span data-stu-id="521d5-164">In order to install package to the global environment, activate to the root or py35 environment using the `source activate` command as an Administrator or a user with sudo permission.</span></span> <span data-ttu-id="521d5-165">Then you can use a package manager like `conda` or `pip` to install or update packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-165">Then you can use a package manager like `conda` or `pip` to install or update packages.</span></span> 

<span data-ttu-id="521d5-166">**Windows 2012**</span><span class="sxs-lookup"><span data-stu-id="521d5-166">**Windows 2012**</span></span>
* <span data-ttu-id="521d5-167">Running in command prompt</span><span class="sxs-lookup"><span data-stu-id="521d5-167">Running in command prompt</span></span>

<span data-ttu-id="521d5-168">Open command prompt and do the following depending on the version of Python you want to run.</span><span class="sxs-lookup"><span data-stu-id="521d5-168">Open command prompt and do the following depending on the version of Python you want to run.</span></span> 

```
# To run Python 2.7
activate 
python --version

# To run Python 3.5
activate py35
python --version

```
* <span data-ttu-id="521d5-169">Using in an IDE</span><span class="sxs-lookup"><span data-stu-id="521d5-169">Using in an IDE</span></span>

<span data-ttu-id="521d5-170">Use Python Tools for Visual Studio (PTVS) installed in the Visual Studio Community edition.</span><span class="sxs-lookup"><span data-stu-id="521d5-170">Use Python Tools for Visual Studio (PTVS) installed in the Visual Studio Community edition.</span></span> <span data-ttu-id="521d5-171">The only environment setup automatically in PTVS in Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="521d5-171">The only environment setup automatically in PTVS in Python 2.7.</span></span> 
> [!NOTE]
> <span data-ttu-id="521d5-172">To point the PTVS at Python 3.5, you need to create a  custom environment in PTVS.</span><span class="sxs-lookup"><span data-stu-id="521d5-172">To point the PTVS at Python 3.5, you need to create a  custom environment in PTVS.</span></span> <span data-ttu-id="521d5-173">To set this environment paths in the Visual Studio  Community Edition, navigate to **Tools** -> **Python Tools** -> **Python Environments** and then click **+ Custom**.</span><span class="sxs-lookup"><span data-stu-id="521d5-173">To set this environment paths in the Visual Studio  Community Edition, navigate to **Tools** -> **Python Tools** -> **Python Environments** and then click **+ Custom**.</span></span> <span data-ttu-id="521d5-174">Then set the location to `c:\anaconda\envs\py35` and then click _Auto Detect_.</span><span class="sxs-lookup"><span data-stu-id="521d5-174">Then set the location to `c:\anaconda\envs\py35` and then click _Auto Detect_.</span></span> 

* <span data-ttu-id="521d5-175">Using in Jupyter</span><span class="sxs-lookup"><span data-stu-id="521d5-175">Using in Jupyter</span></span>

<span data-ttu-id="521d5-176">Open Jupyter and click on the `New` button to create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="521d5-176">Open Jupyter and click on the `New` button to create a new notebook.</span></span> <span data-ttu-id="521d5-177">At this point, you can choose the kernel type as _Python [Conda Root]_ for Python 2.7 and _Python [Conda env:py35]_ for Python 3.5 environment.</span><span class="sxs-lookup"><span data-stu-id="521d5-177">At this point, you can choose the kernel type as _Python [Conda Root]_ for Python 2.7 and _Python [Conda env:py35]_ for Python 3.5 environment.</span></span> 

* <span data-ttu-id="521d5-178">Installing Python packages</span><span class="sxs-lookup"><span data-stu-id="521d5-178">Installing Python packages</span></span>

<span data-ttu-id="521d5-179">The default Python environments on the DSVM are global environment readable by all users.</span><span class="sxs-lookup"><span data-stu-id="521d5-179">The default Python environments on the DSVM are global environment readable by all users.</span></span> <span data-ttu-id="521d5-180">But only administrators can write / install global packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-180">But only administrators can write / install global packages.</span></span> <span data-ttu-id="521d5-181">In order to install package to the global environment, activate to the root or py35 environment using the `activate` command as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="521d5-181">In order to install package to the global environment, activate to the root or py35 environment using the `activate` command as an Administrator.</span></span> <span data-ttu-id="521d5-182">Then you can use the package manager like `conda` or `pip` to install or update packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-182">Then you can use the package manager like `conda` or `pip` to install or update packages.</span></span> 

## <a name="r"></a><span data-ttu-id="521d5-183">R</span><span class="sxs-lookup"><span data-stu-id="521d5-183">R</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="521d5-184">Language versions Supported</span><span class="sxs-lookup"><span data-stu-id="521d5-184">Language versions Supported</span></span> | <span data-ttu-id="521d5-185">Microsoft R Open 3.x (100% compatible with CRAN-R</span><span class="sxs-lookup"><span data-stu-id="521d5-185">Microsoft R Open 3.x (100% compatible with CRAN-R</span></span><br /> <span data-ttu-id="521d5-186">Microsoft R Server 9.x Developer edition (A Scalable Enterprise ready R platform)</span><span class="sxs-lookup"><span data-stu-id="521d5-186">Microsoft R Server 9.x Developer edition (A Scalable Enterprise ready R platform)</span></span>|
| <span data-ttu-id="521d5-187">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="521d5-187">Supported DSVM Editions</span></span>      | <span data-ttu-id="521d5-188">Linux, Windows</span><span class="sxs-lookup"><span data-stu-id="521d5-188">Linux, Windows</span></span>     |
| <span data-ttu-id="521d5-189">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="521d5-189">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="521d5-190">Windows: `C:\Program Files\Microsoft\ML Server\R_SERVER`</span><span class="sxs-lookup"><span data-stu-id="521d5-190">Windows: `C:\Program Files\Microsoft\ML Server\R_SERVER`</span></span> <br /><span data-ttu-id="521d5-191">Linux: ` /usr/lib64/microsoft-r/3.3/lib64/R`</span><span class="sxs-lookup"><span data-stu-id="521d5-191">Linux: ` /usr/lib64/microsoft-r/3.3/lib64/R`</span></span>    |
| <span data-ttu-id="521d5-192">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="521d5-192">Links to Samples</span></span>      | <span data-ttu-id="521d5-193">Sample Jupyter notebooks for R are included</span><span class="sxs-lookup"><span data-stu-id="521d5-193">Sample Jupyter notebooks for R are included</span></span>     |
| <span data-ttu-id="521d5-194">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="521d5-194">Related Tools on the DSVM</span></span>      | <span data-ttu-id="521d5-195">SparkR, Python, Julia</span><span class="sxs-lookup"><span data-stu-id="521d5-195">SparkR, Python, Julia</span></span>      |
### <a name="how-to-use--run-it"></a><span data-ttu-id="521d5-196">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="521d5-196">How to use / run it?</span></span>    

<span data-ttu-id="521d5-197">**Windows**:</span><span class="sxs-lookup"><span data-stu-id="521d5-197">**Windows**:</span></span>

* <span data-ttu-id="521d5-198">Running in command prompt</span><span class="sxs-lookup"><span data-stu-id="521d5-198">Running in command prompt</span></span>

<span data-ttu-id="521d5-199">Open command prompt and just type `R`.</span><span class="sxs-lookup"><span data-stu-id="521d5-199">Open command prompt and just type `R`.</span></span>

* <span data-ttu-id="521d5-200">Using in an IDE</span><span class="sxs-lookup"><span data-stu-id="521d5-200">Using in an IDE</span></span>

<span data-ttu-id="521d5-201">Use RTools for Visual Studio (RTVS) installed in the Visual Studio Community edition or RStudio.</span><span class="sxs-lookup"><span data-stu-id="521d5-201">Use RTools for Visual Studio (RTVS) installed in the Visual Studio Community edition or RStudio.</span></span> <span data-ttu-id="521d5-202">These are available on the start menu or as a desktop icon.</span><span class="sxs-lookup"><span data-stu-id="521d5-202">These are available on the start menu or as a desktop icon.</span></span> 

* <span data-ttu-id="521d5-203">Using in Jupyter</span><span class="sxs-lookup"><span data-stu-id="521d5-203">Using in Jupyter</span></span>

<span data-ttu-id="521d5-204">Open Jupyter and click on the `New` button to create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="521d5-204">Open Jupyter and click on the `New` button to create a new notebook.</span></span> <span data-ttu-id="521d5-205">At this point, you can choose the kernel type as _R_ to use Jupyter R kernel (IRKernel).</span><span class="sxs-lookup"><span data-stu-id="521d5-205">At this point, you can choose the kernel type as _R_ to use Jupyter R kernel (IRKernel).</span></span> 

* <span data-ttu-id="521d5-206">Installing R packages</span><span class="sxs-lookup"><span data-stu-id="521d5-206">Installing R packages</span></span>

<span data-ttu-id="521d5-207">R is installed on the DSVM in a  global environment readable by all users.</span><span class="sxs-lookup"><span data-stu-id="521d5-207">R is installed on the DSVM in a  global environment readable by all users.</span></span> <span data-ttu-id="521d5-208">But only administrators can write / install global packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-208">But only administrators can write / install global packages.</span></span> <span data-ttu-id="521d5-209">In order to install package to the global environment, run R using one of the methods above.</span><span class="sxs-lookup"><span data-stu-id="521d5-209">In order to install package to the global environment, run R using one of the methods above.</span></span> <span data-ttu-id="521d5-210">Then you can run the R package manager `install.packages()` to install or update packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-210">Then you can run the R package manager `install.packages()` to install or update packages.</span></span> 

<span data-ttu-id="521d5-211">**Linux**:</span><span class="sxs-lookup"><span data-stu-id="521d5-211">**Linux**:</span></span>

* <span data-ttu-id="521d5-212">Running in terminal</span><span class="sxs-lookup"><span data-stu-id="521d5-212">Running in terminal</span></span>

<span data-ttu-id="521d5-213">Open terminal and just run `R`.</span><span class="sxs-lookup"><span data-stu-id="521d5-213">Open terminal and just run `R`.</span></span>  

* <span data-ttu-id="521d5-214">Using in an IDE</span><span class="sxs-lookup"><span data-stu-id="521d5-214">Using in an IDE</span></span>

<span data-ttu-id="521d5-215">Use RStudio installed on the Linux DSVM.</span><span class="sxs-lookup"><span data-stu-id="521d5-215">Use RStudio installed on the Linux DSVM.</span></span>  

* <span data-ttu-id="521d5-216">Using in Jupyter</span><span class="sxs-lookup"><span data-stu-id="521d5-216">Using in Jupyter</span></span>

<span data-ttu-id="521d5-217">Open Jupyter and click on the `New` button to create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="521d5-217">Open Jupyter and click on the `New` button to create a new notebook.</span></span> <span data-ttu-id="521d5-218">At this point, you can choose the kernel type as _R_ to use Jupyter R kernel (IRKernel).</span><span class="sxs-lookup"><span data-stu-id="521d5-218">At this point, you can choose the kernel type as _R_ to use Jupyter R kernel (IRKernel).</span></span> 

* <span data-ttu-id="521d5-219">Installing R packages</span><span class="sxs-lookup"><span data-stu-id="521d5-219">Installing R packages</span></span>

<span data-ttu-id="521d5-220">R is installed on the DSVM in a  global environment readable by all users.</span><span class="sxs-lookup"><span data-stu-id="521d5-220">R is installed on the DSVM in a  global environment readable by all users.</span></span> <span data-ttu-id="521d5-221">But only administrators can write / install global packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-221">But only administrators can write / install global packages.</span></span> <span data-ttu-id="521d5-222">In order to install package to the global environment, run R using one of the methods above.</span><span class="sxs-lookup"><span data-stu-id="521d5-222">In order to install package to the global environment, run R using one of the methods above.</span></span> <span data-ttu-id="521d5-223">Then you can run the R package manager `install.packages()` to install or update packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-223">Then you can run the R package manager `install.packages()` to install or update packages.</span></span> 


## <a name="julia"></a><span data-ttu-id="521d5-224">Julia</span><span class="sxs-lookup"><span data-stu-id="521d5-224">Julia</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="521d5-225">Language versions Supported</span><span class="sxs-lookup"><span data-stu-id="521d5-225">Language versions Supported</span></span> | <span data-ttu-id="521d5-226">0.6</span><span class="sxs-lookup"><span data-stu-id="521d5-226">0.6</span></span> |
| <span data-ttu-id="521d5-227">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="521d5-227">Supported DSVM Editions</span></span>      | <span data-ttu-id="521d5-228">Linux, Windows</span><span class="sxs-lookup"><span data-stu-id="521d5-228">Linux, Windows</span></span>     |
| <span data-ttu-id="521d5-229">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="521d5-229">How is it configured / installed on the DSVM?</span></span>  | <span data-ttu-id="521d5-230">Windows: Installed at `C:\JuliaPro-VERSION`</span><span class="sxs-lookup"><span data-stu-id="521d5-230">Windows: Installed at `C:\JuliaPro-VERSION`</span></span><br /> <span data-ttu-id="521d5-231">Linux: Installed at `/opt/JuliaPro-VERSION`</span><span class="sxs-lookup"><span data-stu-id="521d5-231">Linux: Installed at `/opt/JuliaPro-VERSION`</span></span>    |
| <span data-ttu-id="521d5-232">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="521d5-232">Links to Samples</span></span>      | <span data-ttu-id="521d5-233">Sample Jupyter notebooks for Julia are included</span><span class="sxs-lookup"><span data-stu-id="521d5-233">Sample Jupyter notebooks for Julia are included</span></span>     |
| <span data-ttu-id="521d5-234">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="521d5-234">Related Tools on the DSVM</span></span>      | <span data-ttu-id="521d5-235">Python, R</span><span class="sxs-lookup"><span data-stu-id="521d5-235">Python, R</span></span>      |
### <a name="how-to-use--run-it"></a><span data-ttu-id="521d5-236">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="521d5-236">How to use / run it?</span></span>    

<span data-ttu-id="521d5-237">**Windows**:</span><span class="sxs-lookup"><span data-stu-id="521d5-237">**Windows**:</span></span>

* <span data-ttu-id="521d5-238">Running in command prompt</span><span class="sxs-lookup"><span data-stu-id="521d5-238">Running in command prompt</span></span>

<span data-ttu-id="521d5-239">Open command prompt and just run `julia`.</span><span class="sxs-lookup"><span data-stu-id="521d5-239">Open command prompt and just run `julia`.</span></span> 
* <span data-ttu-id="521d5-240">Using in an IDE</span><span class="sxs-lookup"><span data-stu-id="521d5-240">Using in an IDE</span></span>

<span data-ttu-id="521d5-241">Use `Juno` the Julia IDE installed on the DSVM and available as a desktop shortcut.</span><span class="sxs-lookup"><span data-stu-id="521d5-241">Use `Juno` the Julia IDE installed on the DSVM and available as a desktop shortcut.</span></span>

* <span data-ttu-id="521d5-242">Using in Jupyter</span><span class="sxs-lookup"><span data-stu-id="521d5-242">Using in Jupyter</span></span>

<span data-ttu-id="521d5-243">Open Jupyter and click on the `New` button to create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="521d5-243">Open Jupyter and click on the `New` button to create a new notebook.</span></span> <span data-ttu-id="521d5-244">At this point, you can choose the kernel type as `Julia VERSION`</span><span class="sxs-lookup"><span data-stu-id="521d5-244">At this point, you can choose the kernel type as `Julia VERSION`</span></span> 

* <span data-ttu-id="521d5-245">Installing Julia packages</span><span class="sxs-lookup"><span data-stu-id="521d5-245">Installing Julia packages</span></span>

<span data-ttu-id="521d5-246">The default Julia location is a global environment readable by all users.</span><span class="sxs-lookup"><span data-stu-id="521d5-246">The default Julia location is a global environment readable by all users.</span></span> <span data-ttu-id="521d5-247">But only administrators can write / install global packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-247">But only administrators can write / install global packages.</span></span> <span data-ttu-id="521d5-248">In order to install package to the global environment, run Julia using one of the methods above.</span><span class="sxs-lookup"><span data-stu-id="521d5-248">In order to install package to the global environment, run Julia using one of the methods above.</span></span> <span data-ttu-id="521d5-249">Then you can run the Julia package manager commands like `Pkg.add()` to install or update packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-249">Then you can run the Julia package manager commands like `Pkg.add()` to install or update packages.</span></span> 


<span data-ttu-id="521d5-250">**Linux**:</span><span class="sxs-lookup"><span data-stu-id="521d5-250">**Linux**:</span></span>
* <span data-ttu-id="521d5-251">Running in terminal.</span><span class="sxs-lookup"><span data-stu-id="521d5-251">Running in terminal.</span></span>

<span data-ttu-id="521d5-252">Open terminal and just run `julia`.</span><span class="sxs-lookup"><span data-stu-id="521d5-252">Open terminal and just run `julia`.</span></span> 
* <span data-ttu-id="521d5-253">Using in an IDE</span><span class="sxs-lookup"><span data-stu-id="521d5-253">Using in an IDE</span></span>

<span data-ttu-id="521d5-254">Use `Juno` the Julia IDE installed on the DSVM and available as a Application menu shortcut.</span><span class="sxs-lookup"><span data-stu-id="521d5-254">Use `Juno` the Julia IDE installed on the DSVM and available as a Application menu shortcut.</span></span>

* <span data-ttu-id="521d5-255">Using in Jupyter</span><span class="sxs-lookup"><span data-stu-id="521d5-255">Using in Jupyter</span></span>

<span data-ttu-id="521d5-256">Open Jupyter and click on the `New` button to create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="521d5-256">Open Jupyter and click on the `New` button to create a new notebook.</span></span> <span data-ttu-id="521d5-257">At this point, you can choose the kernel type as `Julia VERSION`</span><span class="sxs-lookup"><span data-stu-id="521d5-257">At this point, you can choose the kernel type as `Julia VERSION`</span></span> 

* <span data-ttu-id="521d5-258">Installing Julia packages</span><span class="sxs-lookup"><span data-stu-id="521d5-258">Installing Julia packages</span></span>

<span data-ttu-id="521d5-259">The default Julia location is a global environment readable by all users.</span><span class="sxs-lookup"><span data-stu-id="521d5-259">The default Julia location is a global environment readable by all users.</span></span> <span data-ttu-id="521d5-260">But only administrators can write / install global packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-260">But only administrators can write / install global packages.</span></span> <span data-ttu-id="521d5-261">In order to install package to the global environment, run Julia using one of the methods above.</span><span class="sxs-lookup"><span data-stu-id="521d5-261">In order to install package to the global environment, run Julia using one of the methods above.</span></span> <span data-ttu-id="521d5-262">Then you can run the Julia package manager commands like `Pkg.add()` to install or update packages.</span><span class="sxs-lookup"><span data-stu-id="521d5-262">Then you can run the Julia package manager commands like `Pkg.add()` to install or update packages.</span></span> 

## <a name="other-languages"></a><span data-ttu-id="521d5-263">Other languages</span><span class="sxs-lookup"><span data-stu-id="521d5-263">Other languages</span></span>

<span data-ttu-id="521d5-264">**C#**: Available on Windows and accessible through the Visual Studio Community edition or on a `Developer Command Prompt for Visual Studio` where you can just run `csc` command.</span><span class="sxs-lookup"><span data-stu-id="521d5-264">**C#**: Available on Windows and accessible through the Visual Studio Community edition or on a `Developer Command Prompt for Visual Studio` where you can just run `csc` command.</span></span> 

<span data-ttu-id="521d5-265">**Java**: OpenJDK is available on both Linux and Windows edition of the DSVM and set on the path.</span><span class="sxs-lookup"><span data-stu-id="521d5-265">**Java**: OpenJDK is available on both Linux and Windows edition of the DSVM and set on the path.</span></span> <span data-ttu-id="521d5-266">You can type `javac` or `java` command on the command prompt in Windows or on bash shell in Linux to use Java.</span><span class="sxs-lookup"><span data-stu-id="521d5-266">You can type `javac` or `java` command on the command prompt in Windows or on bash shell in Linux to use Java.</span></span> 

<span data-ttu-id="521d5-267">**node.js**: node.js is available on both Linux and Windows edition of the DSVM and set on the path.</span><span class="sxs-lookup"><span data-stu-id="521d5-267">**node.js**: node.js is available on both Linux and Windows edition of the DSVM and set on the path.</span></span> <span data-ttu-id="521d5-268">You can type `node` or `npm` command on the command prompt in Windows or on bash shell in Linux to access node.js.</span><span class="sxs-lookup"><span data-stu-id="521d5-268">You can type `node` or `npm` command on the command prompt in Windows or on bash shell in Linux to access node.js.</span></span> <span data-ttu-id="521d5-269">On Windows, the Node.js tools for Visual Studio extension is installed to provide a graphical IDE to develop your node.js application.</span><span class="sxs-lookup"><span data-stu-id="521d5-269">On Windows, the Node.js tools for Visual Studio extension is installed to provide a graphical IDE to develop your node.js application.</span></span> 

<span data-ttu-id="521d5-270">**F#**: Available on Windows and accessible through the Visual Studio Community edition or on a `Developer Command Prompt for Visual Studio` where you can just run `fsc` command.</span><span class="sxs-lookup"><span data-stu-id="521d5-270">**F#**: Available on Windows and accessible through the Visual Studio Community edition or on a `Developer Command Prompt for Visual Studio` where you can just run `fsc` command.</span></span> 


