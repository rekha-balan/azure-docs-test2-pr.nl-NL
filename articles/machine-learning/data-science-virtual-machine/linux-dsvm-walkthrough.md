---
title: Data science with the Linux Data Science Virtual Machine on Azure| Microsoft Docs
description: How to perform several common data science tasks with the Linux Data Science VM.
services: machine-learning
documentationcenter: ''
author: gopitk
manager: cgronlun
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.component: data-science-vm
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/16/2018
ms.author: gokuma
ms.openlocfilehash: d9b89329e2a9bdb26c9aa1d12bc181c61518dcb8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864669"
---
# <a name="data-science-with-a-linux-data-science-virtual-machine-on-azure"></a><span data-ttu-id="ec3ce-103">Data science with a Linux Data Science Virtual Machine on Azure</span><span class="sxs-lookup"><span data-stu-id="ec3ce-103">Data science with a Linux Data Science Virtual Machine on Azure</span></span>
<span data-ttu-id="ec3ce-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span></span> <span data-ttu-id="ec3ce-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="ec3ce-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](linux-dsvm-intro.md) topic.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="ec3ce-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span></span> <span data-ttu-id="ec3ce-108">You can easily scale up the VM, if needed, and stop it when not in use.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-108">You can easily scale up the VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="ec3ce-109">So this resource is both elastic and cost-efficient.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="ec3ce-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="ec3ce-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span></span> <span data-ttu-id="ec3ce-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="ec3ce-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="ec3ce-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span></span> <span data-ttu-id="ec3ce-115">The statistics included are discussed in the next but one section.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-115">The statistics included are discussed in the next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec3ce-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ec3ce-116">Prerequisites</span></span>
<span data-ttu-id="ec3ce-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span></span>

