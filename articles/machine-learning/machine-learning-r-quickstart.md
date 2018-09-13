---
title: Quickstart tutorial for R language for Machine Learning | Microsoft Docs
description: Use this R programming tutorial to get started quickly using the R language with Azure Machine Learning Studio to create a forecasting solution.
keywords: quickstart,r language,r programming language,r programming tutorial
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: f1c3a10a3e6e0787bec94f42442c199b97b8b302
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552051"
---
# <a name="quickstart-tutorial-for-the-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="29b79-104">Quickstart tutorial for the R programming language for Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="29b79-104">Quickstart tutorial for the R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="29b79-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="29b79-105">Introduction</span></span>
<span data-ttu-id="29b79-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using the R programming language.</span><span class="sxs-lookup"><span data-stu-id="29b79-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using the R programming language.</span></span> <span data-ttu-id="29b79-107">Follow this R programming tutorial to create, test and execute R code within Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="29b79-107">Follow this R programming tutorial to create, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="29b79-108">As you work through tutorial, you will create a complete forecasting solution by using the R language in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="29b79-108">As you work through tutorial, you will create a complete forecasting solution by using the R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="29b79-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span><span class="sxs-lookup"><span data-stu-id="29b79-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="29b79-110">The powerful R language has been described as the lingua franca of analytics.</span><span class="sxs-lookup"><span data-stu-id="29b79-110">The powerful R language has been described as the lingua franca of analytics.</span></span> <span data-ttu-id="29b79-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides the scalability and ease of deployment of Azure Machine Learning with the flexibility and deep analytics of R.</span><span class="sxs-lookup"><span data-stu-id="29b79-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides the scalability and ease of deployment of Azure Machine Learning with the flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-the-dataset"></a><span data-ttu-id="29b79-112">Forecasting and the dataset</span><span class="sxs-lookup"><span data-stu-id="29b79-112">Forecasting and the dataset</span></span>
<span data-ttu-id="29b79-113">Forecasting is a widely employed and quite useful analytical method.</span><span class="sxs-lookup"><span data-stu-id="29b79-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="29b79-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, to predicting macroeconomic variables.</span><span class="sxs-lookup"><span data-stu-id="29b79-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, to predicting macroeconomic variables.</span></span> <span data-ttu-id="29b79-115">Forecasting is typically done with time series models.</span><span class="sxs-lookup"><span data-stu-id="29b79-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="29b79-116">Time series data is data in which the values have a time index.</span><span class="sxs-lookup"><span data-stu-id="29b79-116">Time series data is data in which the values have a time index.</span></span> <span data-ttu-id="29b79-117">The time index can be regular, e.g. every month or every minute, or irregular.</span><span class="sxs-lookup"><span data-stu-id="29b79-117">The time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="29b79-118">A time series model is based on time series data.</span><span class="sxs-lookup"><span data-stu-id="29b79-118">A time series model is based on time series data.</span></span> <span data-ttu-id="29b79-119">The R programming language contains a flexible framework and extensive analytics for time series data.</span><span class="sxs-lookup"><span data-stu-id="29b79-119">The R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="29b79-120">In this quickstart guide we will be working with California dairy production and pricing data.</span><span class="sxs-lookup"><span data-stu-id="29b79-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="29b79-121">This data includes monthly information on the production of several dairy products and the price of milk fat, a benchmark commodity.</span><span class="sxs-lookup"><span data-stu-id="29b79-121">This data includes monthly information on the production of several dairy products and the price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="29b79-122">The data used in this article, along with R scripts, can be [downloaded here][download].</span><span class="sxs-lookup"><span data-stu-id="29b79-122">The data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="29b79-123">This data was originally synthesized from information available from the University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="29b79-123">This data was originally synthesized from information available from the University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="29b79-124">Organization</span><span class="sxs-lookup"><span data-stu-id="29b79-124">Organization</span></span>
<span data-ttu-id="29b79-125">We will progress through several steps as you learn how to create, test and execute analytics and data manipulation R code in the Azure Machine Learning environment.</span><span class="sxs-lookup"><span data-stu-id="29b79-125">We will progress through several steps as you learn how to create, test and execute analytics and data manipulation R code in the Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="29b79-126">First we will explore the basics of using the R language in the Azure Machine Learning Studio environment.</span><span class="sxs-lookup"><span data-stu-id="29b79-126">First we will explore the basics of using the R language in the Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="29b79-127">Then we progress to discussing various aspects of I/O for data, R code and graphics in the Azure Machine Learning environment.</span><span class="sxs-lookup"><span data-stu-id="29b79-127">Then we progress to discussing various aspects of I/O for data, R code and graphics in the Azure Machine Learning environment.</span></span>
* <span data-ttu-id="29b79-128">We will then construct the first part of our forecasting solution by creating code for data cleaning and transformation.</span><span class="sxs-lookup"><span data-stu-id="29b79-128">We will then construct the first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="29b79-129">With our data prepared we will perform an analysis of the correlations between several of the variables in our dataset.</span><span class="sxs-lookup"><span data-stu-id="29b79-129">With our data prepared we will perform an analysis of the correlations between several of the variables in our dataset.</span></span>
* <span data-ttu-id="29b79-130">Finally, we will create a seasonal time series forecasting model for milk production.</span><span class="sxs-lookup"><span data-stu-id="29b79-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <a id="mlstudio"></a><span data-ttu-id="29b79-131">Interact with R language in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="29b79-131">Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="29b79-132">This section takes you through some basics of interacting with the R programming language in the Machine Learning Studio environment.</span><span class="sxs-lookup"><span data-stu-id="29b79-132">This section takes you through some basics of interacting with the R programming language in the Machine Learning Studio environment.</span></span> <span data-ttu-id="29b79-133">The R language provides a powerful tool to create customized analytics and data manipulation modules within the Azure Machine Learning environment.</span><span class="sxs-lookup"><span data-stu-id="29b79-133">The R language provides a powerful tool to create customized analytics and data manipulation modules within the Azure Machine Learning environment.</span></span>

<span data-ttu-id="29b79-134">I will use RStudio to develop, test and debug R code on a small scale.</span><span class="sxs-lookup"><span data-stu-id="29b79-134">I will use RStudio to develop, test and debug R code on a small scale.</span></span> <span data-ttu-id="29b79-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready to run.</span><span class="sxs-lookup"><span data-stu-id="29b79-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready to run.</span></span>  

### <a name="the-execute-r-script-module"></a><span data-ttu-id="29b79-136">The Execute R Script module</span><span class="sxs-lookup"><span data-stu-id="29b79-136">The Execute R Script module</span></span>
<span data-ttu-id="29b79-137">Within Machine Learning Studio, R scripts are run within the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-137">Within Machine Learning Studio, R scripts are run within the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="29b79-138">An example of the [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span><span class="sxs-lookup"><span data-stu-id="29b79-138">An example of the [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![R programming language: The Execute R Script module selected in Machine Learning Studio][1]

<span data-ttu-id="29b79-140">*Figure 1. The Machine Learning Studio environment showing the Execute R Script module selected.*</span><span class="sxs-lookup"><span data-stu-id="29b79-140">*Figure 1. The Machine Learning Studio environment showing the Execute R Script module selected.*</span></span>

