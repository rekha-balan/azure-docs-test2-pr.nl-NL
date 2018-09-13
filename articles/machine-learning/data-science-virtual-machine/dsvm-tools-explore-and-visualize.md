---
title: Data exploration and visualization tools - Azure | Microsoft Docs
description: Data exploration and visualization tools for the Data Science Virtual Machine.
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
ms.date: 03/16/2018
ms.author: gokuma
ms.openlocfilehash: df29d0a55317d06d656d8444c6bd7754c6c955eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871399"
---
# <a name="data-exploration-and-visualization-tools-on-the-data-science-virtual-machine"></a><span data-ttu-id="a9811-104">Data exploration and visualization tools on the Data Science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="a9811-104">Data exploration and visualization tools on the Data Science Virtual Machine</span></span>

<span data-ttu-id="a9811-105">A key step in data science is to understand the data.</span><span class="sxs-lookup"><span data-stu-id="a9811-105">A key step in data science is to understand the data.</span></span> <span data-ttu-id="a9811-106">Visualization and data exploration tools help accelerate data understanding.</span><span class="sxs-lookup"><span data-stu-id="a9811-106">Visualization and data exploration tools help accelerate data understanding.</span></span> <span data-ttu-id="a9811-107">Here are some tools provided on the DSVM that faciliate this key step.</span><span class="sxs-lookup"><span data-stu-id="a9811-107">Here are some tools provided on the DSVM that faciliate this key step.</span></span> 

## <a name="apache-drill"></a><span data-ttu-id="a9811-108">Apache Drill</span><span class="sxs-lookup"><span data-stu-id="a9811-108">Apache Drill</span></span>
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a9811-109">What is it?</span><span class="sxs-lookup"><span data-stu-id="a9811-109">What is it?</span></span>   | <span data-ttu-id="a9811-110">Open source SQL query engine on Big data</span><span class="sxs-lookup"><span data-stu-id="a9811-110">Open source SQL query engine on Big data</span></span>    |
| <span data-ttu-id="a9811-111">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="a9811-111">Supported DSVM Versions</span></span>      | <span data-ttu-id="a9811-112">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="a9811-112">Windows, Linux</span></span>  |
| <span data-ttu-id="a9811-113">How is it configured / installed on the DSVM?</span><span class="sxs-lookup"><span data-stu-id="a9811-113">How is it configured / installed on the DSVM?</span></span>      |  <span data-ttu-id="a9811-114">Installed in `/dsvm/tools/drill*` in embedded mode only</span><span class="sxs-lookup"><span data-stu-id="a9811-114">Installed in `/dsvm/tools/drill*` in embedded mode only</span></span>   |
| <span data-ttu-id="a9811-115">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a9811-115">Typical Uses</span></span>      |  <span data-ttu-id="a9811-116">In-situ Data exploration without requiring ETL.</span><span class="sxs-lookup"><span data-stu-id="a9811-116">In-situ Data exploration without requiring ETL.</span></span> <span data-ttu-id="a9811-117">Query different data sources and formats includign CSV, JSON, relational tables, Hadoop</span><span class="sxs-lookup"><span data-stu-id="a9811-117">Query different data sources and formats includign CSV, JSON, relational tables, Hadoop</span></span>     |
| <span data-ttu-id="a9811-118">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a9811-118">How to use / run it?</span></span>      | <span data-ttu-id="a9811-119">Desktop Shortcut</span><span class="sxs-lookup"><span data-stu-id="a9811-119">Desktop Shortcut</span></span>  <br/> [<span data-ttu-id="a9811-120">Get started with Drill in 10 minutes</span><span class="sxs-lookup"><span data-stu-id="a9811-120">Get started with Drill in 10 minutes</span></span>](https://drill.apache.org/docs/drill-in-10-minutes/)  |
| <span data-ttu-id="a9811-121">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a9811-121">Related Tools on the DSVM</span></span>      |   <span data-ttu-id="a9811-122">Rattle, Weka, SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="a9811-122">Rattle, Weka, SQL Server Management Studio</span></span>      |

