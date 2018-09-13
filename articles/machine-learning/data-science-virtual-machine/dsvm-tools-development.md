---
title: Data Science Virtual Machine development tools - Azure | Microsoft Docs
description: Data Science Virtual machine development tools.
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
ms.openlocfilehash: b8b0b8934b51080c3583281673183c1498c26417
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855948"
---
# <a name="development-tools-on-the-data-science-virtual-machine"></a><span data-ttu-id="a3559-104">Development tools on the Data Science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="a3559-104">Development tools on the Data Science Virtual Machine</span></span>

<span data-ttu-id="a3559-105">The Data Science Virtual Machine (DSVM) provides a productive environment for your development by bundling several popular tools and IDE.</span><span class="sxs-lookup"><span data-stu-id="a3559-105">The Data Science Virtual Machine (DSVM) provides a productive environment for your development by bundling several popular tools and IDE.</span></span> <span data-ttu-id="a3559-106">Here are some tools that are provided on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="a3559-106">Here are some tools that are provided on the DSVM.</span></span> 

## <a name="visual-studio-2017"></a><span data-ttu-id="a3559-107">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a3559-107">Visual Studio 2017</span></span>  
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a3559-108">What is it?</span><span class="sxs-lookup"><span data-stu-id="a3559-108">What is it?</span></span>   | <span data-ttu-id="a3559-109">General Purpose IDE</span><span class="sxs-lookup"><span data-stu-id="a3559-109">General Purpose IDE</span></span>      |
| <span data-ttu-id="a3559-110">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="a3559-110">Supported DSVM Versions</span></span>      | <span data-ttu-id="a3559-111">Windows</span><span class="sxs-lookup"><span data-stu-id="a3559-111">Windows</span></span>      |
| <span data-ttu-id="a3559-112">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a3559-112">Typical Uses</span></span>      | <span data-ttu-id="a3559-113">Software Development</span><span class="sxs-lookup"><span data-stu-id="a3559-113">Software Development</span></span>    |
| <span data-ttu-id="a3559-114">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="a3559-114">How is it configured / installed on the DSVM?</span></span>      | <span data-ttu-id="a3559-115">Data Science Workload (Python and R tools), Azure workload (Hadoop, Data Lake), Node.js, SQL Server tools, [Visual Studio Tools for AI](https://github.com/Microsoft/vs-tools-for-ai)</span><span class="sxs-lookup"><span data-stu-id="a3559-115">Data Science Workload (Python and R tools), Azure workload (Hadoop, Data Lake), Node.js, SQL Server tools, [Visual Studio Tools for AI](https://github.com/Microsoft/vs-tools-for-ai)</span></span>    |
| <span data-ttu-id="a3559-116">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a3559-116">How to use / run it?</span></span>      | <span data-ttu-id="a3559-117">Desktop Shortcut (`C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\devenv.exe`)</span><span class="sxs-lookup"><span data-stu-id="a3559-117">Desktop Shortcut (`C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\devenv.exe`)</span></span>    |
| <span data-ttu-id="a3559-118">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a3559-118">Related Tools on the DSVM</span></span>      |     <span data-ttu-id="a3559-119">Visual Studio Code, RStudio, Juno</span><span class="sxs-lookup"><span data-stu-id="a3559-119">Visual Studio Code, RStudio, Juno</span></span>  |

## <a name="visual-studio-code"></a><span data-ttu-id="a3559-120">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a3559-120">Visual Studio Code</span></span> 
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a3559-121">What is it?</span><span class="sxs-lookup"><span data-stu-id="a3559-121">What is it?</span></span>   | <span data-ttu-id="a3559-122">General Purpose IDE</span><span class="sxs-lookup"><span data-stu-id="a3559-122">General Purpose IDE</span></span>      |
| <span data-ttu-id="a3559-123">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="a3559-123">Supported DSVM Versions</span></span>      | <span data-ttu-id="a3559-124">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="a3559-124">Windows, Linux</span></span>     |
| <span data-ttu-id="a3559-125">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a3559-125">Typical Uses</span></span>      | <span data-ttu-id="a3559-126">Code editor and Git integration</span><span class="sxs-lookup"><span data-stu-id="a3559-126">Code editor and Git integration</span></span>   |
| <span data-ttu-id="a3559-127">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a3559-127">How to use / run it?</span></span>      | <span data-ttu-id="a3559-128">Desktop Shortcut (`C:\Program Files (x86)\Microsoft VS Code\Code.exe`) in Windows, desktop shortcut or terminal (`code`) in Linux</span><span class="sxs-lookup"><span data-stu-id="a3559-128">Desktop Shortcut (`C:\Program Files (x86)\Microsoft VS Code\Code.exe`) in Windows, desktop shortcut or terminal (`code`) in Linux</span></span>    |
| <span data-ttu-id="a3559-129">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a3559-129">Related Tools on the DSVM</span></span>      |     <span data-ttu-id="a3559-130">Visual Studio 2017, RStudio, Juno</span><span class="sxs-lookup"><span data-stu-id="a3559-130">Visual Studio 2017, RStudio, Juno</span></span>  |

## <a name="rstudio--desktop"></a><span data-ttu-id="a3559-131">RStudio  Desktop</span><span class="sxs-lookup"><span data-stu-id="a3559-131">RStudio  Desktop</span></span> 
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a3559-132">What is it?</span><span class="sxs-lookup"><span data-stu-id="a3559-132">What is it?</span></span>   | <span data-ttu-id="a3559-133">Client IDE for R</span><span class="sxs-lookup"><span data-stu-id="a3559-133">Client IDE for R</span></span>    |
| <span data-ttu-id="a3559-134">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="a3559-134">Supported DSVM Versions</span></span>      | <span data-ttu-id="a3559-135">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="a3559-135">Windows, Linux</span></span>      |
| <span data-ttu-id="a3559-136">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a3559-136">Typical Uses</span></span>      |  <span data-ttu-id="a3559-137">R development</span><span class="sxs-lookup"><span data-stu-id="a3559-137">R development</span></span>     |
| <span data-ttu-id="a3559-138">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a3559-138">How to use / run it?</span></span>      | <span data-ttu-id="a3559-139">Desktop Shortcut (`C:\Program Files\RStudio\bin\rstudio.exe`) on Windows, Desktop Shortcut (`/usr/bin/rstudio`) on Linux</span><span class="sxs-lookup"><span data-stu-id="a3559-139">Desktop Shortcut (`C:\Program Files\RStudio\bin\rstudio.exe`) on Windows, Desktop Shortcut (`/usr/bin/rstudio`) on Linux</span></span>      |
| <span data-ttu-id="a3559-140">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a3559-140">Related Tools on the DSVM</span></span>      |   <span data-ttu-id="a3559-141">Visual Studio 2017, Visual Studio Code, Juno</span><span class="sxs-lookup"><span data-stu-id="a3559-141">Visual Studio 2017, Visual Studio Code, Juno</span></span>      |

## <a name="rstudio--server"></a><span data-ttu-id="a3559-142">RStudio  Server</span><span class="sxs-lookup"><span data-stu-id="a3559-142">RStudio  Server</span></span> 
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a3559-143">What is it?</span><span class="sxs-lookup"><span data-stu-id="a3559-143">What is it?</span></span>   | <span data-ttu-id="a3559-144">Web-based IDE for R</span><span class="sxs-lookup"><span data-stu-id="a3559-144">Web-based IDE for R</span></span>    |
| <span data-ttu-id="a3559-145">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="a3559-145">Supported DSVM Versions</span></span>      | <span data-ttu-id="a3559-146">Linux</span><span class="sxs-lookup"><span data-stu-id="a3559-146">Linux</span></span>      |
| <span data-ttu-id="a3559-147">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a3559-147">Typical Uses</span></span>      |  <span data-ttu-id="a3559-148">R development</span><span class="sxs-lookup"><span data-stu-id="a3559-148">R development</span></span>     |
| <span data-ttu-id="a3559-149">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a3559-149">How to use / run it?</span></span>      | <span data-ttu-id="a3559-150">Enable the service with _systemctl enable rstudio-server_, then start the service with _systemctl start rstudio-server_.</span><span class="sxs-lookup"><span data-stu-id="a3559-150">Enable the service with _systemctl enable rstudio-server_, then start the service with _systemctl start rstudio-server_.</span></span> <span data-ttu-id="a3559-151">You can then log in to RStudio Server at http://your-vm-ip:8787.</span><span class="sxs-lookup"><span data-stu-id="a3559-151">You can then log in to RStudio Server at http://your-vm-ip:8787.</span></span>       |
| <span data-ttu-id="a3559-152">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a3559-152">Related Tools on the DSVM</span></span>      |   <span data-ttu-id="a3559-153">Visual Studio 2017, Visual Studio Code, RStudio Desktop</span><span class="sxs-lookup"><span data-stu-id="a3559-153">Visual Studio 2017, Visual Studio Code, RStudio Desktop</span></span>      |

## <a name="juno"></a><span data-ttu-id="a3559-154">Juno</span><span class="sxs-lookup"><span data-stu-id="a3559-154">Juno</span></span> 
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a3559-155">What is it?</span><span class="sxs-lookup"><span data-stu-id="a3559-155">What is it?</span></span>   | <span data-ttu-id="a3559-156">Client IDE for Julia language</span><span class="sxs-lookup"><span data-stu-id="a3559-156">Client IDE for Julia language</span></span>   |
| <span data-ttu-id="a3559-157">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="a3559-157">Supported DSVM Versions</span></span>      | <span data-ttu-id="a3559-158">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="a3559-158">Windows, Linux</span></span>      |
| <span data-ttu-id="a3559-159">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a3559-159">Typical Uses</span></span>      |  <span data-ttu-id="a3559-160">Julia development</span><span class="sxs-lookup"><span data-stu-id="a3559-160">Julia development</span></span>     |
| <span data-ttu-id="a3559-161">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a3559-161">How to use / run it?</span></span>      | <span data-ttu-id="a3559-162">Desktop Shortcut (`C:\JuliaPro-0.5.1.1\Juno.bat`) on Windows, Desktop Shortcut (`/opt/JuliaPro-VERSION/Juno`) on Linux</span><span class="sxs-lookup"><span data-stu-id="a3559-162">Desktop Shortcut (`C:\JuliaPro-0.5.1.1\Juno.bat`) on Windows, Desktop Shortcut (`/opt/JuliaPro-VERSION/Juno`) on Linux</span></span>      |
| <span data-ttu-id="a3559-163">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a3559-163">Related Tools on the DSVM</span></span>      |   <span data-ttu-id="a3559-164">Visual Studio 2017, Visual Studio Code, RStudio</span><span class="sxs-lookup"><span data-stu-id="a3559-164">Visual Studio 2017, Visual Studio Code, RStudio</span></span>      |

## <a name="pycharm"></a><span data-ttu-id="a3559-165">Pycharm</span><span class="sxs-lookup"><span data-stu-id="a3559-165">Pycharm</span></span>
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a3559-166">What is it?</span><span class="sxs-lookup"><span data-stu-id="a3559-166">What is it?</span></span>   | <span data-ttu-id="a3559-167">Client IDE for Python language</span><span class="sxs-lookup"><span data-stu-id="a3559-167">Client IDE for Python language</span></span>    |
| <span data-ttu-id="a3559-168">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="a3559-168">Supported DSVM Versions</span></span>      | <span data-ttu-id="a3559-169">Linux</span><span class="sxs-lookup"><span data-stu-id="a3559-169">Linux</span></span>      |
| <span data-ttu-id="a3559-170">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a3559-170">Typical Uses</span></span>      |  <span data-ttu-id="a3559-171">R development</span><span class="sxs-lookup"><span data-stu-id="a3559-171">R development</span></span>     |
| <span data-ttu-id="a3559-172">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a3559-172">How to use / run it?</span></span>      | <span data-ttu-id="a3559-173">Desktop Shortcut (`/usr/bin/pycharm`) on Linux</span><span class="sxs-lookup"><span data-stu-id="a3559-173">Desktop Shortcut (`/usr/bin/pycharm`) on Linux</span></span>      |
| <span data-ttu-id="a3559-174">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a3559-174">Related Tools on the DSVM</span></span>      |   <span data-ttu-id="a3559-175">Visual Studio 2017, Visual Studio Code, RStudio</span><span class="sxs-lookup"><span data-stu-id="a3559-175">Visual Studio 2017, Visual Studio Code, RStudio</span></span>      |



## <a name="powerbi-desktop"></a><span data-ttu-id="a3559-176">PowerBI Desktop</span><span class="sxs-lookup"><span data-stu-id="a3559-176">PowerBI Desktop</span></span> 
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a3559-177">What is it?</span><span class="sxs-lookup"><span data-stu-id="a3559-177">What is it?</span></span>   | <span data-ttu-id="a3559-178">Interactive Data Visualization and BI Tool</span><span class="sxs-lookup"><span data-stu-id="a3559-178">Interactive Data Visualization and BI Tool</span></span>    |
| <span data-ttu-id="a3559-179">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="a3559-179">Supported DSVM Versions</span></span>      | <span data-ttu-id="a3559-180">Windows</span><span class="sxs-lookup"><span data-stu-id="a3559-180">Windows</span></span>  |
| <span data-ttu-id="a3559-181">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a3559-181">Typical Uses</span></span>      |  <span data-ttu-id="a3559-182">Data Visualization and building Dashboards</span><span class="sxs-lookup"><span data-stu-id="a3559-182">Data Visualization and building Dashboards</span></span>   |
| <span data-ttu-id="a3559-183">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a3559-183">How to use / run it?</span></span>      | <span data-ttu-id="a3559-184">Desktop Shortcut (`C:\Program Files\Microsoft Power BI Desktop\bin\PBIDesktop.exe`)</span><span class="sxs-lookup"><span data-stu-id="a3559-184">Desktop Shortcut (`C:\Program Files\Microsoft Power BI Desktop\bin\PBIDesktop.exe`)</span></span>      |
| <span data-ttu-id="a3559-185">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a3559-185">Related Tools on the DSVM</span></span>      |   <span data-ttu-id="a3559-186">Visual Studio 2017, Visual Studio Code, Juno</span><span class="sxs-lookup"><span data-stu-id="a3559-186">Visual Studio 2017, Visual Studio Code, Juno</span></span>      |