<span data-ttu-id="29b79-141">Referring to Figure 1, let's look at some of the key parts of the Machine Learning Studio environment for working with the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-141">Referring to Figure 1, let's look at some of the key parts of the Machine Learning Studio environment for working with the [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="29b79-142">The modules in the experiment are shown in the center pane.</span><span class="sxs-lookup"><span data-stu-id="29b79-142">The modules in the experiment are shown in the center pane.</span></span>
* <span data-ttu-id="29b79-143">The upper part of the right pane contains a window to view and edit your R scripts.</span><span class="sxs-lookup"><span data-stu-id="29b79-143">The upper part of the right pane contains a window to view and edit your R scripts.</span></span>  
* <span data-ttu-id="29b79-144">The lower part of right pane shows some properties of the [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="29b79-144">The lower part of right pane shows some properties of the [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="29b79-145">You can view the error and output logs by clicking on the appropriate spots of this pane.</span><span class="sxs-lookup"><span data-stu-id="29b79-145">You can view the error and output logs by clicking on the appropriate spots of this pane.</span></span>

<span data-ttu-id="29b79-146">We will, of course, be discussing the [Execute R Script][execute-r-script] in greater detail in the rest of this document.</span><span class="sxs-lookup"><span data-stu-id="29b79-146">We will, of course, be discussing the [Execute R Script][execute-r-script] in greater detail in the rest of this document.</span></span>

<span data-ttu-id="29b79-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span><span class="sxs-lookup"><span data-stu-id="29b79-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="29b79-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span><span class="sxs-lookup"><span data-stu-id="29b79-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="29b79-149">Then cut and paste your functions into the R script window of the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-149">Then cut and paste your functions into the R script window of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="29b79-150">This approach allows you to harness both the RStudio integrated development environment (IDE) and the power of Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="29b79-150">This approach allows you to harness both the RStudio integrated development environment (IDE) and the power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="29b79-151">Execute R code</span><span class="sxs-lookup"><span data-stu-id="29b79-151">Execute R code</span></span>
<span data-ttu-id="29b79-152">Any R code in the [Execute R Script][execute-r-script] module will execute when you run the experiment by clicking on the **Run** button.</span><span class="sxs-lookup"><span data-stu-id="29b79-152">Any R code in the [Execute R Script][execute-r-script] module will execute when you run the experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="29b79-153">When execution has completed, a check mark will appear on the [Execute R Script][execute-r-script] icon.</span><span class="sxs-lookup"><span data-stu-id="29b79-153">When execution has completed, a check mark will appear on the [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="29b79-154">Defensive R coding for Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="29b79-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="29b79-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span><span class="sxs-lookup"><span data-stu-id="29b79-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="29b79-156">To maintain clarity, I have not included much in the way of checking or exception handling in most of the code examples shown.</span><span class="sxs-lookup"><span data-stu-id="29b79-156">To maintain clarity, I have not included much in the way of checking or exception handling in most of the code examples shown.</span></span> <span data-ttu-id="29b79-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span><span class="sxs-lookup"><span data-stu-id="29b79-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="29b79-158">If you need a more complete treatment of R exception handling, I recommend you read the applicable sections of the book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="29b79-158">If you need a more complete treatment of R exception handling, I recommend you read the applicable sections of the book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="29b79-159">Debug and test R in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="29b79-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="29b79-160">To reiterate, I recommend you test and debug your R code on a small scale in RStudio.</span><span class="sxs-lookup"><span data-stu-id="29b79-160">To reiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="29b79-161">However, there are cases where you will need to track down R code problems in the [Execute R Script][execute-r-script] itself.</span><span class="sxs-lookup"><span data-stu-id="29b79-161">However, there are cases where you will need to track down R code problems in the [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="29b79-162">In addition, it is good practice to check your results in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="29b79-162">In addition, it is good practice to check your results in Machine Learning Studio.</span></span>

<span data-ttu-id="29b79-163">Output from the execution of your R code and on the Azure Machine Learning platform is found primarily in output.log.</span><span class="sxs-lookup"><span data-stu-id="29b79-163">Output from the execution of your R code and on the Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="29b79-164">Some additional information will be seen in error.log.</span><span class="sxs-lookup"><span data-stu-id="29b79-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="29b79-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be to look at error.log.</span><span class="sxs-lookup"><span data-stu-id="29b79-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be to look at error.log.</span></span> <span data-ttu-id="29b79-166">This file can contain useful error messages to help you understand and correct your error.</span><span class="sxs-lookup"><span data-stu-id="29b79-166">This file can contain useful error messages to help you understand and correct your error.</span></span> <span data-ttu-id="29b79-167">To view error.log, click on **View error log** on the **properties pane** for the [Execute R Script][execute-r-script] containing the error.</span><span class="sxs-lookup"><span data-stu-id="29b79-167">To view error.log, click on **View error log** on the **properties pane** for the [Execute R Script][execute-r-script] containing the error.</span></span>

<span data-ttu-id="29b79-168">For example, I ran the following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span><span class="sxs-lookup"><span data-stu-id="29b79-168">For example, I ran the following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="29b79-169">This code fails to execute, resulting in an error condition.</span><span class="sxs-lookup"><span data-stu-id="29b79-169">This code fails to execute, resulting in an error condition.</span></span> <span data-ttu-id="29b79-170">Clicking on **View error log** on the **properties pane** produces the display shown in Figure 2.</span><span class="sxs-lookup"><span data-stu-id="29b79-170">Clicking on **View error log** on the **properties pane** produces the display shown in Figure 2.</span></span>

  ![Error message pop up][2]

<span data-ttu-id="29b79-172">*Figure 2. Error message pop-up.*</span><span class="sxs-lookup"><span data-stu-id="29b79-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="29b79-173">It looks like we need to look in output.log to see the R error message.</span><span class="sxs-lookup"><span data-stu-id="29b79-173">It looks like we need to look in output.log to see the R error message.</span></span> <span data-ttu-id="29b79-174">Click on the [Execute R Script][execute-r-script] and then click on the **View output.log** item on the **properties pane** to the right.</span><span class="sxs-lookup"><span data-stu-id="29b79-174">Click on the [Execute R Script][execute-r-script] and then click on the **View output.log** item on the **properties pane** to the right.</span></span> <span data-ttu-id="29b79-175">A new browser window opens, and I see the following.</span><span class="sxs-lookup"><span data-stu-id="29b79-175">A new browser window opens, and I see the following.</span></span>

    [Critical]     Error: Error 0063: The following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="29b79-176">This error message contains no surprises and clearly identifies the problem.</span><span class="sxs-lookup"><span data-stu-id="29b79-176">This error message contains no surprises and clearly identifies the problem.</span></span>

<span data-ttu-id="29b79-177">To inspect the value of any object in R, you can print these values to the output.log file.</span><span class="sxs-lookup"><span data-stu-id="29b79-177">To inspect the value of any object in R, you can print these values to the output.log file.</span></span> <span data-ttu-id="29b79-178">The rules for examining object values are essentially the same as in an interactive R session.</span><span class="sxs-lookup"><span data-stu-id="29b79-178">The rules for examining object values are essentially the same as in an interactive R session.</span></span> <span data-ttu-id="29b79-179">For example, if you type a variable name on a line, the value of the object will be printed to the output.log file.</span><span class="sxs-lookup"><span data-stu-id="29b79-179">For example, if you type a variable name on a line, the value of the object will be printed to the output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="29b79-180">Packages in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="29b79-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="29b79-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span><span class="sxs-lookup"><span data-stu-id="29b79-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="29b79-182">You can use the following code in the [Execute R Script][execute-r-script] module to retrieve a list of the preinstalled packages.</span><span class="sxs-lookup"><span data-stu-id="29b79-182">You can use the following code in the [Execute R Script][execute-r-script] module to retrieve a list of the preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="29b79-183">If you don't understand the last line of this code at the moment, read on.</span><span class="sxs-lookup"><span data-stu-id="29b79-183">If you don't understand the last line of this code at the moment, read on.</span></span> <span data-ttu-id="29b79-184">In the rest of this document we will extensively discuss using R in the Azure Machine Learning environment.</span><span class="sxs-lookup"><span data-stu-id="29b79-184">In the rest of this document we will extensively discuss using R in the Azure Machine Learning environment.</span></span>

### <a name="introduction-to-rstudio"></a><span data-ttu-id="29b79-185">Introduction to RStudio</span><span class="sxs-lookup"><span data-stu-id="29b79-185">Introduction to RStudio</span></span>
<span data-ttu-id="29b79-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of the R code used in this quick start guide.</span><span class="sxs-lookup"><span data-stu-id="29b79-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of the R code used in this quick start guide.</span></span> <span data-ttu-id="29b79-187">Once R code is tested and ready, you simply cut and paste from the RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-187">Once R code is tested and ready, you simply cut and paste from the RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="29b79-188">If you do not have the R programming language installed on your desktop machine, I recommend you do so now.</span><span class="sxs-lookup"><span data-stu-id="29b79-188">If you do not have the R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="29b79-189">Free downloads of open source R language are available at the Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="29b79-189">Free downloads of open source R language are available at the Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="29b79-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="29b79-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="29b79-191">Choose a nearby mirror and follow the download directions.</span><span class="sxs-lookup"><span data-stu-id="29b79-191">Choose a nearby mirror and follow the download directions.</span></span> <span data-ttu-id="29b79-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span><span class="sxs-lookup"><span data-stu-id="29b79-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="29b79-193">If you are new to RStudio, you should download and install the desktop version.</span><span class="sxs-lookup"><span data-stu-id="29b79-193">If you are new to RStudio, you should download and install the desktop version.</span></span> <span data-ttu-id="29b79-194">You can find the RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="29b79-194">You can find the RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="29b79-195">Follow the directions provided to install RStudio on your desktop machine.</span><span class="sxs-lookup"><span data-stu-id="29b79-195">Follow the directions provided to install RStudio on your desktop machine.</span></span>  

<span data-ttu-id="29b79-196">A tutorial introduction to RStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="29b79-196">A tutorial introduction to RStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="29b79-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span><span class="sxs-lookup"><span data-stu-id="29b79-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <a id="scriptmodule"></a><span data-ttu-id="29b79-198">Get data in and out of the Execute R Script module</span><span class="sxs-lookup"><span data-stu-id="29b79-198">Get data in and out of the Execute R Script module</span></span>
<span data-ttu-id="29b79-199">In this section we will discuss how you get data into and out of the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-199">In this section we will discuss how you get data into and out of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="29b79-200">We will review how to handle various data types read into and out of the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-200">We will review how to handle various data types read into and out of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="29b79-201">The complete code for this section is in the zip file you downloaded earlier.</span><span class="sxs-lookup"><span data-stu-id="29b79-201">The complete code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="29b79-202">Load and check data in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="29b79-202">Load and check data in Machine Learning Studio</span></span>
#### <a id="loading"></a><span data-ttu-id="29b79-203">Load the dataset</span><span class="sxs-lookup"><span data-stu-id="29b79-203">Load the dataset</span></span>
<span data-ttu-id="29b79-204">We will start by loading the **csdairydata.csv** file into Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="29b79-204">We will start by loading the **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="29b79-205">Start your Azure Machine Learning Studio environment.</span><span class="sxs-lookup"><span data-stu-id="29b79-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="29b79-206">Click on **+ NEW** at the lower left of your screen and select **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="29b79-206">Click on **+ NEW** at the lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="29b79-207">Select **From Local File**, and then **Browse** to select the file.</span><span class="sxs-lookup"><span data-stu-id="29b79-207">Select **From Local File**, and then **Browse** to select the file.</span></span>
* <span data-ttu-id="29b79-208">Make sure you have selected **Generic CSV file with header (.csv)** as the type for the dataset.</span><span class="sxs-lookup"><span data-stu-id="29b79-208">Make sure you have selected **Generic CSV file with header (.csv)** as the type for the dataset.</span></span>
* <span data-ttu-id="29b79-209">Click the check mark.</span><span class="sxs-lookup"><span data-stu-id="29b79-209">Click the check mark.</span></span>
* <span data-ttu-id="29b79-210">After the dataset has been uploaded, you should see the new dataset by clicking on the **Datasets** tab.</span><span class="sxs-lookup"><span data-stu-id="29b79-210">After the dataset has been uploaded, you should see the new dataset by clicking on the **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="29b79-211">Create an experiment</span><span class="sxs-lookup"><span data-stu-id="29b79-211">Create an experiment</span></span>
<span data-ttu-id="29b79-212">Now that we have some data in Machine Learning Studio, we need to create an experiment to do the analysis.</span><span class="sxs-lookup"><span data-stu-id="29b79-212">Now that we have some data in Machine Learning Studio, we need to create an experiment to do the analysis.</span></span>  

* <span data-ttu-id="29b79-213">Click on **+ NEW** at the lower left and select **Experiment**, then **Blank Experiment**.</span><span class="sxs-lookup"><span data-stu-id="29b79-213">Click on **+ NEW** at the lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="29b79-214">You can name your experiment by selecting, and modifying, the **Experiment created on ...** title at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="29b79-214">You can name your experiment by selecting, and modifying, the **Experiment created on ...** title at the top of the page.</span></span> <span data-ttu-id="29b79-215">For example, changing it to **CA Dairy Analysis**.</span><span class="sxs-lookup"><span data-stu-id="29b79-215">For example, changing it to **CA Dairy Analysis**.</span></span>
* <span data-ttu-id="29b79-216">On the left of the experiment page, expand **Saved Datasets**, and then **My Datasets**.</span><span class="sxs-lookup"><span data-stu-id="29b79-216">On the left of the experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="29b79-217">You should see the **cadairydata.csv** that you uploaded earlier.</span><span class="sxs-lookup"><span data-stu-id="29b79-217">You should see the **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="29b79-218">Drag and drop the **csdairydata.csv dataset** onto the experiment.</span><span class="sxs-lookup"><span data-stu-id="29b79-218">Drag and drop the **csdairydata.csv dataset** onto the experiment.</span></span>
* <span data-ttu-id="29b79-219">In the **Search experiment items** box on the top of the left pane, type [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="29b79-219">In the **Search experiment items** box on the top of the left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="29b79-220">You will see the module appear in the search list.</span><span class="sxs-lookup"><span data-stu-id="29b79-220">You will see the module appear in the search list.</span></span>
* <span data-ttu-id="29b79-221">Drag and drop the [Execute R Script][execute-r-script] module onto your pallet.</span><span class="sxs-lookup"><span data-stu-id="29b79-221">Drag and drop the [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="29b79-222">Connect the output of the **csdairydata.csv dataset** to the leftmost input (**Dataset1**) of the [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="29b79-222">Connect the output of the **csdairydata.csv dataset** to the leftmost input (**Dataset1**) of the [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="29b79-223">**Don't forget to click on 'Save'!**</span><span class="sxs-lookup"><span data-stu-id="29b79-223">**Don't forget to click on 'Save'!**</span></span>  

<span data-ttu-id="29b79-224">At this point your experiment should look something like Figure 3.</span><span class="sxs-lookup"><span data-stu-id="29b79-224">At this point your experiment should look something like Figure 3.</span></span>

![The CA Dairy Analysis experiment with dataset and Execute R Script module][3]

<span data-ttu-id="29b79-226">*Figure 3. The CA Dairy Analysis experiment with dataset and Execute R Script module.*</span><span class="sxs-lookup"><span data-stu-id="29b79-226">*Figure 3. The CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-the-data"></a><span data-ttu-id="29b79-227">Check on the data</span><span class="sxs-lookup"><span data-stu-id="29b79-227">Check on the data</span></span>
<span data-ttu-id="29b79-228">Let's have a look at the data we have loaded into our experiment.</span><span class="sxs-lookup"><span data-stu-id="29b79-228">Let's have a look at the data we have loaded into our experiment.</span></span> <span data-ttu-id="29b79-229">In the experiment, click on the output of the **cadairydata.csv dataset** and select **visualize**.</span><span class="sxs-lookup"><span data-stu-id="29b79-229">In the experiment, click on the output of the **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="29b79-230">You should see something like Figure 4.</span><span class="sxs-lookup"><span data-stu-id="29b79-230">You should see something like Figure 4.</span></span>  

![Summary of the cadairydata.csv dataset][4]

<span data-ttu-id="29b79-232">*Figure 4. Summary of the cadairydata.csv dataset.*</span><span class="sxs-lookup"><span data-stu-id="29b79-232">*Figure 4. Summary of the cadairydata.csv dataset.*</span></span>

<span data-ttu-id="29b79-233">In this view we see a lot of useful information.</span><span class="sxs-lookup"><span data-stu-id="29b79-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="29b79-234">We can see the first several rows of that dataset.</span><span class="sxs-lookup"><span data-stu-id="29b79-234">We can see the first several rows of that dataset.</span></span> <span data-ttu-id="29b79-235">If we select a column, the Statistics section shows more information about the column.</span><span class="sxs-lookup"><span data-stu-id="29b79-235">If we select a column, the Statistics section shows more information about the column.</span></span> <span data-ttu-id="29b79-236">For example, the Feature Type row shows us what data types Azure Machine Learning Studio assigned to the column.</span><span class="sxs-lookup"><span data-stu-id="29b79-236">For example, the Feature Type row shows us what data types Azure Machine Learning Studio assigned to the column.</span></span> <span data-ttu-id="29b79-237">Having a quick look like this is a good sanity check before we start to do any serious work.</span><span class="sxs-lookup"><span data-stu-id="29b79-237">Having a quick look like this is a good sanity check before we start to do any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="29b79-238">First R script</span><span class="sxs-lookup"><span data-stu-id="29b79-238">First R script</span></span>
<span data-ttu-id="29b79-239">Let's create a simple first R script to experiment with in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="29b79-239">Let's create a simple first R script to experiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="29b79-240">I have created and tested the following script in RStudio.</span><span class="sxs-lookup"><span data-stu-id="29b79-240">I have created and tested the following script in RStudio.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="29b79-241">Now I need to transfer this script to Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="29b79-241">Now I need to transfer this script to Azure Machine Learning Studio.</span></span> <span data-ttu-id="29b79-242">I could simply cut and paste.</span><span class="sxs-lookup"><span data-stu-id="29b79-242">I could simply cut and paste.</span></span> <span data-ttu-id="29b79-243">However, in this case, I will transfer my R script via a zip file.</span><span class="sxs-lookup"><span data-stu-id="29b79-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-to-the-execute-r-script-module"></a><span data-ttu-id="29b79-244">Data input to the Execute R Script module</span><span class="sxs-lookup"><span data-stu-id="29b79-244">Data input to the Execute R Script module</span></span>
<span data-ttu-id="29b79-245">Let's have a look at the inputs to the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-245">Let's have a look at the inputs to the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="29b79-246">In this example we will read the California dairy data into the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-246">In this example we will read the California dairy data into the [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="29b79-247">There are three possible inputs for the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-247">There are three possible inputs for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="29b79-248">You may use any one or all of these inputs, depending on your application.</span><span class="sxs-lookup"><span data-stu-id="29b79-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="29b79-249">It is also perfectly reasonable to use an R script that takes no input at all.</span><span class="sxs-lookup"><span data-stu-id="29b79-249">It is also perfectly reasonable to use an R script that takes no input at all.</span></span>  

<span data-ttu-id="29b79-250">Let's look at each of these inputs, going from left to right.</span><span class="sxs-lookup"><span data-stu-id="29b79-250">Let's look at each of these inputs, going from left to right.</span></span> <span data-ttu-id="29b79-251">You can see the names of each of the inputs by placing your cursor over the input and reading the tooltip.</span><span class="sxs-lookup"><span data-stu-id="29b79-251">You can see the names of each of the inputs by placing your cursor over the input and reading the tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="29b79-252">Script Bundle</span><span class="sxs-lookup"><span data-stu-id="29b79-252">Script Bundle</span></span>
<span data-ttu-id="29b79-253">The Script Bundle input allows you to pass the contents of a zip file into [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-253">The Script Bundle input allows you to pass the contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="29b79-254">You can use one of the following commands to read the contents of the zip file into your R code.</span><span class="sxs-lookup"><span data-stu-id="29b79-254">You can use one of the following commands to read the contents of the zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="29b79-255">Azure Machine Learning treats files in the zip as if they are in the src/ directory, so you need to prefix your file names with this directory name.</span><span class="sxs-lookup"><span data-stu-id="29b79-255">Azure Machine Learning treats files in the zip as if they are in the src/ directory, so you need to prefix your file names with this directory name.</span></span> <span data-ttu-id="29b79-256">For example, if the zip contains the files `yourfile.R` and `yourData.rdata` in the root of the zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span><span class="sxs-lookup"><span data-stu-id="29b79-256">For example, if the zip contains the files `yourfile.R` and `yourData.rdata` in the root of the zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="29b79-257">We already discussed loading datasets in [Loading the dataset](#loading).</span><span class="sxs-lookup"><span data-stu-id="29b79-257">We already discussed loading datasets in [Loading the dataset](#loading).</span></span> <span data-ttu-id="29b79-258">Once you have created and tested the R script shown in the previous section, do the following:</span><span class="sxs-lookup"><span data-stu-id="29b79-258">Once you have created and tested the R script shown in the previous section, do the following:</span></span>

1. <span data-ttu-id="29b79-259">Save the R script into a .R file.</span><span class="sxs-lookup"><span data-stu-id="29b79-259">Save the R script into a .R file.</span></span> <span data-ttu-id="29b79-260">I call my script file "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="29b79-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="29b79-261">Here's the contents.</span><span class="sxs-lookup"><span data-stu-id="29b79-261">Here's the contents.</span></span>
   
        ## Only one of the following two lines should be used
        ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
        ## If in RStudio, use the second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## The following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="29b79-262">Create a zip file and copy your script into this zip file.</span><span class="sxs-lookup"><span data-stu-id="29b79-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="29b79-263">On Windows, you can right-click on the file and select **Send to**, and then **Compressed folder**.</span><span class="sxs-lookup"><span data-stu-id="29b79-263">On Windows, you can right-click on the file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="29b79-264">This will create a new zip file containing the "simpleplot.R" file.</span><span class="sxs-lookup"><span data-stu-id="29b79-264">This will create a new zip file containing the "simpleplot.R" file.</span></span>
3. <span data-ttu-id="29b79-265">Add your file to the **datasets** in Machine Learning Studio, specifying the type as **zip**.</span><span class="sxs-lookup"><span data-stu-id="29b79-265">Add your file to the **datasets** in Machine Learning Studio, specifying the type as **zip**.</span></span> <span data-ttu-id="29b79-266">You should now see the zip file in your datasets.</span><span class="sxs-lookup"><span data-stu-id="29b79-266">You should now see the zip file in your datasets.</span></span>
4. <span data-ttu-id="29b79-267">Drag and drop the zip file from **datasets** onto the **ML Studio canvas**.</span><span class="sxs-lookup"><span data-stu-id="29b79-267">Drag and drop the zip file from **datasets** onto the **ML Studio canvas**.</span></span>
5. <span data-ttu-id="29b79-268">Connect the output of the **zip data** icon to the **Script Bundle** input of the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-268">Connect the output of the **zip data** icon to the **Script Bundle** input of the [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="29b79-269">Type the `source()` function with your zip file name into the code window for the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-269">Type the `source()` function with your zip file name into the code window for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="29b79-270">In my case I typed `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="29b79-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="29b79-271">Make sure you click **Save**.</span><span class="sxs-lookup"><span data-stu-id="29b79-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="29b79-272">Once these steps are complete, the [Execute R Script][execute-r-script] module will execute the R script in the zip file when the experiment is run.</span><span class="sxs-lookup"><span data-stu-id="29b79-272">Once these steps are complete, the [Execute R Script][execute-r-script] module will execute the R script in the zip file when the experiment is run.</span></span> <span data-ttu-id="29b79-273">At this point your experiment should look something like Figure 5.</span><span class="sxs-lookup"><span data-stu-id="29b79-273">At this point your experiment should look something like Figure 5.</span></span>

![Experiment using zipped R script][6]

<span data-ttu-id="29b79-275">*Figure 5. Experiment using zipped R script.*</span><span class="sxs-lookup"><span data-stu-id="29b79-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="29b79-276">Dataset1</span><span class="sxs-lookup"><span data-stu-id="29b79-276">Dataset1</span></span>
<span data-ttu-id="29b79-277">You can pass a rectangular table of data to your R code by using the Dataset1 input.</span><span class="sxs-lookup"><span data-stu-id="29b79-277">You can pass a rectangular table of data to your R code by using the Dataset1 input.</span></span> <span data-ttu-id="29b79-278">In our simple script the `maml.mapInputPort(1)` function reads the data from port 1.</span><span class="sxs-lookup"><span data-stu-id="29b79-278">In our simple script the `maml.mapInputPort(1)` function reads the data from port 1.</span></span> <span data-ttu-id="29b79-279">This data is then assigned to a dataframe variable name in your code.</span><span class="sxs-lookup"><span data-stu-id="29b79-279">This data is then assigned to a dataframe variable name in your code.</span></span> <span data-ttu-id="29b79-280">In our simple script the first line of code performs the assignment.</span><span class="sxs-lookup"><span data-stu-id="29b79-280">In our simple script the first line of code performs the assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="29b79-281">Execute your experiment by clicking on the **Run** button.</span><span class="sxs-lookup"><span data-stu-id="29b79-281">Execute your experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="29b79-282">When the execution finishes, click on the [Execute R Script][execute-r-script] module and then click **View output log** on the properties pane.</span><span class="sxs-lookup"><span data-stu-id="29b79-282">When the execution finishes, click on the [Execute R Script][execute-r-script] module and then click **View output log** on the properties pane.</span></span> <span data-ttu-id="29b79-283">A new page should appear in your browser showing the contents of the output.log file.</span><span class="sxs-lookup"><span data-stu-id="29b79-283">A new page should appear in your browser showing the contents of the output.log file.</span></span> <span data-ttu-id="29b79-284">When you scroll down you should see something like the following.</span><span class="sxs-lookup"><span data-stu-id="29b79-284">When you scroll down you should see something like the following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="29b79-285">Farther down the page is more detailed information on the columns, which will look something like the following.</span><span class="sxs-lookup"><span data-stu-id="29b79-285">Farther down the page is more detailed information on the columns, which will look something like the following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="29b79-286">These results are mostly as expected, with 228 observations and 9 columns in the dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-286">These results are mostly as expected, with 228 observations and 9 columns in the dataframe.</span></span> <span data-ttu-id="29b79-287">We can see the column names, the R data type and a sample of each column.</span><span class="sxs-lookup"><span data-stu-id="29b79-287">We can see the column names, the R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="29b79-288">This same printed output is conveniently available from the R Device output of the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-288">This same printed output is conveniently available from the R Device output of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="29b79-289">We will discuss the outputs of the [Execute R Script][execute-r-script] module in the next section.</span><span class="sxs-lookup"><span data-stu-id="29b79-289">We will discuss the outputs of the [Execute R Script][execute-r-script] module in the next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="29b79-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="29b79-290">Dataset2</span></span>
<span data-ttu-id="29b79-291">The behavior of the Dataset2 input is identical to that of Dataset1.</span><span class="sxs-lookup"><span data-stu-id="29b79-291">The behavior of the Dataset2 input is identical to that of Dataset1.</span></span> <span data-ttu-id="29b79-292">Using this input you can pass a second rectangular table of data into your R code.</span><span class="sxs-lookup"><span data-stu-id="29b79-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="29b79-293">The function `maml.mapInputPort(2)`, with the argument 2, is used to pass this data.</span><span class="sxs-lookup"><span data-stu-id="29b79-293">The function `maml.mapInputPort(2)`, with the argument 2, is used to pass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="29b79-294">Execute R Script outputs</span><span class="sxs-lookup"><span data-stu-id="29b79-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="29b79-295">Output a dataframe</span><span class="sxs-lookup"><span data-stu-id="29b79-295">Output a dataframe</span></span>
<span data-ttu-id="29b79-296">You can output the contents of an R dataframe as a rectangular table through the Result Dataset1 port by using the `maml.mapOutputPort()` function.</span><span class="sxs-lookup"><span data-stu-id="29b79-296">You can output the contents of an R dataframe as a rectangular table through the Result Dataset1 port by using the `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="29b79-297">In our simple R script this is performed by the following line.</span><span class="sxs-lookup"><span data-stu-id="29b79-297">In our simple R script this is performed by the following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="29b79-298">After running the experiment, click on the Result Dataset1 output port and then click on **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="29b79-298">After running the experiment, click on the Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="29b79-299">You should see something like Figure 6.</span><span class="sxs-lookup"><span data-stu-id="29b79-299">You should see something like Figure 6.</span></span>

![The visualization of the output of the California dairy data][7]

<span data-ttu-id="29b79-301">*Figure 6. The visualization of the output of the California dairy data.*</span><span class="sxs-lookup"><span data-stu-id="29b79-301">*Figure 6. The visualization of the output of the California dairy data.*</span></span>

<span data-ttu-id="29b79-302">This output looks identical to the input, exactly as we expected.</span><span class="sxs-lookup"><span data-stu-id="29b79-302">This output looks identical to the input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="29b79-303">R Device output</span><span class="sxs-lookup"><span data-stu-id="29b79-303">R Device output</span></span>
<span data-ttu-id="29b79-304">The Device output of the [Execute R Script][execute-r-script] module contains messages and graphics output.</span><span class="sxs-lookup"><span data-stu-id="29b79-304">The Device output of the [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="29b79-305">Both standard output and standard error messages from R are sent to the R Device output port.</span><span class="sxs-lookup"><span data-stu-id="29b79-305">Both standard output and standard error messages from R are sent to the R Device output port.</span></span>  

<span data-ttu-id="29b79-306">To view the R Device output, click on the port and then on **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="29b79-306">To view the R Device output, click on the port and then on **Visualize**.</span></span> <span data-ttu-id="29b79-307">We see the standard output and standard error from the R script in Figure 7.</span><span class="sxs-lookup"><span data-stu-id="29b79-307">We see the standard output and standard error from the R script in Figure 7.</span></span>

![Standard output and standard error from the R Device port][8]

<span data-ttu-id="29b79-309">*Figure 7. Standard output and standard error from the R Device port.*</span><span class="sxs-lookup"><span data-stu-id="29b79-309">*Figure 7. Standard output and standard error from the R Device port.*</span></span>

<span data-ttu-id="29b79-310">Scrolling down we see the graphics output from our R script in Figure 8.</span><span class="sxs-lookup"><span data-stu-id="29b79-310">Scrolling down we see the graphics output from our R script in Figure 8.</span></span>  

![Graphics output from the R Device port][9]

<span data-ttu-id="29b79-312">*Figure 8. Graphics output from the R Device port.*</span><span class="sxs-lookup"><span data-stu-id="29b79-312">*Figure 8. Graphics output from the R Device port.*</span></span>  

## <a id="filtering"></a><span data-ttu-id="29b79-313">Data filtering and transformation</span><span class="sxs-lookup"><span data-stu-id="29b79-313">Data filtering and transformation</span></span>
<span data-ttu-id="29b79-314">In this section we will perform some basic data filtering and transformation operations on the California dairy data.</span><span class="sxs-lookup"><span data-stu-id="29b79-314">In this section we will perform some basic data filtering and transformation operations on the California dairy data.</span></span> <span data-ttu-id="29b79-315">By the end of this section we will have data in a format suitable for building an analytic model.</span><span class="sxs-lookup"><span data-stu-id="29b79-315">By the end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="29b79-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span><span class="sxs-lookup"><span data-stu-id="29b79-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="29b79-317">This background should help you deal with the many variations encountered in real-world problems.</span><span class="sxs-lookup"><span data-stu-id="29b79-317">This background should help you deal with the many variations encountered in real-world problems.</span></span>

<span data-ttu-id="29b79-318">The complete R code for this section is available in the zip file you downloaded earlier.</span><span class="sxs-lookup"><span data-stu-id="29b79-318">The complete R code for this section is available in the zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="29b79-319">Type transformations</span><span class="sxs-lookup"><span data-stu-id="29b79-319">Type transformations</span></span>
<span data-ttu-id="29b79-320">Now that we can read the California dairy data into the R code in the [Execute R Script][execute-r-script] module, we need to ensure that the data in the columns has the intended type and format.</span><span class="sxs-lookup"><span data-stu-id="29b79-320">Now that we can read the California dairy data into the R code in the [Execute R Script][execute-r-script] module, we need to ensure that the data in the columns has the intended type and format.</span></span>  

<span data-ttu-id="29b79-321">R is a dynamically typed language, which means that data types are coerced from one to another as required.</span><span class="sxs-lookup"><span data-stu-id="29b79-321">R is a dynamically typed language, which means that data types are coerced from one to another as required.</span></span> <span data-ttu-id="29b79-322">The atomic data types in R include numeric, logical and character.</span><span class="sxs-lookup"><span data-stu-id="29b79-322">The atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="29b79-323">The factor type is used to compactly store categorical data.</span><span class="sxs-lookup"><span data-stu-id="29b79-323">The factor type is used to compactly store categorical data.</span></span> <span data-ttu-id="29b79-324">You can find much more information on data types in the references in [Appendix B - Further reading](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="29b79-324">You can find much more information on data types in the references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="29b79-325">When tabular data is read into R from an external source, it is always a good idea to check the resulting types in the columns.</span><span class="sxs-lookup"><span data-stu-id="29b79-325">When tabular data is read into R from an external source, it is always a good idea to check the resulting types in the columns.</span></span> <span data-ttu-id="29b79-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span><span class="sxs-lookup"><span data-stu-id="29b79-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="29b79-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span><span class="sxs-lookup"><span data-stu-id="29b79-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="29b79-328">Fortunately, it is easy to convert one type to another, as long as mapping is possible.</span><span class="sxs-lookup"><span data-stu-id="29b79-328">Fortunately, it is easy to convert one type to another, as long as mapping is possible.</span></span> <span data-ttu-id="29b79-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it to a factor (categorical variable).</span><span class="sxs-lookup"><span data-stu-id="29b79-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it to a factor (categorical variable).</span></span> <span data-ttu-id="29b79-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span><span class="sxs-lookup"><span data-stu-id="29b79-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="29b79-331">The syntax for any of these conversions is simple: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="29b79-331">The syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="29b79-332">These type conversion functions include the following.</span><span class="sxs-lookup"><span data-stu-id="29b79-332">These type conversion functions include the following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="29b79-333">Looking at the data types of the columns we input in the previous section: all columns are of type numeric, except for the column labeled 'Month', which is of type character.</span><span class="sxs-lookup"><span data-stu-id="29b79-333">Looking at the data types of the columns we input in the previous section: all columns are of type numeric, except for the column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="29b79-334">Let's convert this to a factor and test the results.</span><span class="sxs-lookup"><span data-stu-id="29b79-334">Let's convert this to a factor and test the results.</span></span>  

<span data-ttu-id="29b79-335">I have deleted the line that created the scatterplot matrix and added a line converting the 'Month' column to a factor.</span><span class="sxs-lookup"><span data-stu-id="29b79-335">I have deleted the line that created the scatterplot matrix and added a line converting the 'Month' column to a factor.</span></span> <span data-ttu-id="29b79-336">In my experiment I will just cut and paste the R code into the code window of the [Execute R Script][execute-r-script] Module.</span><span class="sxs-lookup"><span data-stu-id="29b79-336">In my experiment I will just cut and paste the R code into the code window of the [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="29b79-337">You could also update the zip file and upload it to Azure Machine Learning Studio, but this takes several steps.</span><span class="sxs-lookup"><span data-stu-id="29b79-337">You could also update the zip file and upload it to Azure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check the result
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="29b79-338">Let's execute this code and look at the output log for the R script.</span><span class="sxs-lookup"><span data-stu-id="29b79-338">Let's execute this code and look at the output log for the R script.</span></span> <span data-ttu-id="29b79-339">The relevant data from the log is shown in Figure 9.</span><span class="sxs-lookup"><span data-stu-id="29b79-339">The relevant data from the log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="29b79-340">*Figure 9. Summary of the dataframe with a factor variable.*</span><span class="sxs-lookup"><span data-stu-id="29b79-340">*Figure 9. Summary of the dataframe with a factor variable.*</span></span>

<span data-ttu-id="29b79-341">The type for Month should now say '**Factor w/ 14 levels**'.</span><span class="sxs-lookup"><span data-stu-id="29b79-341">The type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="29b79-342">This is a problem since there are only 12 months in the year.</span><span class="sxs-lookup"><span data-stu-id="29b79-342">This is a problem since there are only 12 months in the year.</span></span> <span data-ttu-id="29b79-343">You can also check to see that the type in **Visualize** of the Result Dataset port is '**Categorical**'.</span><span class="sxs-lookup"><span data-stu-id="29b79-343">You can also check to see that the type in **Visualize** of the Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="29b79-344">The problem is that the 'Month' column has not been coded systematically.</span><span class="sxs-lookup"><span data-stu-id="29b79-344">The problem is that the 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="29b79-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming the string to 3 characters.</span><span class="sxs-lookup"><span data-stu-id="29b79-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming the string to 3 characters.</span></span> <span data-ttu-id="29b79-346">The line of code now looks like the following:</span><span class="sxs-lookup"><span data-stu-id="29b79-346">The line of code now looks like the following:</span></span>

    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="29b79-347">Rerun the experiment and view the output log.</span><span class="sxs-lookup"><span data-stu-id="29b79-347">Rerun the experiment and view the output log.</span></span> <span data-ttu-id="29b79-348">The expected results are shown in Figure 10.</span><span class="sxs-lookup"><span data-stu-id="29b79-348">The expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="29b79-349">*Figure 10. Summary of the dataframe with correct number of factor levels.*</span><span class="sxs-lookup"><span data-stu-id="29b79-349">*Figure 10. Summary of the dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="29b79-350">Our factor variable now has the desired 12 levels.</span><span class="sxs-lookup"><span data-stu-id="29b79-350">Our factor variable now has the desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="29b79-351">Basic data frame filtering</span><span class="sxs-lookup"><span data-stu-id="29b79-351">Basic data frame filtering</span></span>
<span data-ttu-id="29b79-352">R dataframes support powerful filtering capabilities.</span><span class="sxs-lookup"><span data-stu-id="29b79-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="29b79-353">Datasets can be subsetted by using logical filters on either rows or columns.</span><span class="sxs-lookup"><span data-stu-id="29b79-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="29b79-354">In many cases, complex filter criteria will be required.</span><span class="sxs-lookup"><span data-stu-id="29b79-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="29b79-355">The references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span><span class="sxs-lookup"><span data-stu-id="29b79-355">The references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="29b79-356">There is one bit of filtering we should do on our dataset.</span><span class="sxs-lookup"><span data-stu-id="29b79-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="29b79-357">If you look at the columns in the cadairydata dataframe, you will see two unnecessary columns.</span><span class="sxs-lookup"><span data-stu-id="29b79-357">If you look at the columns in the cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="29b79-358">The first column just holds a row number, which is not very useful.</span><span class="sxs-lookup"><span data-stu-id="29b79-358">The first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="29b79-359">The second column, Year.Month, contains redundant information.</span><span class="sxs-lookup"><span data-stu-id="29b79-359">The second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="29b79-360">We can easily exclude these columns by using the following R code.</span><span class="sxs-lookup"><span data-stu-id="29b79-360">We can easily exclude these columns by using the following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="29b79-361">From now on in this section, I will just show you the additional code I am adding in the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-361">From now on in this section, I will just show you the additional code I am adding in the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="29b79-362">I will add each new line **before** the `str()` function.</span><span class="sxs-lookup"><span data-stu-id="29b79-362">I will add each new line **before** the `str()` function.</span></span> <span data-ttu-id="29b79-363">I use this function to verify my results in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="29b79-363">I use this function to verify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="29b79-364">I add the following line to my R code in the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-364">I add the following line to my R code in the [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="29b79-365">Run this code in your experiment and check the result from the output log.</span><span class="sxs-lookup"><span data-stu-id="29b79-365">Run this code in your experiment and check the result from the output log.</span></span> <span data-ttu-id="29b79-366">These results are shown in Figure 11.</span><span class="sxs-lookup"><span data-stu-id="29b79-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="29b79-367">*Figure 11. Summary of the dataframe with two columns removed.*</span><span class="sxs-lookup"><span data-stu-id="29b79-367">*Figure 11. Summary of the dataframe with two columns removed.*</span></span>

<span data-ttu-id="29b79-368">Good news!</span><span class="sxs-lookup"><span data-stu-id="29b79-368">Good news!</span></span> <span data-ttu-id="29b79-369">We get the expected results.</span><span class="sxs-lookup"><span data-stu-id="29b79-369">We get the expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="29b79-370">Add a new column</span><span class="sxs-lookup"><span data-stu-id="29b79-370">Add a new column</span></span>
<span data-ttu-id="29b79-371">To create time series models it will be convenient to have a column containing the months since the start of the time series.</span><span class="sxs-lookup"><span data-stu-id="29b79-371">To create time series models it will be convenient to have a column containing the months since the start of the time series.</span></span> <span data-ttu-id="29b79-372">We will create a new column 'Month.Count'.</span><span class="sxs-lookup"><span data-stu-id="29b79-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="29b79-373">To help organize the code we will create our first simple function, `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="29b79-373">To help organize the code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="29b79-374">We will then apply this function to create a new column in the dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-374">We will then apply this function to create a new column in the dataframe.</span></span> <span data-ttu-id="29b79-375">The new code is as follows.</span><span class="sxs-lookup"><span data-stu-id="29b79-375">The new code is as follows.</span></span>

    ## Create a new column with the month count
    ## Function to find the number of months from the first
    ## month of the time series
    num.month <- function(Year, Month) {
      ## Find the starting year
      min.year  <- min(Year)

      ## Compute the number of months from the start of the time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute the new column for the dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="29b79-376">Now run the updated experiment and use the output log to view the results.</span><span class="sxs-lookup"><span data-stu-id="29b79-376">Now run the updated experiment and use the output log to view the results.</span></span> <span data-ttu-id="29b79-377">These results are shown in Figure 12.</span><span class="sxs-lookup"><span data-stu-id="29b79-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="29b79-378">*Figure 12. Summary of the dataframe with the additional column.*</span><span class="sxs-lookup"><span data-stu-id="29b79-378">*Figure 12. Summary of the dataframe with the additional column.*</span></span>

<span data-ttu-id="29b79-379">It looks like everything is working.</span><span class="sxs-lookup"><span data-stu-id="29b79-379">It looks like everything is working.</span></span> <span data-ttu-id="29b79-380">We have the new column with the expected values in our dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-380">We have the new column with the expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="29b79-381">Value transformations</span><span class="sxs-lookup"><span data-stu-id="29b79-381">Value transformations</span></span>
<span data-ttu-id="29b79-382">In this section we will perform some simple transformations on the values in some of the columns of our dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-382">In this section we will perform some simple transformations on the values in some of the columns of our dataframe.</span></span> <span data-ttu-id="29b79-383">The R language supports nearly arbitrary value transformations.</span><span class="sxs-lookup"><span data-stu-id="29b79-383">The R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="29b79-384">The references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span><span class="sxs-lookup"><span data-stu-id="29b79-384">The references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="29b79-385">If you look at the values in the summaries of our dataframe you should see something odd here.</span><span class="sxs-lookup"><span data-stu-id="29b79-385">If you look at the values in the summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="29b79-386">Is more ice cream than milk produced in California?</span><span class="sxs-lookup"><span data-stu-id="29b79-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="29b79-387">No, of course not, as this makes no sense, sad as this fact may be to some of us ice cream lovers.</span><span class="sxs-lookup"><span data-stu-id="29b79-387">No, of course not, as this makes no sense, sad as this fact may be to some of us ice cream lovers.</span></span> <span data-ttu-id="29b79-388">The units are different.</span><span class="sxs-lookup"><span data-stu-id="29b79-388">The units are different.</span></span> <span data-ttu-id="29b79-389">The price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span><span class="sxs-lookup"><span data-stu-id="29b79-389">The price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="29b79-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do the multiplication to convert these values so they are all in equal units of 1,000 pounds.</span><span class="sxs-lookup"><span data-stu-id="29b79-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do the multiplication to convert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="29b79-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span><span class="sxs-lookup"><span data-stu-id="29b79-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="29b79-392">A log transformation allows us to use a linear model, simplifying this process.</span><span class="sxs-lookup"><span data-stu-id="29b79-392">A log transformation allows us to use a linear model, simplifying this process.</span></span> <span data-ttu-id="29b79-393">We can apply the log transformation in the same function where the multiplier is applied.</span><span class="sxs-lookup"><span data-stu-id="29b79-393">We can apply the log transformation in the same function where the multiplier is applied.</span></span>

<span data-ttu-id="29b79-394">In the following code, I define a new function, `log.transform()`, and apply it to the rows containing the numerical values.</span><span class="sxs-lookup"><span data-stu-id="29b79-394">In the following code, I define a new function, `log.transform()`, and apply it to the rows containing the numerical values.</span></span> <span data-ttu-id="29b79-395">The R `Map()` function is used to apply the `log.transform()` function to the selected columns of the dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-395">The R `Map()` function is used to apply the `log.transform()` function to the selected columns of the dataframe.</span></span> <span data-ttu-id="29b79-396">`Map()` is similar to `apply()` but allows for more than one list of arguments to the function.</span><span class="sxs-lookup"><span data-stu-id="29b79-396">`Map()` is similar to `apply()` but allows for more than one list of arguments to the function.</span></span> <span data-ttu-id="29b79-397">Note that a list of multipliers supplies the second argument to the `log.transform()` function.</span><span class="sxs-lookup"><span data-stu-id="29b79-397">Note that a list of multipliers supplies the second argument to the `log.transform()` function.</span></span> <span data-ttu-id="29b79-398">The `na.omit()` function is used as a bit of cleanup to ensure we do not have missing or undefined values in the dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-398">The `na.omit()` function is used as a bit of cleanup to ensure we do not have missing or undefined values in the dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for the transformation, which is the log
      ## of the input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments to function log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier to funcition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check the input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap the multiplication in tryCatch
      ## If there is an exception, print the warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply the transformation function to the 4 columns
    ## of the dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="29b79-399">There is quite a bit happening in the `log.transform()` function.</span><span class="sxs-lookup"><span data-stu-id="29b79-399">There is quite a bit happening in the `log.transform()` function.</span></span> <span data-ttu-id="29b79-400">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span><span class="sxs-lookup"><span data-stu-id="29b79-400">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="29b79-401">Only a few lines of this code actually do the computations.</span><span class="sxs-lookup"><span data-stu-id="29b79-401">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="29b79-402">The goal of the defensive programming is to prevent the failure of a single function that prevents processing from continuing.</span><span class="sxs-lookup"><span data-stu-id="29b79-402">The goal of the defensive programming is to prevent the failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="29b79-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span><span class="sxs-lookup"><span data-stu-id="29b79-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="29b79-404">To avoid this situation, default return values must be chosen that will limit damage to downstream processing.</span><span class="sxs-lookup"><span data-stu-id="29b79-404">To avoid this situation, default return values must be chosen that will limit damage to downstream processing.</span></span> <span data-ttu-id="29b79-405">A message is also produced to alert users that something has gone wrong.</span><span class="sxs-lookup"><span data-stu-id="29b79-405">A message is also produced to alert users that something has gone wrong.</span></span>

<span data-ttu-id="29b79-406">If you are not used to defensive programming in R, all this code may seem a bit overwhelming.</span><span class="sxs-lookup"><span data-stu-id="29b79-406">If you are not used to defensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="29b79-407">I will walk you through the major steps:</span><span class="sxs-lookup"><span data-stu-id="29b79-407">I will walk you through the major steps:</span></span>

1. <span data-ttu-id="29b79-408">A vector of four messages is defined.</span><span class="sxs-lookup"><span data-stu-id="29b79-408">A vector of four messages is defined.</span></span> <span data-ttu-id="29b79-409">These messages are used to communicate information about some of the possible errors and exceptions that can occur with this code.</span><span class="sxs-lookup"><span data-stu-id="29b79-409">These messages are used to communicate information about some of the possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="29b79-410">I return a value of NA for each case.</span><span class="sxs-lookup"><span data-stu-id="29b79-410">I return a value of NA for each case.</span></span> <span data-ttu-id="29b79-411">There are many other possibilities that might have fewer side effects.</span><span class="sxs-lookup"><span data-stu-id="29b79-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="29b79-412">I could return a vector of zeroes, or the original input vector, for example.</span><span class="sxs-lookup"><span data-stu-id="29b79-412">I could return a vector of zeroes, or the original input vector, for example.</span></span>
3. <span data-ttu-id="29b79-413">Checks are run on the arguments to the function.</span><span class="sxs-lookup"><span data-stu-id="29b79-413">Checks are run on the arguments to the function.</span></span> <span data-ttu-id="29b79-414">In each case, if an error is detected, a default value is returned and a message is produced by the `warning()` function.</span><span class="sxs-lookup"><span data-stu-id="29b79-414">In each case, if an error is detected, a default value is returned and a message is produced by the `warning()` function.</span></span> <span data-ttu-id="29b79-415">I am using `warning()` rather than `stop()` as the latter will terminate execution, exactly what I am trying to avoid.</span><span class="sxs-lookup"><span data-stu-id="29b79-415">I am using `warning()` rather than `stop()` as the latter will terminate execution, exactly what I am trying to avoid.</span></span> <span data-ttu-id="29b79-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span><span class="sxs-lookup"><span data-stu-id="29b79-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="29b79-417">The log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt to processing.</span><span class="sxs-lookup"><span data-stu-id="29b79-417">The log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt to processing.</span></span> <span data-ttu-id="29b79-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span><span class="sxs-lookup"><span data-stu-id="29b79-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="29b79-419">Execute this R code in your experiment and have a look at the printed output in the output.log file.</span><span class="sxs-lookup"><span data-stu-id="29b79-419">Execute this R code in your experiment and have a look at the printed output in the output.log file.</span></span> <span data-ttu-id="29b79-420">You will now see the transformed values of the four columns in the log, as shown in Figure 13.</span><span class="sxs-lookup"><span data-stu-id="29b79-420">You will now see the transformed values of the four columns in the log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="29b79-421">*Figure 13. Summary of the transformed values in the dataframe.*</span><span class="sxs-lookup"><span data-stu-id="29b79-421">*Figure 13. Summary of the transformed values in the dataframe.*</span></span>

<span data-ttu-id="29b79-422">We see the values have been transformed.</span><span class="sxs-lookup"><span data-stu-id="29b79-422">We see the values have been transformed.</span></span> <span data-ttu-id="29b79-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span><span class="sxs-lookup"><span data-stu-id="29b79-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="29b79-424">At this point our data is cleaned up and we are ready for some modeling.</span><span class="sxs-lookup"><span data-stu-id="29b79-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="29b79-425">Looking at the visualization summary for the Result Dataset output of our [Execute R Script][execute-r-script] module, you will see the 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span><span class="sxs-lookup"><span data-stu-id="29b79-425">Looking at the visualization summary for the Result Dataset output of our [Execute R Script][execute-r-script] module, you will see the 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <a id="timeseries"></a><span data-ttu-id="29b79-426">Time series objects and correlation analysis</span><span class="sxs-lookup"><span data-stu-id="29b79-426">Time series objects and correlation analysis</span></span>
<span data-ttu-id="29b79-427">In this section we will explore a few basic R time series objects and analyze the correlations between some of the variables.</span><span class="sxs-lookup"><span data-stu-id="29b79-427">In this section we will explore a few basic R time series objects and analyze the correlations between some of the variables.</span></span> <span data-ttu-id="29b79-428">Our goal is to output a dataframe containing the pairwise correlation information at several lags.</span><span class="sxs-lookup"><span data-stu-id="29b79-428">Our goal is to output a dataframe containing the pairwise correlation information at several lags.</span></span>

<span data-ttu-id="29b79-429">The complete R code for this section is in the zip file you downloaded earlier.</span><span class="sxs-lookup"><span data-stu-id="29b79-429">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="29b79-430">Time series objects in R</span><span class="sxs-lookup"><span data-stu-id="29b79-430">Time series objects in R</span></span>
<span data-ttu-id="29b79-431">As already mentioned, time series are a series of data values indexed by time.</span><span class="sxs-lookup"><span data-stu-id="29b79-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="29b79-432">R time series objects are used to create and manage the time index.</span><span class="sxs-lookup"><span data-stu-id="29b79-432">R time series objects are used to create and manage the time index.</span></span> <span data-ttu-id="29b79-433">There are several advantages to using time series objects.</span><span class="sxs-lookup"><span data-stu-id="29b79-433">There are several advantages to using time series objects.</span></span> <span data-ttu-id="29b79-434">Time series objects free you from the many details of managing the time series index values that are encapsulated in the object.</span><span class="sxs-lookup"><span data-stu-id="29b79-434">Time series objects free you from the many details of managing the time series index values that are encapsulated in the object.</span></span> <span data-ttu-id="29b79-435">In addition, time series objects allow you to use the many time series methods for plotting, printing, modeling, etc.</span><span class="sxs-lookup"><span data-stu-id="29b79-435">In addition, time series objects allow you to use the many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="29b79-436">The POSIXct time series class is commonly used and is relatively simple.</span><span class="sxs-lookup"><span data-stu-id="29b79-436">The POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="29b79-437">This time series class measures time from the start of the epoch, January 1, 1970.</span><span class="sxs-lookup"><span data-stu-id="29b79-437">This time series class measures time from the start of the epoch, January 1, 1970.</span></span> <span data-ttu-id="29b79-438">We will use POSIXct time series objects in this example.</span><span class="sxs-lookup"><span data-stu-id="29b79-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="29b79-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span><span class="sxs-lookup"><span data-stu-id="29b79-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in the references in Section 5.7. [commenting because this section doesn't exist, even in the original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="29b79-440">Time series object example</span><span class="sxs-lookup"><span data-stu-id="29b79-440">Time series object example</span></span>
<span data-ttu-id="29b79-441">Let's get started with our example.</span><span class="sxs-lookup"><span data-stu-id="29b79-441">Let's get started with our example.</span></span> <span data-ttu-id="29b79-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span><span class="sxs-lookup"><span data-stu-id="29b79-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="29b79-443">Connect the Result Dataset1 output port of the existing [Execute R Script][execute-r-script] module to the Dataset1 input port of the new [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="29b79-443">Connect the Result Dataset1 output port of the existing [Execute R Script][execute-r-script] module to the Dataset1 input port of the new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="29b79-444">As I did for the first examples, as we progress through the example, at some points I will show only the incremental additional lines of R code at each step.</span><span class="sxs-lookup"><span data-stu-id="29b79-444">As I did for the first examples, as we progress through the example, at some points I will show only the incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-the-dataframe"></a><span data-ttu-id="29b79-445">Reading the dataframe</span><span class="sxs-lookup"><span data-stu-id="29b79-445">Reading the dataframe</span></span>
<span data-ttu-id="29b79-446">As a first step, let's read in a dataframe and make sure we get the expected results.</span><span class="sxs-lookup"><span data-stu-id="29b79-446">As a first step, let's read in a dataframe and make sure we get the expected results.</span></span> <span data-ttu-id="29b79-447">The following code should do the job.</span><span class="sxs-lookup"><span data-stu-id="29b79-447">The following code should do the job.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check the results

<span data-ttu-id="29b79-448">Now, run the experiment.</span><span class="sxs-lookup"><span data-stu-id="29b79-448">Now, run the experiment.</span></span> <span data-ttu-id="29b79-449">The log of the new Execute R Script shape should look like Figure 14.</span><span class="sxs-lookup"><span data-stu-id="29b79-449">The log of the new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="29b79-450">*Figure 14. Summary of the dataframe in the Execute R Script module.*</span><span class="sxs-lookup"><span data-stu-id="29b79-450">*Figure 14. Summary of the dataframe in the Execute R Script module.*</span></span>

<span data-ttu-id="29b79-451">This data is of the expected types and format.</span><span class="sxs-lookup"><span data-stu-id="29b79-451">This data is of the expected types and format.</span></span> <span data-ttu-id="29b79-452">Note that the 'Month' column is of type factor and has the expected number of levels.</span><span class="sxs-lookup"><span data-stu-id="29b79-452">Note that the 'Month' column is of type factor and has the expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="29b79-453">Creating a time series object</span><span class="sxs-lookup"><span data-stu-id="29b79-453">Creating a time series object</span></span>
<span data-ttu-id="29b79-454">We need to add a time series object to our dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-454">We need to add a time series object to our dataframe.</span></span> <span data-ttu-id="29b79-455">Replace the current code with the following, which adds a new column of class POSIXct.</span><span class="sxs-lookup"><span data-stu-id="29b79-455">Replace the current code with the following, which adds a new column of class POSIXct.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check the results

<span data-ttu-id="29b79-456">Now, check the log.</span><span class="sxs-lookup"><span data-stu-id="29b79-456">Now, check the log.</span></span> <span data-ttu-id="29b79-457">It should look like Figure 15.</span><span class="sxs-lookup"><span data-stu-id="29b79-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="29b79-458">*Figure 15. Summary of the dataframe with a time series object.*</span><span class="sxs-lookup"><span data-stu-id="29b79-458">*Figure 15. Summary of the dataframe with a time series object.*</span></span>

<span data-ttu-id="29b79-459">We can see from the summary that the new column is in fact of class POSIXct.</span><span class="sxs-lookup"><span data-stu-id="29b79-459">We can see from the summary that the new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-the-data"></a><span data-ttu-id="29b79-460">Exploring and transforming the data</span><span class="sxs-lookup"><span data-stu-id="29b79-460">Exploring and transforming the data</span></span>
<span data-ttu-id="29b79-461">Let's explore some of the variables in this dataset.</span><span class="sxs-lookup"><span data-stu-id="29b79-461">Let's explore some of the variables in this dataset.</span></span> <span data-ttu-id="29b79-462">A scatterplot matrix is a good way to produce a quick look.</span><span class="sxs-lookup"><span data-stu-id="29b79-462">A scatterplot matrix is a good way to produce a quick look.</span></span> <span data-ttu-id="29b79-463">I am replacing the `str()` function in the previous R code with the following line.</span><span class="sxs-lookup"><span data-stu-id="29b79-463">I am replacing the `str()` function in the previous R code with the following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="29b79-464">Run this code and see what happens.</span><span class="sxs-lookup"><span data-stu-id="29b79-464">Run this code and see what happens.</span></span> <span data-ttu-id="29b79-465">The plot produced at the R Device port should look like Figure 16.</span><span class="sxs-lookup"><span data-stu-id="29b79-465">The plot produced at the R Device port should look like Figure 16.</span></span>

![Scatterplot matrix of selected variables][17]

<span data-ttu-id="29b79-467">*Figure 16. Scatterplot matrix of selected variables.*</span><span class="sxs-lookup"><span data-stu-id="29b79-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="29b79-468">There is some odd-looking structure in the relationships between these variables.</span><span class="sxs-lookup"><span data-stu-id="29b79-468">There is some odd-looking structure in the relationships between these variables.</span></span> <span data-ttu-id="29b79-469">Perhaps this arises from trends in the data and from the fact that we have not standardized the variables.</span><span class="sxs-lookup"><span data-stu-id="29b79-469">Perhaps this arises from trends in the data and from the fact that we have not standardized the variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="29b79-470">Correlation analysis</span><span class="sxs-lookup"><span data-stu-id="29b79-470">Correlation analysis</span></span>
<span data-ttu-id="29b79-471">To perform correlation analysis we need to both de-trend and standardize the variables.</span><span class="sxs-lookup"><span data-stu-id="29b79-471">To perform correlation analysis we need to both de-trend and standardize the variables.</span></span> <span data-ttu-id="29b79-472">We could simply use the R `scale()` function, which both centers and scales variables.</span><span class="sxs-lookup"><span data-stu-id="29b79-472">We could simply use the R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="29b79-473">This function might well run faster.</span><span class="sxs-lookup"><span data-stu-id="29b79-473">This function might well run faster.</span></span> <span data-ttu-id="29b79-474">However, I want to show you an example of defensive programing in R.</span><span class="sxs-lookup"><span data-stu-id="29b79-474">However, I want to show you an example of defensive programing in R.</span></span>

<span data-ttu-id="29b79-475">The `ts.detrend()` function shown below performs both of these operations.</span><span class="sxs-lookup"><span data-stu-id="29b79-475">The `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="29b79-476">The following two lines of code de-trend the data and then standardize the values.</span><span class="sxs-lookup"><span data-stu-id="29b79-476">The following two lines of code de-trend the data and then standardize the values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function to de-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time to have the same length',
                    'ERROR: ts.detrend requires argument ts to be of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros to return as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # The input arguments are not of the same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If the ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If the ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that the Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend the time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply the detrend.ts function to the variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot the results to look at the relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="29b79-477">There is quite a bit happening in the `ts.detrend()` function.</span><span class="sxs-lookup"><span data-stu-id="29b79-477">There is quite a bit happening in the `ts.detrend()` function.</span></span> <span data-ttu-id="29b79-478">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span><span class="sxs-lookup"><span data-stu-id="29b79-478">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="29b79-479">Only a few lines of this code actually do the computations.</span><span class="sxs-lookup"><span data-stu-id="29b79-479">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="29b79-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="29b79-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="29b79-481">Both computation blocks are wrapped in `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="29b79-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="29b79-482">For some errors it makes sense to return the original input vector, and in other cases, I return a vector of zeros.</span><span class="sxs-lookup"><span data-stu-id="29b79-482">For some errors it makes sense to return the original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="29b79-483">Note that the linear regression used for de-trending is a time series regression.</span><span class="sxs-lookup"><span data-stu-id="29b79-483">Note that the linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="29b79-484">The predictor variable is a time series object.</span><span class="sxs-lookup"><span data-stu-id="29b79-484">The predictor variable is a time series object.</span></span>  

<span data-ttu-id="29b79-485">Once `ts.detrend()` is defined we apply it to the variables of interest in our dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-485">Once `ts.detrend()` is defined we apply it to the variables of interest in our dataframe.</span></span> <span data-ttu-id="29b79-486">We must coerce the resulting list created by `lapply()` to data dataframe by using `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="29b79-486">We must coerce the resulting list created by `lapply()` to data dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="29b79-487">Because of defensive aspects of `ts.detrend()`, failure to process one of the variables will not prevent correct processing of the others.</span><span class="sxs-lookup"><span data-stu-id="29b79-487">Because of defensive aspects of `ts.detrend()`, failure to process one of the variables will not prevent correct processing of the others.</span></span>  

<span data-ttu-id="29b79-488">The final line of code creates a pairwise scatterplot.</span><span class="sxs-lookup"><span data-stu-id="29b79-488">The final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="29b79-489">After running the R code, the results of the scatterplot are shown in Figure 17.</span><span class="sxs-lookup"><span data-stu-id="29b79-489">After running the R code, the results of the scatterplot are shown in Figure 17.</span></span>

![Pairwise scatterplot of de-trended and standardized time series][18]

<span data-ttu-id="29b79-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span><span class="sxs-lookup"><span data-stu-id="29b79-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="29b79-492">You can compare these results to those shown in Figure 16.</span><span class="sxs-lookup"><span data-stu-id="29b79-492">You can compare these results to those shown in Figure 16.</span></span> <span data-ttu-id="29b79-493">With the trend removed and the variables standardized, we see a lot less structure in the relationships between these variables.</span><span class="sxs-lookup"><span data-stu-id="29b79-493">With the trend removed and the variables standardized, we see a lot less structure in the relationships between these variables.</span></span>

<span data-ttu-id="29b79-494">The code to compute the correlations as R ccf objects is as follows.</span><span class="sxs-lookup"><span data-stu-id="29b79-494">The code to compute the correlations as R ccf objects is as follows.</span></span>

    ## A function to compute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of the pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute the list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="29b79-495">Running this code produces the log shown in Figure 18.</span><span class="sxs-lookup"><span data-stu-id="29b79-495">Running this code produces the log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="29b79-496">*Figure 18. List of ccf objects from the pairwise correlation analysis.*</span><span class="sxs-lookup"><span data-stu-id="29b79-496">*Figure 18. List of ccf objects from the pairwise correlation analysis.*</span></span>

<span data-ttu-id="29b79-497">There is a correlation value for each lag.</span><span class="sxs-lookup"><span data-stu-id="29b79-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="29b79-498">None of these correlation values is large enough to be significant.</span><span class="sxs-lookup"><span data-stu-id="29b79-498">None of these correlation values is large enough to be significant.</span></span> <span data-ttu-id="29b79-499">We can therefore conclude that we can model each variable independently.</span><span class="sxs-lookup"><span data-stu-id="29b79-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="29b79-500">Output a dataframe</span><span class="sxs-lookup"><span data-stu-id="29b79-500">Output a dataframe</span></span>
<span data-ttu-id="29b79-501">We have computed the pairwise correlations as a list of R ccf objects.</span><span class="sxs-lookup"><span data-stu-id="29b79-501">We have computed the pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="29b79-502">This presents a bit of a problem as the Result Dataset output port really requires a dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-502">This presents a bit of a problem as the Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="29b79-503">Further, the ccf object is itself a list and we want only the values in the first element of this list, the correlations at the various lags.</span><span class="sxs-lookup"><span data-stu-id="29b79-503">Further, the ccf object is itself a list and we want only the values in the first element of this list, the correlations at the various lags.</span></span>

<span data-ttu-id="29b79-504">The following code extracts the lag values from the list of ccf objects, which are themselves lists.</span><span class="sxs-lookup"><span data-stu-id="29b79-504">The following code extracts the lag values from the list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with the row names column and the
    ## correlation data frame and assign the column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## The following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="29b79-505">The first line of code is a bit tricky, and some explanation may help you understand it.</span><span class="sxs-lookup"><span data-stu-id="29b79-505">The first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="29b79-506">Working from the inside out we have the following:</span><span class="sxs-lookup"><span data-stu-id="29b79-506">Working from the inside out we have the following:</span></span>

1. <span data-ttu-id="29b79-507">The '**[[**' operator with the argument '**1**' selects the vector of correlations at the lags from the first element of the ccf object list.</span><span class="sxs-lookup"><span data-stu-id="29b79-507">The '**[[**' operator with the argument '**1**' selects the vector of correlations at the lags from the first element of the ccf object list.</span></span>
2. <span data-ttu-id="29b79-508">The `do.call()` function applies the `rbind()` function over the elements of the list returns by `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="29b79-508">The `do.call()` function applies the `rbind()` function over the elements of the list returns by `lapply()`.</span></span>
3. <span data-ttu-id="29b79-509">The `data.frame()` function coerces the result produced by `do.call()` to a dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-509">The `data.frame()` function coerces the result produced by `do.call()` to a dataframe.</span></span>

<span data-ttu-id="29b79-510">Note that the row names are in a column of the dataframe.</span><span class="sxs-lookup"><span data-stu-id="29b79-510">Note that the row names are in a column of the dataframe.</span></span> <span data-ttu-id="29b79-511">Doing so preserves the row names when they are output from the [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="29b79-511">Doing so preserves the row names when they are output from the [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="29b79-512">Running the code produces the output shown in Figure 19 when I **Visualize** the output at the Result Dataset port.</span><span class="sxs-lookup"><span data-stu-id="29b79-512">Running the code produces the output shown in Figure 19 when I **Visualize** the output at the Result Dataset port.</span></span> <span data-ttu-id="29b79-513">The row names are in the first column, as intended.</span><span class="sxs-lookup"><span data-stu-id="29b79-513">The row names are in the first column, as intended.</span></span>

![Results output from the correlation analysis][20]

<span data-ttu-id="29b79-515">*Figure 19. Results output from the correlation analysis.*</span><span class="sxs-lookup"><span data-stu-id="29b79-515">*Figure 19. Results output from the correlation analysis.*</span></span>

## <a id="seasonalforecasting"></a><span data-ttu-id="29b79-516">Time series example: seasonal forecasting</span><span class="sxs-lookup"><span data-stu-id="29b79-516">Time series example: seasonal forecasting</span></span>
<span data-ttu-id="29b79-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between the variables.</span><span class="sxs-lookup"><span data-stu-id="29b79-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between the variables.</span></span> <span data-ttu-id="29b79-518">Let's move on and create a time series forecasting model.</span><span class="sxs-lookup"><span data-stu-id="29b79-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="29b79-519">Using this model we will forecast California milk production for the 12 months of 2013.</span><span class="sxs-lookup"><span data-stu-id="29b79-519">Using this model we will forecast California milk production for the 12 months of 2013.</span></span>

<span data-ttu-id="29b79-520">Our forecasting model will have two components, a trend component and a seasonal component.</span><span class="sxs-lookup"><span data-stu-id="29b79-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="29b79-521">The complete forecast is the product of these two components.</span><span class="sxs-lookup"><span data-stu-id="29b79-521">The complete forecast is the product of these two components.</span></span> <span data-ttu-id="29b79-522">This type of model is known as a multiplicative model.</span><span class="sxs-lookup"><span data-stu-id="29b79-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="29b79-523">The alternative is an additive model.</span><span class="sxs-lookup"><span data-stu-id="29b79-523">The alternative is an additive model.</span></span> <span data-ttu-id="29b79-524">We have already applied a log transformation to the variables of interest, which makes this analysis tractable.</span><span class="sxs-lookup"><span data-stu-id="29b79-524">We have already applied a log transformation to the variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="29b79-525">The complete R code for this section is in the zip file you downloaded earlier.</span><span class="sxs-lookup"><span data-stu-id="29b79-525">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="creating-the-dataframe-for-analysis"></a><span data-ttu-id="29b79-526">Creating the dataframe for analysis</span><span class="sxs-lookup"><span data-stu-id="29b79-526">Creating the dataframe for analysis</span></span>
<span data-ttu-id="29b79-527">Start by adding a **new** [Execute R Script][execute-r-script] module to your experiment.</span><span class="sxs-lookup"><span data-stu-id="29b79-527">Start by adding a **new** [Execute R Script][execute-r-script] module to your experiment.</span></span> <span data-ttu-id="29b79-528">Connect the **Result Dataset** output of the existing [Execute R Script][execute-r-script] module to the **Dataset1** input of the new module.</span><span class="sxs-lookup"><span data-stu-id="29b79-528">Connect the **Result Dataset** output of the existing [Execute R Script][execute-r-script] module to the **Dataset1** input of the new module.</span></span> <span data-ttu-id="29b79-529">The result should look something like Figure 20.</span><span class="sxs-lookup"><span data-stu-id="29b79-529">The result should look something like Figure 20.</span></span>

![The experiment with the new Execute R Script module added][21]

<span data-ttu-id="29b79-531">*Figure 20. The experiment with the new Execute R Script module added.*</span><span class="sxs-lookup"><span data-stu-id="29b79-531">*Figure 20. The experiment with the new Execute R Script module added.*</span></span>

<span data-ttu-id="29b79-532">As with the correlation analysis we just completed, we need to add a column with a POSIXct time series object.</span><span class="sxs-lookup"><span data-stu-id="29b79-532">As with the correlation analysis we just completed, we need to add a column with a POSIXct time series object.</span></span> <span data-ttu-id="29b79-533">The following code will do just this.</span><span class="sxs-lookup"><span data-stu-id="29b79-533">The following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment the first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="29b79-534">Run this code and look at the log.</span><span class="sxs-lookup"><span data-stu-id="29b79-534">Run this code and look at the log.</span></span> <span data-ttu-id="29b79-535">The result should look like Figure 21.</span><span class="sxs-lookup"><span data-stu-id="29b79-535">The result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="29b79-536">*Figure 21. A summary of the dataframe.*</span><span class="sxs-lookup"><span data-stu-id="29b79-536">*Figure 21. A summary of the dataframe.*</span></span>

<span data-ttu-id="29b79-537">With this result, we are ready to start our analysis.</span><span class="sxs-lookup"><span data-stu-id="29b79-537">With this result, we are ready to start our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="29b79-538">Create a training dataset</span><span class="sxs-lookup"><span data-stu-id="29b79-538">Create a training dataset</span></span>
<span data-ttu-id="29b79-539">With the dataframe constructed we need to create a training dataset.</span><span class="sxs-lookup"><span data-stu-id="29b79-539">With the dataframe constructed we need to create a training dataset.</span></span> <span data-ttu-id="29b79-540">This data will include all of the observations except the last 12, of the year 2013, which is our test dataset.</span><span class="sxs-lookup"><span data-stu-id="29b79-540">This data will include all of the observations except the last 12, of the year 2013, which is our test dataset.</span></span> <span data-ttu-id="29b79-541">The following code subsets the dataframe and creates plots of the dairy production and price variables.</span><span class="sxs-lookup"><span data-stu-id="29b79-541">The following code subsets the dataframe and creates plots of the dairy production and price variables.</span></span> <span data-ttu-id="29b79-542">I then create plots of the four production and price variables.</span><span class="sxs-lookup"><span data-stu-id="29b79-542">I then create plots of the four production and price variables.</span></span> <span data-ttu-id="29b79-543">An anonymous function is used to define some augments for plot, and then iterate over the list of the other two arguments with `Map()`.</span><span class="sxs-lookup"><span data-stu-id="29b79-543">An anonymous function is used to define some augments for plot, and then iterate over the list of the other two arguments with `Map()`.</span></span> <span data-ttu-id="29b79-544">If you are thinking that a for loop would have worked fine here, you are correct.</span><span class="sxs-lookup"><span data-stu-id="29b79-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="29b79-545">But, since R is a functional language I am showing you a functional approach.</span><span class="sxs-lookup"><span data-stu-id="29b79-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="29b79-546">Running the code produces the series of time series plots from the R Device output shown in Figure 22.</span><span class="sxs-lookup"><span data-stu-id="29b79-546">Running the code produces the series of time series plots from the R Device output shown in Figure 22.</span></span> <span data-ttu-id="29b79-547">Note that the time axis is in units of dates, a nice benefit of the time series plot method.</span><span class="sxs-lookup"><span data-stu-id="29b79-547">Note that the time axis is in units of dates, a nice benefit of the time series plot method.</span></span>

![First of time series plots of California dairy production and price data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Second of time series plots of California dairy production and price data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Third of time series plots of California dairy production and price data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Fourth of time series plots of California dairy production and price data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="29b79-552">*Figure 22. Time series plots of California dairy production and price data.*</span><span class="sxs-lookup"><span data-stu-id="29b79-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="29b79-553">A trend model</span><span class="sxs-lookup"><span data-stu-id="29b79-553">A trend model</span></span>
<span data-ttu-id="29b79-554">Having created a time series object and having had a look at the data, let's start to construct a trend model for the California milk production data.</span><span class="sxs-lookup"><span data-stu-id="29b79-554">Having created a time series object and having had a look at the data, let's start to construct a trend model for the California milk production data.</span></span> <span data-ttu-id="29b79-555">We can do this with a time series regression.</span><span class="sxs-lookup"><span data-stu-id="29b79-555">We can do this with a time series regression.</span></span> <span data-ttu-id="29b79-556">However, it is clear from the plot that we will need more than a slope and intercept to accurately model the observed trend in the training data.</span><span class="sxs-lookup"><span data-stu-id="29b79-556">However, it is clear from the plot that we will need more than a slope and intercept to accurately model the observed trend in the training data.</span></span>

<span data-ttu-id="29b79-557">Given the small scale of the data, I will build the model for trend in RStudio and then cut and paste the resulting model into Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="29b79-557">Given the small scale of the data, I will build the model for trend in RStudio and then cut and paste the resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="29b79-558">RStudio provides an interactive environment for this type of interactive analysis.</span><span class="sxs-lookup"><span data-stu-id="29b79-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="29b79-559">As a first attempt, I will try a polynomial regression with powers up to 3.</span><span class="sxs-lookup"><span data-stu-id="29b79-559">As a first attempt, I will try a polynomial regression with powers up to 3.</span></span> <span data-ttu-id="29b79-560">There is a real danger of over-fitting these kinds of models.</span><span class="sxs-lookup"><span data-stu-id="29b79-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="29b79-561">Therefore, it is best to avoid high order terms.</span><span class="sxs-lookup"><span data-stu-id="29b79-561">Therefore, it is best to avoid high order terms.</span></span> <span data-ttu-id="29b79-562">The `I()` function inhibits interpretation of the contents (interprets the contents 'as is') and allows you to write a literally interpreted function in a regression equation.</span><span class="sxs-lookup"><span data-stu-id="29b79-562">The `I()` function inhibits interpretation of the contents (interprets the contents 'as is') and allows you to write a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="29b79-563">This generates the following.</span><span class="sxs-lookup"><span data-stu-id="29b79-563">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="29b79-564">From P values (Pr(>|t|)) in this output, we can see that the squared term may not be significant.</span><span class="sxs-lookup"><span data-stu-id="29b79-564">From P values (Pr(>|t|)) in this output, we can see that the squared term may not be significant.</span></span> <span data-ttu-id="29b79-565">I will use the `update()` function to modify this model by dropping the squared term.</span><span class="sxs-lookup"><span data-stu-id="29b79-565">I will use the `update()` function to modify this model by dropping the squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="29b79-566">This generates the following.</span><span class="sxs-lookup"><span data-stu-id="29b79-566">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="29b79-567">This looks better.</span><span class="sxs-lookup"><span data-stu-id="29b79-567">This looks better.</span></span> <span data-ttu-id="29b79-568">All of the terms are significant.</span><span class="sxs-lookup"><span data-stu-id="29b79-568">All of the terms are significant.</span></span> <span data-ttu-id="29b79-569">However, the 2e-16 value is a default value, and should not be taken too seriously.</span><span class="sxs-lookup"><span data-stu-id="29b79-569">However, the 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="29b79-570">As a sanity test, let's make a time series plot of the California dairy production data with the trend curve shown.</span><span class="sxs-lookup"><span data-stu-id="29b79-570">As a sanity test, let's make a time series plot of the California dairy production data with the trend curve shown.</span></span> <span data-ttu-id="29b79-571">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) to create the model and make a plot.</span><span class="sxs-lookup"><span data-stu-id="29b79-571">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) to create the model and make a plot.</span></span> <span data-ttu-id="29b79-572">The result is shown in Figure 23.</span><span class="sxs-lookup"><span data-stu-id="29b79-572">The result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![California milk production data with trend model shown](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="29b79-574">*Figure 23. California milk production data with trend model shown.*</span><span class="sxs-lookup"><span data-stu-id="29b79-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="29b79-575">It looks like the trend model fits the data fairly well.</span><span class="sxs-lookup"><span data-stu-id="29b79-575">It looks like the trend model fits the data fairly well.</span></span> <span data-ttu-id="29b79-576">Further, there does not seem to be evidence of over-fitting, such as odd wiggles in the model curve.</span><span class="sxs-lookup"><span data-stu-id="29b79-576">Further, there does not seem to be evidence of over-fitting, such as odd wiggles in the model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="29b79-577">Seasonal model</span><span class="sxs-lookup"><span data-stu-id="29b79-577">Seasonal model</span></span>
<span data-ttu-id="29b79-578">With a trend model in hand, we need to push on and include the seasonal effects.</span><span class="sxs-lookup"><span data-stu-id="29b79-578">With a trend model in hand, we need to push on and include the seasonal effects.</span></span> <span data-ttu-id="29b79-579">We will use the month of the year as a dummy variable in the linear model to capture the month-by-month effect.</span><span class="sxs-lookup"><span data-stu-id="29b79-579">We will use the month of the year as a dummy variable in the linear model to capture the month-by-month effect.</span></span> <span data-ttu-id="29b79-580">Note that when you introduce factor variables into a model, the intercept must not be computed.</span><span class="sxs-lookup"><span data-stu-id="29b79-580">Note that when you introduce factor variables into a model, the intercept must not be computed.</span></span> <span data-ttu-id="29b79-581">If you do not do this, the formula is over-specified and R will drop one of the desired factors but keep the intercept term.</span><span class="sxs-lookup"><span data-stu-id="29b79-581">If you do not do this, the formula is over-specified and R will drop one of the desired factors but keep the intercept term.</span></span>

<span data-ttu-id="29b79-582">Since we have a satisfactory trend model we can use the `update()` function to add the new terms to the existing model.</span><span class="sxs-lookup"><span data-stu-id="29b79-582">Since we have a satisfactory trend model we can use the `update()` function to add the new terms to the existing model.</span></span> <span data-ttu-id="29b79-583">The -1 in the update formula drops the intercept term.</span><span class="sxs-lookup"><span data-stu-id="29b79-583">The -1 in the update formula drops the intercept term.</span></span> <span data-ttu-id="29b79-584">Continuing in RStudio for the moment:</span><span class="sxs-lookup"><span data-stu-id="29b79-584">Continuing in RStudio for the moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="29b79-585">This generates the following.</span><span class="sxs-lookup"><span data-stu-id="29b79-585">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="29b79-586">We see that the model no longer has an intercept term and has 12 significant month factors.</span><span class="sxs-lookup"><span data-stu-id="29b79-586">We see that the model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="29b79-587">This is exactly what we wanted to see.</span><span class="sxs-lookup"><span data-stu-id="29b79-587">This is exactly what we wanted to see.</span></span>

<span data-ttu-id="29b79-588">Let's make another time series plot of the California dairy production data to see how well the seasonal model is working.</span><span class="sxs-lookup"><span data-stu-id="29b79-588">Let's make another time series plot of the California dairy production data to see how well the seasonal model is working.</span></span> <span data-ttu-id="29b79-589">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] to create the model and make a plot.</span><span class="sxs-lookup"><span data-stu-id="29b79-589">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] to create the model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="29b79-590">Running this code in Azure Machine Learning produces the plot shown in Figure 24.</span><span class="sxs-lookup"><span data-stu-id="29b79-590">Running this code in Azure Machine Learning produces the plot shown in Figure 24.</span></span>

![California milk production with model including seasonal effects](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="29b79-592">*Figure 24. California milk production with model including seasonal effects.*</span><span class="sxs-lookup"><span data-stu-id="29b79-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="29b79-593">The fit to the data shown in Figure 24 is rather encouraging.</span><span class="sxs-lookup"><span data-stu-id="29b79-593">The fit to the data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="29b79-594">Both the trend and the seasonal effect (monthly variation) look reasonable.</span><span class="sxs-lookup"><span data-stu-id="29b79-594">Both the trend and the seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="29b79-595">As another check on our model, let's have a look at the residuals.</span><span class="sxs-lookup"><span data-stu-id="29b79-595">As another check on our model, let's have a look at the residuals.</span></span> <span data-ttu-id="29b79-596">The following code computes the predicted values from our two models, computes the residuals for the seasonal model, and then plots these residuals for the training data.</span><span class="sxs-lookup"><span data-stu-id="29b79-596">The following code computes the predicted values from our two models, computes the residuals for the seasonal model, and then plots these residuals for the training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot the residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="29b79-597">The residual plot is shown in Figure 25.</span><span class="sxs-lookup"><span data-stu-id="29b79-597">The residual plot is shown in Figure 25.</span></span>

![Residuals of the seasonal model for the training data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="29b79-599">*Figure 25. Residuals of the seasonal model for the training data.*</span><span class="sxs-lookup"><span data-stu-id="29b79-599">*Figure 25. Residuals of the seasonal model for the training data.*</span></span>

<span data-ttu-id="29b79-600">These residuals look reasonable.</span><span class="sxs-lookup"><span data-stu-id="29b79-600">These residuals look reasonable.</span></span> <span data-ttu-id="29b79-601">There is no particular structure, except the effect of the 2008-2009 recession, which our model does not account for particularly well.</span><span class="sxs-lookup"><span data-stu-id="29b79-601">There is no particular structure, except the effect of the 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="29b79-602">The plot shown in Figure 25 is useful for detecting any time-dependent patterns in the residuals.</span><span class="sxs-lookup"><span data-stu-id="29b79-602">The plot shown in Figure 25 is useful for detecting any time-dependent patterns in the residuals.</span></span> <span data-ttu-id="29b79-603">The explicit approach of computing and plotting the residuals I used places the residuals in time order on the plot.</span><span class="sxs-lookup"><span data-stu-id="29b79-603">The explicit approach of computing and plotting the residuals I used places the residuals in time order on the plot.</span></span> <span data-ttu-id="29b79-604">If, on the other hand, I had plotted `milk.lm$residuals`, the plot would not have been in time order.</span><span class="sxs-lookup"><span data-stu-id="29b79-604">If, on the other hand, I had plotted `milk.lm$residuals`, the plot would not have been in time order.</span></span>

<span data-ttu-id="29b79-605">You can also use `plot.lm()` to produce a series of diagnostic plots.</span><span class="sxs-lookup"><span data-stu-id="29b79-605">You can also use `plot.lm()` to produce a series of diagnostic plots.</span></span>

    ## Show the diagnostic plots for the model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="29b79-606">This code produces a series of diagnostic plots shown in Figure 26.</span><span class="sxs-lookup"><span data-stu-id="29b79-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![First of diagnostic plots for the seasonal model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Second of diagnostic plots for the seasonal model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Third of diagnostic plots for the seasonal model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Fourth of diagnostic plots for the seasonal model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="29b79-611">*Figure 26. Diagnostic plots for the seasonal model.*</span><span class="sxs-lookup"><span data-stu-id="29b79-611">*Figure 26. Diagnostic plots for the seasonal model.*</span></span>

<span data-ttu-id="29b79-612">There are a few highly influential points identified in these plots, but nothing to cause great concern.</span><span class="sxs-lookup"><span data-stu-id="29b79-612">There are a few highly influential points identified in these plots, but nothing to cause great concern.</span></span> <span data-ttu-id="29b79-613">Further, we can see from the Normal Q-Q plot that the residuals are close to normally distributed, an important assumption for linear models.</span><span class="sxs-lookup"><span data-stu-id="29b79-613">Further, we can see from the Normal Q-Q plot that the residuals are close to normally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="29b79-614">Forecasting and model evaluation</span><span class="sxs-lookup"><span data-stu-id="29b79-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="29b79-615">There is just one more thing to do to complete our example.</span><span class="sxs-lookup"><span data-stu-id="29b79-615">There is just one more thing to do to complete our example.</span></span> <span data-ttu-id="29b79-616">We need to compute forecasts and measure the error against the actual data.</span><span class="sxs-lookup"><span data-stu-id="29b79-616">We need to compute forecasts and measure the error against the actual data.</span></span> <span data-ttu-id="29b79-617">Our forecast will be for the 12 months of 2013.</span><span class="sxs-lookup"><span data-stu-id="29b79-617">Our forecast will be for the 12 months of 2013.</span></span> <span data-ttu-id="29b79-618">We can compute an error measure for this forecast to the actual data that is not part of our training dataset.</span><span class="sxs-lookup"><span data-stu-id="29b79-618">We can compute an error measure for this forecast to the actual data that is not part of our training dataset.</span></span> <span data-ttu-id="29b79-619">Additionally, we can compare performance on the 18 years of training data to the 12 months of test data.</span><span class="sxs-lookup"><span data-stu-id="29b79-619">Additionally, we can compare performance on the 18 years of training data to the 12 months of test data.</span></span>  

<span data-ttu-id="29b79-620">A number of metrics are used to measure the performance of time series models.</span><span class="sxs-lookup"><span data-stu-id="29b79-620">A number of metrics are used to measure the performance of time series models.</span></span> <span data-ttu-id="29b79-621">In our case we will use the root mean square (RMS) error.</span><span class="sxs-lookup"><span data-stu-id="29b79-621">In our case we will use the root mean square (RMS) error.</span></span> <span data-ttu-id="29b79-622">The following function computes the RMS error between two series.</span><span class="sxs-lookup"><span data-stu-id="29b79-622">The following function computes the RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function to compute the RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments to function RMS.error of wrong type encountered",
                    "ERROR: Input vector to function RMS.error is too short",
                    "ERROR: Input vectors to function RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check the arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate the values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute the RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="29b79-623">As with the `log.transform()` function we discussed in the "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span><span class="sxs-lookup"><span data-stu-id="29b79-623">As with the `log.transform()` function we discussed in the "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="29b79-624">The principles employed are the same.</span><span class="sxs-lookup"><span data-stu-id="29b79-624">The principles employed are the same.</span></span> <span data-ttu-id="29b79-625">The work is done in two places wrapped in `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="29b79-625">The work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="29b79-626">First, the time series are exponentiated, since we have been working with the logs of the values.</span><span class="sxs-lookup"><span data-stu-id="29b79-626">First, the time series are exponentiated, since we have been working with the logs of the values.</span></span> <span data-ttu-id="29b79-627">Second, the actual RMS error is computed.</span><span class="sxs-lookup"><span data-stu-id="29b79-627">Second, the actual RMS error is computed.</span></span>  

<span data-ttu-id="29b79-628">Equipped with a function to measure the RMS error, let's build and output a dataframe containing the RMS errors.</span><span class="sxs-lookup"><span data-stu-id="29b79-628">Equipped with a function to measure the RMS error, let's build and output a dataframe containing the RMS errors.</span></span> <span data-ttu-id="29b79-629">We will include terms for the trend model alone and the complete model with seasonal factors.</span><span class="sxs-lookup"><span data-stu-id="29b79-629">We will include terms for the trend model alone and the complete model with seasonal factors.</span></span> <span data-ttu-id="29b79-630">The following code does the job by using the two linear models we have constructed.</span><span class="sxs-lookup"><span data-stu-id="29b79-630">The following code does the job by using the two linear models we have constructed.</span></span>

    ## Compute the RMS error in a dataframe
    ## Include the row names in the first column so they will
    ## appear in the output of the Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="29b79-631">Running this code produces the output shown in Figure 27 at the Result Dataset output port.</span><span class="sxs-lookup"><span data-stu-id="29b79-631">Running this code produces the output shown in Figure 27 at the Result Dataset output port.</span></span>

![Comparison of RMS errors for the models][26]

<span data-ttu-id="29b79-633">*Figure 27. Comparison of RMS errors for the models.*</span><span class="sxs-lookup"><span data-stu-id="29b79-633">*Figure 27. Comparison of RMS errors for the models.*</span></span>

<span data-ttu-id="29b79-634">From these results, we see that adding the seasonal factors to the model reduces the RMS error significantly.</span><span class="sxs-lookup"><span data-stu-id="29b79-634">From these results, we see that adding the seasonal factors to the model reduces the RMS error significantly.</span></span> <span data-ttu-id="29b79-635">Not too surprisingly, the RMS error for the training data is a bit less than for the forecast.</span><span class="sxs-lookup"><span data-stu-id="29b79-635">Not too surprisingly, the RMS error for the training data is a bit less than for the forecast.</span></span>

## <a id="appendixa"></a><span data-ttu-id="29b79-636">APPENDIX A: Guide to RStudio</span><span class="sxs-lookup"><span data-stu-id="29b79-636">APPENDIX A: Guide to RStudio</span></span>
<span data-ttu-id="29b79-637">RStudio is quite well documented, so in this appendix I will provide some links to the key sections of the RStudio documentation to get you started.</span><span class="sxs-lookup"><span data-stu-id="29b79-637">RStudio is quite well documented, so in this appendix I will provide some links to the key sections of the RStudio documentation to get you started.</span></span>

1. <span data-ttu-id="29b79-638">Creating projects</span><span class="sxs-lookup"><span data-stu-id="29b79-638">Creating projects</span></span>
   
   <span data-ttu-id="29b79-639">You can organize and manage your R code into projects by using RStudio.</span><span class="sxs-lookup"><span data-stu-id="29b79-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="29b79-640">The documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="29b79-640">The documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="29b79-641">I recommend that you follow these directions and create a project for the R code examples in this document.</span><span class="sxs-lookup"><span data-stu-id="29b79-641">I recommend that you follow these directions and create a project for the R code examples in this document.</span></span>  
2. <span data-ttu-id="29b79-642">Editing and executing R code</span><span class="sxs-lookup"><span data-stu-id="29b79-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="29b79-643">RStudio provides an integrated environment for editing and executing R code.</span><span class="sxs-lookup"><span data-stu-id="29b79-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="29b79-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="29b79-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="29b79-645">Debugging</span><span class="sxs-lookup"><span data-stu-id="29b79-645">Debugging</span></span>
   
   <span data-ttu-id="29b79-646">RStudio includes powerful debugging capabilities.</span><span class="sxs-lookup"><span data-stu-id="29b79-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="29b79-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="29b79-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="29b79-648">The breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="29b79-648">The breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <a id="appendixb"></a><span data-ttu-id="29b79-649">APPENDIX B: Further reading</span><span class="sxs-lookup"><span data-stu-id="29b79-649">APPENDIX B: Further reading</span></span>
<span data-ttu-id="29b79-650">This R programming tutorial covers the basics of what you need to use the R language with Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="29b79-650">This R programming tutorial covers the basics of what you need to use the R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="29b79-651">If you are not familiar with R, two introductions are available on CRAN:</span><span class="sxs-lookup"><span data-stu-id="29b79-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="29b79-652">R for Beginners by Emmanuel Paradis is a good place to start at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="29b79-652">R for Beginners by Emmanuel Paradis is a good place to start at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="29b79-653">An Introduction to R by W. N.</span><span class="sxs-lookup"><span data-stu-id="29b79-653">An Introduction to R by W. N.</span></span> <span data-ttu-id="29b79-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="29b79-654">Venables et.</span></span> <span data-ttu-id="29b79-655">al.</span><span class="sxs-lookup"><span data-stu-id="29b79-655">al.</span></span> <span data-ttu-id="29b79-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="29b79-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="29b79-657">There are many books on R that can help you get started.</span><span class="sxs-lookup"><span data-stu-id="29b79-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="29b79-658">Here are a few I find useful:</span><span class="sxs-lookup"><span data-stu-id="29b79-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="29b79-659">The Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction to programming in R.</span><span class="sxs-lookup"><span data-stu-id="29b79-659">The Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction to programming in R.</span></span>  
* <span data-ttu-id="29b79-660">R Cookbook by Paul Teetor provides a problem and solution approach to using R.</span><span class="sxs-lookup"><span data-stu-id="29b79-660">R Cookbook by Paul Teetor provides a problem and solution approach to using R.</span></span>  
* <span data-ttu-id="29b79-661">R in Action by Robert Kabacoff is another useful introductory book.</span><span class="sxs-lookup"><span data-stu-id="29b79-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="29b79-662">The companion Quick R website is a useful resource at http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="29b79-662">The companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="29b79-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. The book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="29b79-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. The book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="29b79-664">If you want a deep dive into advanced topics in R, have a look at the book Advanced R by Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="29b79-664">If you want a deep dive into advanced topics in R, have a look at the book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="29b79-665">The online version of this book is available for free at http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="29b79-665">The online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="29b79-666">A catalogue of R time series packages can be found in the CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="29b79-666">A catalogue of R time series packages can be found in the CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="29b79-667">For information on specific time series object packages, you should refer to the documentation for that package.</span><span class="sxs-lookup"><span data-stu-id="29b79-667">For information on specific time series object packages, you should refer to the documentation for that package.</span></span>

<span data-ttu-id="29b79-668">The book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction to using R for time series analysis.</span><span class="sxs-lookup"><span data-stu-id="29b79-668">The book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction to using R for time series analysis.</span></span> <span data-ttu-id="29b79-669">Many more theoretical texts provide R examples.</span><span class="sxs-lookup"><span data-stu-id="29b79-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="29b79-670">Some great internet resources:</span><span class="sxs-lookup"><span data-stu-id="29b79-670">Some great internet resources:</span></span>

* <span data-ttu-id="29b79-671">DataCamp: DataCamp teaches R in the comfort of your browser with video lessons and coding exercises.</span><span class="sxs-lookup"><span data-stu-id="29b79-671">DataCamp: DataCamp teaches R in the comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="29b79-672">There are interactive tutorials on the latest R techniques and packages.</span><span class="sxs-lookup"><span data-stu-id="29b79-672">There are interactive tutorials on the latest R techniques and packages.</span></span> <span data-ttu-id="29b79-673">Take the free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span><span class="sxs-lookup"><span data-stu-id="29b79-673">Take the free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="29b79-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="29b79-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="29b79-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="29b79-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="29b79-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="29b79-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig8.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig9.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig10.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig11.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig12.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig13.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig14.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig15.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig16.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig17.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig18.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig19.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig20.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig21.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig22.png

[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

