## <a name="weka"></a><span data-ttu-id="a9811-123">Weka</span><span class="sxs-lookup"><span data-stu-id="a9811-123">Weka</span></span>
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a9811-124">What is it?</span><span class="sxs-lookup"><span data-stu-id="a9811-124">What is it?</span></span>   |  <span data-ttu-id="a9811-125">Weka is a collection of machine learning algorithms for data mining tasks.</span><span class="sxs-lookup"><span data-stu-id="a9811-125">Weka is a collection of machine learning algorithms for data mining tasks.</span></span> <span data-ttu-id="a9811-126">The algorithms can either be applied directly to a dataset or called from your own Java code.</span><span class="sxs-lookup"><span data-stu-id="a9811-126">The algorithms can either be applied directly to a dataset or called from your own Java code.</span></span> <span data-ttu-id="a9811-127">Weka contains tools for data pre-processing, classification, regression, clustering, association rules, and visualization.</span><span class="sxs-lookup"><span data-stu-id="a9811-127">Weka contains tools for data pre-processing, classification, regression, clustering, association rules, and visualization.</span></span> |
| <span data-ttu-id="a9811-128">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="a9811-128">Supported DSVM Editions</span></span>     | <span data-ttu-id="a9811-129">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="a9811-129">Windows, Linux</span></span>     |
| <span data-ttu-id="a9811-130">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a9811-130">Typical Uses</span></span>      | <span data-ttu-id="a9811-131">General ML Tool</span><span class="sxs-lookup"><span data-stu-id="a9811-131">General ML Tool</span></span>     |
| <span data-ttu-id="a9811-132">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a9811-132">How to use / run it?</span></span>      | <span data-ttu-id="a9811-133">On Windows, search for Weka in the Start Menu.</span><span class="sxs-lookup"><span data-stu-id="a9811-133">On Windows, search for Weka in the Start Menu.</span></span> <span data-ttu-id="a9811-134">On Linux, log in with X2Go, then navigate to Applications -> Development -> Weka.</span><span class="sxs-lookup"><span data-stu-id="a9811-134">On Linux, log in with X2Go, then navigate to Applications -> Development -> Weka.</span></span> |
| <span data-ttu-id="a9811-135">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="a9811-135">Links to Samples</span></span>      | [<span data-ttu-id="a9811-136">Weka samples</span><span class="sxs-lookup"><span data-stu-id="a9811-136">Weka samples</span></span>](http://www.cs.waikato.ac.nz/ml/weka/documentation.html) |
| <span data-ttu-id="a9811-137">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a9811-137">Related Tools on the DSVM</span></span>      |<span data-ttu-id="a9811-138">LightGBM, Rattle, Xgboost</span><span class="sxs-lookup"><span data-stu-id="a9811-138">LightGBM, Rattle, Xgboost</span></span>   |

## <a name="rattle"></a><span data-ttu-id="a9811-139">Rattle</span><span class="sxs-lookup"><span data-stu-id="a9811-139">Rattle</span></span>
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a9811-140">What is it?</span><span class="sxs-lookup"><span data-stu-id="a9811-140">What is it?</span></span>   |   <span data-ttu-id="a9811-141">A Graphical User Interface for Data Mining using R</span><span class="sxs-lookup"><span data-stu-id="a9811-141">A Graphical User Interface for Data Mining using R</span></span>   |
| <span data-ttu-id="a9811-142">Supported DSVM Editions</span><span class="sxs-lookup"><span data-stu-id="a9811-142">Supported DSVM Editions</span></span>     | <span data-ttu-id="a9811-143">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="a9811-143">Windows, Linux</span></span>     |
| <span data-ttu-id="a9811-144">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a9811-144">Typical Uses</span></span>      | <span data-ttu-id="a9811-145">General UI Data Mining tool for R</span><span class="sxs-lookup"><span data-stu-id="a9811-145">General UI Data Mining tool for R</span></span>    |
| <span data-ttu-id="a9811-146">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a9811-146">How to use / run it?</span></span>      | <span data-ttu-id="a9811-147">UI tool.</span><span class="sxs-lookup"><span data-stu-id="a9811-147">UI tool.</span></span> <span data-ttu-id="a9811-148">On Windows, start a Command Prompt, run R, then inside R run `rattle()`.</span><span class="sxs-lookup"><span data-stu-id="a9811-148">On Windows, start a Command Prompt, run R, then inside R run `rattle()`.</span></span> <span data-ttu-id="a9811-149">On Linux, connect with X2Go, start a terminal, run R, then inside R run `rattle()`.</span><span class="sxs-lookup"><span data-stu-id="a9811-149">On Linux, connect with X2Go, start a terminal, run R, then inside R run `rattle()`.</span></span> |
| <span data-ttu-id="a9811-150">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="a9811-150">Links to Samples</span></span>      | [<span data-ttu-id="a9811-151">Rattle</span><span class="sxs-lookup"><span data-stu-id="a9811-151">Rattle</span></span>](https://togaware.com/onepager/) |
| <span data-ttu-id="a9811-152">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a9811-152">Related Tools on the DSVM</span></span>      |<span data-ttu-id="a9811-153">LightGBM, Weka, Xgboost</span><span class="sxs-lookup"><span data-stu-id="a9811-153">LightGBM, Weka, Xgboost</span></span>   |

## <a name="powerbi-desktop"></a><span data-ttu-id="a9811-154">PowerBI Desktop</span><span class="sxs-lookup"><span data-stu-id="a9811-154">PowerBI Desktop</span></span> 
|    |           |
| ------------- | ------------- |
| <span data-ttu-id="a9811-155">What is it?</span><span class="sxs-lookup"><span data-stu-id="a9811-155">What is it?</span></span>   | <span data-ttu-id="a9811-156">Interactive Data Visualization and BI Tool</span><span class="sxs-lookup"><span data-stu-id="a9811-156">Interactive Data Visualization and BI Tool</span></span>    |
| <span data-ttu-id="a9811-157">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="a9811-157">Supported DSVM Versions</span></span>      | <span data-ttu-id="a9811-158">Windows</span><span class="sxs-lookup"><span data-stu-id="a9811-158">Windows</span></span>  |
| <span data-ttu-id="a9811-159">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="a9811-159">Typical Uses</span></span>      |  <span data-ttu-id="a9811-160">Data Visualization and building Dashboards</span><span class="sxs-lookup"><span data-stu-id="a9811-160">Data Visualization and building Dashboards</span></span>   |
| <span data-ttu-id="a9811-161">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="a9811-161">How to use / run it?</span></span>      | <span data-ttu-id="a9811-162">Desktop Shortcut (`C:\Program Files\Microsoft Power BI Desktop\bin\PBIDesktop.exe`)</span><span class="sxs-lookup"><span data-stu-id="a9811-162">Desktop Shortcut (`C:\Program Files\Microsoft Power BI Desktop\bin\PBIDesktop.exe`)</span></span>      |
| <span data-ttu-id="a9811-163">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="a9811-163">Related Tools on the DSVM</span></span>      |   <span data-ttu-id="a9811-164">Visual Studio 2017, Visual Studio Code, Juno</span><span class="sxs-lookup"><span data-stu-id="a9811-164">Visual Studio 2017, Visual Studio Code, Juno</span></span>      |