* <span data-ttu-id="ec3ce-118">An **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-118">An **Azure subscription**.</span></span> <span data-ttu-id="ec3ce-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="ec3ce-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="ec3ce-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="ec3ce-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="ec3ce-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span>
* <span data-ttu-id="ec3ce-124">For a smoother scrolling experience, toggle the gfx.xrender.enabled flag in about:config in VMs FireFox browser.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-124">For a smoother scrolling experience, toggle the gfx.xrender.enabled flag in about:config in VMs FireFox browser.</span></span> <span data-ttu-id="ec3ce-125">[See more here.](https://www.reddit.com/r/firefox/comments/4nfmvp/ff_47_unbearable_slow_over_remote_x11/).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-125">[See more here.](https://www.reddit.com/r/firefox/comments/4nfmvp/ff_47_unbearable_slow_over_remote_x11/).</span></span> <span data-ttu-id="ec3ce-126">Also consider toggling *mousewheel.enable_pixel_scrolling* to False.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-126">Also consider toggling *mousewheel.enable_pixel_scrolling* to False.</span></span> [<span data-ttu-id="ec3ce-127">Instructions here.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-127">Instructions here.</span></span>](https://support.mozilla.org/en-US/questions/981140)
* <span data-ttu-id="ec3ce-128">An **AzureML account**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-128">An **AzureML account**.</span></span> <span data-ttu-id="ec3ce-129">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-129">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="ec3ce-130">There is a free usage tier to help you get started.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-130">There is a free usage tier to help you get started.</span></span>

## <a name="download-the-spambase-dataset"></a><span data-ttu-id="ec3ce-131">Download the spambase dataset</span><span class="sxs-lookup"><span data-stu-id="ec3ce-131">Download the spambase dataset</span></span>
<span data-ttu-id="ec3ce-132">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-132">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="ec3ce-133">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-133">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="ec3ce-134">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine (CentOS Edition).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-134">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine (CentOS Edition).</span></span> <span data-ttu-id="ec3ce-135">This size DSVM is capable of handling the procedures in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-135">This size DSVM is capable of handling the procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="ec3ce-136">If you need more storage space, you can create additional disks and attach them to your VM.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-136">If you need more storage space, you can create additional disks and attach them to your VM.</span></span> <span data-ttu-id="ec3ce-137">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-137">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span></span> <span data-ttu-id="ec3ce-138">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-138">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ec3ce-139">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-139">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span></span> <span data-ttu-id="ec3ce-140">So these procedures can be done entirely from the VM itself.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-140">So these procedures can be done entirely from the VM itself.</span></span> <span data-ttu-id="ec3ce-141">Another option to increase storage is to use [Azure files](../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-141">Another option to increase storage is to use [Azure files](../../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="ec3ce-142">To download the data, open a terminal window and run this command:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-142">To download the data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="ec3ce-143">The downloaded file does not have a header row, so let's create another file that does have a header.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-143">The downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="ec3ce-144">Run this command to create a file with the appropriate headers:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-144">Run this command to create a file with the appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="ec3ce-145">Then concatenate the two files together with the command:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-145">Then concatenate the two files together with the command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="ec3ce-146">The dataset has several types of statistics on each email:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-146">The dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="ec3ce-147">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-147">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span></span> <span data-ttu-id="ec3ce-148">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-148">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span></span>
* <span data-ttu-id="ec3ce-149">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-149">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span></span>
* <span data-ttu-id="ec3ce-150">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-150">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="ec3ce-151">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-151">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="ec3ce-152">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-152">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="ec3ce-153">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-153">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-the-dataset-with-microsoft-r-open"></a><span data-ttu-id="ec3ce-154">Explore the dataset with Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="ec3ce-154">Explore the dataset with Microsoft R Open</span></span>
<span data-ttu-id="ec3ce-155">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-155">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="ec3ce-156">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-156">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="ec3ce-157">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-157">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span></span>

<span data-ttu-id="ec3ce-158">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-158">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span></span> <span data-ttu-id="ec3ce-159">From the git command line, run:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-159">From the git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="ec3ce-160">Open a terminal window and start a new R session with the R interactive console or use RStudio preinstalled on the machine.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-160">Open a terminal window and start a new R session with the R interactive console or use RStudio preinstalled on the machine.</span></span>


<span data-ttu-id="ec3ce-161">To import the data and set up the environment, run:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-161">To import the data and set up the environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="ec3ce-162">To see summary statistics about each column:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-162">To see summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="ec3ce-163">For a different view of the data:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-163">For a different view of the data:</span></span>

    str(data)

<span data-ttu-id="ec3ce-164">This shows you the type of each variable and the first few values in the dataset.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-164">This shows you the type of each variable and the first few values in the dataset.</span></span>

<span data-ttu-id="ec3ce-165">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-165">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="ec3ce-166">To set its type:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-166">To set its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="ec3ce-167">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-167">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span></span> <span data-ttu-id="ec3ce-168">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-168">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span></span> <span data-ttu-id="ec3ce-169">Let's plot those frequencies here with the following commands:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-169">Let's plot those frequencies here with the following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="ec3ce-170">Since the zero bar is skewing the plot, let's get rid of it:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-170">Since the zero bar is skewing the plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="ec3ce-171">There is a non-trivial density above 1 that looks interesting.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-171">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="ec3ce-172">Let's look at just that data:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-172">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="ec3ce-173">Then split it by spam vs ham:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-173">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="ec3ce-174">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-174">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="ec3ce-175">Train and test an ML model</span><span class="sxs-lookup"><span data-stu-id="ec3ce-175">Train and test an ML model</span></span>
<span data-ttu-id="ec3ce-176">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-176">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span></span> <span data-ttu-id="ec3ce-177">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-177">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="ec3ce-178">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-178">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span></span>
>
>

<span data-ttu-id="ec3ce-179">First, let's split the dataset into training and test sets:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-179">First, let's split the dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="ec3ce-180">And then create a decision tree to classify the emails.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-180">And then create a decision tree to classify the emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="ec3ce-181">Here is the result:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-181">Here is the result:</span></span>

![1](./media/linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="ec3ce-183">To determine how well it performs on the training set, use the following code:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-183">To determine how well it performs on the training set, use the following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="ec3ce-184">To determine how well it performs on the test set:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-184">To determine how well it performs on the test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="ec3ce-185">Let's also try a random forest model.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-185">Let's also try a random forest model.</span></span> <span data-ttu-id="ec3ce-186">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-186">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span></span> <span data-ttu-id="ec3ce-187">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-187">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-to-azure-ml"></a><span data-ttu-id="ec3ce-188">Deploy a model to Azure ML</span><span class="sxs-lookup"><span data-stu-id="ec3ce-188">Deploy a model to Azure ML</span></span>
<span data-ttu-id="ec3ce-189">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-189">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span></span> <span data-ttu-id="ec3ce-190">One of the nice features of AzureML is its ability to publish any R function as a web service.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-190">One of the nice features of AzureML is its ability to publish any R function as a web service.</span></span> <span data-ttu-id="ec3ce-191">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-191">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span></span>

<span data-ttu-id="ec3ce-192">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-192">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span></span> <span data-ttu-id="ec3ce-193">You need your workspace ID and an authorization token to sign in.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-193">You need your workspace ID and an authorization token to sign in.</span></span> <span data-ttu-id="ec3ce-194">To find these values and initialize the AzureML variables with them:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-194">To find these values and initialize the AzureML variables with them:</span></span>

<span data-ttu-id="ec3ce-195">Select **Settings** on the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-195">Select **Settings** on the left-hand menu.</span></span> <span data-ttu-id="ec3ce-196">Note your **WORKSPACE ID**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-196">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="ec3ce-197">![2](./media/linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="ec3ce-197">![2](./media/linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="ec3ce-198">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](./media/linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="ec3ce-198">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](./media/linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="ec3ce-199">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-199">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span></span>

    if(!require("AzureML")) install.packages("AzureML")
    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="ec3ce-200">Let's simplify the model to make this demonstration easier to implement.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-200">Let's simplify the model to make this demonstration easier to implement.</span></span> <span data-ttu-id="ec3ce-201">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-201">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="ec3ce-202">We need a prediction function that takes the features as an input and returns the predicted values:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-202">We need a prediction function that takes the features as an input and returns the predicted values:</span></span>

    predictSpam <- function(newdata) {
      predictDF <- predict(model.rpart, newdata = newdata)
      return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }


<span data-ttu-id="ec3ce-203">Publish the predictSpam function to AzureML using the **publishWebService** function:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-203">Publish the predictSpam function to AzureML using the **publishWebService** function:</span></span>

    spamWebService <- publishWebService(ws, fun = predictSpam, name="spamWebService", inputSchema = smallTrainSet, data.frame=TRUE)


<span data-ttu-id="ec3ce-204">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-204">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span></span>

<span data-ttu-id="ec3ce-205">View details of the latest published web service, including its API endpoint and access keys with the command:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-205">View details of the latest published web service, including its API endpoint and access keys with the command:</span></span>

    s<-tail(services(ws, name = "spamWebService"), 1)
    ep <- endpoints(ws,s)
    ep

<span data-ttu-id="ec3ce-206">To try it out on the first 10 rows of the test set:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-206">To try it out on the first 10 rows of the test set:</span></span>

    consume(ep, smallTestSet[1:10, ])


## <a name="use-other-tools-available"></a><span data-ttu-id="ec3ce-207">Use other tools available</span><span class="sxs-lookup"><span data-stu-id="ec3ce-207">Use other tools available</span></span>
<span data-ttu-id="ec3ce-208">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-208">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span></span>

* <span data-ttu-id="ec3ce-209">XGBoost</span><span class="sxs-lookup"><span data-stu-id="ec3ce-209">XGBoost</span></span>
* <span data-ttu-id="ec3ce-210">Python</span><span class="sxs-lookup"><span data-stu-id="ec3ce-210">Python</span></span>
* <span data-ttu-id="ec3ce-211">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="ec3ce-211">Jupyterhub</span></span>
* <span data-ttu-id="ec3ce-212">Rattle</span><span class="sxs-lookup"><span data-stu-id="ec3ce-212">Rattle</span></span>
* <span data-ttu-id="ec3ce-213">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="ec3ce-213">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="ec3ce-214">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ec3ce-214">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="ec3ce-215">XGBoost</span><span class="sxs-lookup"><span data-stu-id="ec3ce-215">XGBoost</span></span>
<span data-ttu-id="ec3ce-216">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-216">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="ec3ce-217">XGBoost can also call from python or a command line.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-217">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="ec3ce-218">Python</span><span class="sxs-lookup"><span data-stu-id="ec3ce-218">Python</span></span>
<span data-ttu-id="ec3ce-219">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-219">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="ec3ce-220">The Anaconda distribution includes [Conda](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-220">The Anaconda distribution includes [Conda](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="ec3ce-221">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-221">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="ec3ce-222">To make predictions:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-222">To make predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="ec3ce-223">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-223">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span></span>

    X = data[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="ec3ce-224">To publish the model to AzureML:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-224">To publish the model to AzureML:</span></span>

    # Publish the model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about the resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call the model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="ec3ce-225">This is only available for python 2.7 and is not yet supported on 3.5.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-225">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="ec3ce-226">Run with **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-226">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="ec3ce-227">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="ec3ce-227">Jupyterhub</span></span>
<span data-ttu-id="ec3ce-228">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-228">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="ec3ce-229">The Jupyter notebook is accessed through JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-229">The Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="ec3ce-230">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-230">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="ec3ce-231">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-231">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

> [!NOTE]
> <span data-ttu-id="ec3ce-232">To use the Python Package Manager (via the `pip` command) from a Jupyter notebook in the current kernel, the following command may be used in code cell, for example:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-232">To use the Python Package Manager (via the `pip` command) from a Jupyter notebook in the current kernel, the following command may be used in code cell, for example:</span></span>
```python
   import sys
   ! {sys.executable} -m pip install numpy -y
```
>
>

> [!NOTE]
> <span data-ttu-id="ec3ce-233">To use the Conda installer (via the `conda` command) from a Jupyter notebook in the current kernel, the following command may be used in code cell, for example:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-233">To use the Conda installer (via the `conda` command) from a Jupyter notebook in the current kernel, the following command may be used in code cell, for example:</span></span>
```python
   import sys
   ! {sys.prefix}/bin/conda install --yes --prefix {sys.prefix} numpy
```
>
>

<span data-ttu-id="ec3ce-234">Several sample notebooks are already installed on the VM:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-234">Several sample notebooks are already installed on the VM:</span></span>

* <span data-ttu-id="ec3ce-235">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-235">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="ec3ce-236">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-236">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="ec3ce-237">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-237">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="ec3ce-238">The Julia language is also available from the command line on the Linux Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-238">The Julia language is also available from the command line on the Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="ec3ce-239">Rattle</span><span class="sxs-lookup"><span data-stu-id="ec3ce-239">Rattle</span></span>
<span data-ttu-id="ec3ce-240">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-240">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="ec3ce-241">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-241">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="ec3ce-242">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-242">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="ec3ce-243">Install and start Rattle with the following commands:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-243">Install and start Rattle with the following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="ec3ce-244">Installation is not required on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-244">Installation is not required on the DSVM.</span></span> <span data-ttu-id="ec3ce-245">But Rattle may prompt you to install additional packages when it loads.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-245">But Rattle may prompt you to install additional packages when it loads.</span></span>
>
>

<span data-ttu-id="ec3ce-246">Rattle uses a tab-based interface.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-246">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="ec3ce-247">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-247">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="ec3ce-248">The data science process flows from left to right through the tabs.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-248">The data science process flows from left to right through the tabs.</span></span> <span data-ttu-id="ec3ce-249">But the last tab contains a log of the R commands run by Rattle.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-249">But the last tab contains a log of the R commands run by Rattle.</span></span>

<span data-ttu-id="ec3ce-250">To load and configure the dataset:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-250">To load and configure the dataset:</span></span>

* <span data-ttu-id="ec3ce-251">To load the file, select the **Data** tab, then</span><span class="sxs-lookup"><span data-stu-id="ec3ce-251">To load the file, select the **Data** tab, then</span></span>
* <span data-ttu-id="ec3ce-252">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-252">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="ec3ce-253">To load the file.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-253">To load the file.</span></span> <span data-ttu-id="ec3ce-254">select **Execute** in the top row of buttons.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-254">select **Execute** in the top row of buttons.</span></span> <span data-ttu-id="ec3ce-255">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-255">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span></span>
* <span data-ttu-id="ec3ce-256">Rattle has correctly identified the **spam** column as the target.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-256">Rattle has correctly identified the **spam** column as the target.</span></span> <span data-ttu-id="ec3ce-257">Select the spam column, then set the **Target Data Type** to **Categoric**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-257">Select the spam column, then set the **Target Data Type** to **Categoric**.</span></span>

<span data-ttu-id="ec3ce-258">To explore the data:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-258">To explore the data:</span></span>

* <span data-ttu-id="ec3ce-259">Select the **Explore** tab.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-259">Select the **Explore** tab.</span></span>
* <span data-ttu-id="ec3ce-260">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-260">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span></span>
* <span data-ttu-id="ec3ce-261">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-261">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="ec3ce-262">The **Explore** tab also allows you to generate many insightful plots.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-262">The **Explore** tab also allows you to generate many insightful plots.</span></span> <span data-ttu-id="ec3ce-263">To plot a histogram of the data:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-263">To plot a histogram of the data:</span></span>

* <span data-ttu-id="ec3ce-264">Select **Distributions**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-264">Select **Distributions**.</span></span>
* <span data-ttu-id="ec3ce-265">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-265">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="ec3ce-266">Select **Execute**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-266">Select **Execute**.</span></span> <span data-ttu-id="ec3ce-267">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span><span class="sxs-lookup"><span data-stu-id="ec3ce-267">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="ec3ce-268">The Correlation plots are also interesting.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-268">The Correlation plots are also interesting.</span></span> <span data-ttu-id="ec3ce-269">To create one:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-269">To create one:</span></span>

* <span data-ttu-id="ec3ce-270">Choose **Correlation** as the **Type**, then</span><span class="sxs-lookup"><span data-stu-id="ec3ce-270">Choose **Correlation** as the **Type**, then</span></span>
* <span data-ttu-id="ec3ce-271">Select **Execute**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-271">Select **Execute**.</span></span>
* <span data-ttu-id="ec3ce-272">Rattle warns you that it recommends a maximum of 40 variables.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-272">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="ec3ce-273">Select **Yes** to view the plot.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-273">Select **Yes** to view the plot.</span></span>

<span data-ttu-id="ec3ce-274">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-274">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span></span> <span data-ttu-id="ec3ce-275">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-275">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span></span>

<span data-ttu-id="ec3ce-276">The numeric values for the correlations between words are available in the Explore window.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-276">The numeric values for the correlations between words are available in the Explore window.</span></span> <span data-ttu-id="ec3ce-277">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span><span class="sxs-lookup"><span data-stu-id="ec3ce-277">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="ec3ce-278">Rattle can transform the dataset to handle some common issues.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-278">Rattle can transform the dataset to handle some common issues.</span></span> <span data-ttu-id="ec3ce-279">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-279">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="ec3ce-280">Rattle can also identify association rules between observations and/or variables.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-280">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="ec3ce-281">These tabs are out of scope for this introductory walkthrough.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-281">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="ec3ce-282">Rattle can also perform cluster analysis.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-282">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="ec3ce-283">Let's exclude some features to make the output easier to read.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-283">Let's exclude some features to make the output easier to read.</span></span> <span data-ttu-id="ec3ce-284">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-284">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span></span>

* <span data-ttu-id="ec3ce-285">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="ec3ce-285">word_freq_hp</span></span>
* <span data-ttu-id="ec3ce-286">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="ec3ce-286">word_freq_technology</span></span>
* <span data-ttu-id="ec3ce-287">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="ec3ce-287">word_freq_george</span></span>
* <span data-ttu-id="ec3ce-288">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="ec3ce-288">word_freq_remove</span></span>
* <span data-ttu-id="ec3ce-289">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="ec3ce-289">word_freq_your</span></span>
* <span data-ttu-id="ec3ce-290">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="ec3ce-290">word_freq_dollar</span></span>
* <span data-ttu-id="ec3ce-291">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="ec3ce-291">word_freq_money</span></span>
* <span data-ttu-id="ec3ce-292">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="ec3ce-292">capital_run_length_longest</span></span>
* <span data-ttu-id="ec3ce-293">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="ec3ce-293">word_freq_business</span></span>
* <span data-ttu-id="ec3ce-294">spam</span><span class="sxs-lookup"><span data-stu-id="ec3ce-294">spam</span></span>

<span data-ttu-id="ec3ce-295">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-295">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span></span> <span data-ttu-id="ec3ce-296">Then **Execute**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-296">Then **Execute**.</span></span> <span data-ttu-id="ec3ce-297">The results are displayed in the output window.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-297">The results are displayed in the output window.</span></span> <span data-ttu-id="ec3ce-298">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-298">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="ec3ce-299">To build a simple decision tree machine learning model:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-299">To build a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="ec3ce-300">Select the **Model** tab,</span><span class="sxs-lookup"><span data-stu-id="ec3ce-300">Select the **Model** tab,</span></span>
* <span data-ttu-id="ec3ce-301">Choose **Tree** as the **Type**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-301">Choose **Tree** as the **Type**.</span></span>
* <span data-ttu-id="ec3ce-302">Select **Execute** to display the tree in text form in the output window.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-302">Select **Execute** to display the tree in text form in the output window.</span></span>
* <span data-ttu-id="ec3ce-303">Select the **Draw** button to view a graphical version.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-303">Select the **Draw** button to view a graphical version.</span></span> <span data-ttu-id="ec3ce-304">This looks quite similar to the tree we obtained earlier using *rpart*.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-304">This looks quite similar to the tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="ec3ce-305">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-305">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="ec3ce-306">Here is the procedure:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-306">Here is the procedure:</span></span>

* <span data-ttu-id="ec3ce-307">Choose **All** for the **Type**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-307">Choose **All** for the **Type**.</span></span>
* <span data-ttu-id="ec3ce-308">Select **Execute**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-308">Select **Execute**.</span></span>
* <span data-ttu-id="ec3ce-309">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-309">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span></span>
* <span data-ttu-id="ec3ce-310">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-310">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span></span>
* <span data-ttu-id="ec3ce-311">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-311">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="ec3ce-312">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-312">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span></span> <span data-ttu-id="ec3ce-313">You can select the **Export** button to save it.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-313">You can select the **Export** button to save it.</span></span>

> [!NOTE]
> <span data-ttu-id="ec3ce-314">There is a bug in current release of Rattle.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-314">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="ec3ce-315">To modify the script or use it to repeat your steps later, you must insert a # character in front of \*Export this log ... \* in the text of the log.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-315">To modify the script or use it to repeat your steps later, you must insert a # character in front of \*Export this log ... \* in the text of the log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="ec3ce-316">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="ec3ce-316">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="ec3ce-317">The DSVM comes with PostgreSQL installed.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-317">The DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="ec3ce-318">PostgreSQL is a sophisticated, open-source relational database.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-318">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="ec3ce-319">This section shows how to load our spam dataset into PostgreSQL and then query it.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-319">This section shows how to load our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="ec3ce-320">Before you can load the data, you need to allow password authentication from the localhost.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-320">Before you can load the data, you need to allow password authentication from the localhost.</span></span> <span data-ttu-id="ec3ce-321">At a command prompt:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-321">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="ec3ce-322">Near the bottom of the config file are several lines that detail the allowed connections:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-322">Near the bottom of the config file are several lines that detail the allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="ec3ce-323">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-323">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="ec3ce-324">And restart the postgres service:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-324">And restart the postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="ec3ce-325">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-325">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="ec3ce-326">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-326">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="ec3ce-327">Then log in to psql as your user:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-327">Then log in to psql as your user:</span></span>

    psql

<span data-ttu-id="ec3ce-328">And import the data into a new database:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-328">And import the data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="ec3ce-329">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-329">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="ec3ce-330">To get started, launch Squirrel SQL from the Applications menu.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-330">To get started, launch Squirrel SQL from the Applications menu.</span></span> <span data-ttu-id="ec3ce-331">To set up the driver:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-331">To set up the driver:</span></span>

* <span data-ttu-id="ec3ce-332">Select **Windows**, then **View Drivers**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-332">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="ec3ce-333">Right-click on **PostgreSQL** and select **Modify Driver**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-333">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="ec3ce-334">Select **Extra Class Path**, then **Add**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-334">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="ec3ce-335">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span><span class="sxs-lookup"><span data-stu-id="ec3ce-335">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span></span>
* <span data-ttu-id="ec3ce-336">Select **Open**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-336">Select **Open**.</span></span>
* <span data-ttu-id="ec3ce-337">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-337">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="ec3ce-338">To set up the connection to the local server:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-338">To set up the connection to the local server:</span></span>

* <span data-ttu-id="ec3ce-339">Select **Windows**, then **View Aliases.**</span><span class="sxs-lookup"><span data-stu-id="ec3ce-339">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="ec3ce-340">Choose the **+** button to make a new alias.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-340">Choose the **+** button to make a new alias.</span></span>
* <span data-ttu-id="ec3ce-341">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-341">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span></span>
* <span data-ttu-id="ec3ce-342">Set the URL to *jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-342">Set the URL to *jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="ec3ce-343">Enter your *username* and *password*.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-343">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="ec3ce-344">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-344">Click **OK**.</span></span>
* <span data-ttu-id="ec3ce-345">To open the **Connection** window, double-click the ***Spam database*** alias.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-345">To open the **Connection** window, double-click the ***Spam database*** alias.</span></span>
* <span data-ttu-id="ec3ce-346">Select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-346">Select **Connect**.</span></span>

<span data-ttu-id="ec3ce-347">To run some queries:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-347">To run some queries:</span></span>

* <span data-ttu-id="ec3ce-348">Select the **SQL** tab.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-348">Select the **SQL** tab.</span></span>
* <span data-ttu-id="ec3ce-349">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-349">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span></span>
* <span data-ttu-id="ec3ce-350">Press **Ctrl-Enter** to run it.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-350">Press **Ctrl-Enter** to run it.</span></span> <span data-ttu-id="ec3ce-351">By default Squirrel SQL returns the first 100 rows from your query.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-351">By default Squirrel SQL returns the first 100 rows from your query.</span></span>

<span data-ttu-id="ec3ce-352">There are many more queries you could run to explore this data.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-352">There are many more queries you could run to explore this data.</span></span> <span data-ttu-id="ec3ce-353">For example, how does the frequency of the word *make* differ between spam and ham?</span><span class="sxs-lookup"><span data-stu-id="ec3ce-353">For example, how does the frequency of the word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="ec3ce-354">Or what are the characteristics of email that frequently contain *3d*?</span><span class="sxs-lookup"><span data-stu-id="ec3ce-354">Or what are the characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="ec3ce-355">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-355">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span></span>

<span data-ttu-id="ec3ce-356">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-356">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="ec3ce-357">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ec3ce-357">SQL Server Data Warehouse</span></span>
<span data-ttu-id="ec3ce-358">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-358">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="ec3ce-359">For more information, see [What is Azure SQL Data Warehouse?](../../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="ec3ce-359">For more information, see [What is Azure SQL Data Warehouse?](../../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="ec3ce-360">To connect to the data warehouse and create the table, run the following command from a command prompt:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-360">To connect to the data warehouse and create the table, run the following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="ec3ce-361">Then at the sqlcmd prompt:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-361">Then at the sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="ec3ce-362">Copy data with bcp:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-362">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="ec3ce-363">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-363">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span></span>
>
>

<span data-ttu-id="ec3ce-364">And query with sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="ec3ce-364">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="ec3ce-365">You could also query with Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-365">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="ec3ce-366">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-366">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec3ce-367">Next steps</span><span class="sxs-lookup"><span data-stu-id="ec3ce-367">Next steps</span></span>
<span data-ttu-id="ec3ce-368">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-368">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="ec3ce-369">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](../team-data-science-process/walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="ec3ce-369">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](../team-data-science-process/walkthroughs.md).</span></span> <span data-ttu-id="ec3ce-370">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span><span class="sxs-lookup"><span data-stu-id="ec3ce-370">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>
