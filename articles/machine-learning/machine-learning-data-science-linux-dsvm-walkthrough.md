---
title: Data science on the Linux Data Science Virtual Machine | Microsoft Docs
description: How to perform several common data science tasks with the Linux Data Science VM.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: a2d1b97802869021fbc3163f2d802c0f635c5126
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552176"
---
# <a name="data-science-on-the-linux-data-science-virtual-machine"></a><span data-ttu-id="a72ea-103">Data science on the Linux Data Science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="a72ea-103">Data science on the Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="a72ea-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="a72ea-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span></span> <span data-ttu-id="a72ea-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span><span class="sxs-lookup"><span data-stu-id="a72ea-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="a72ea-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span><span class="sxs-lookup"><span data-stu-id="a72ea-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="a72ea-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span><span class="sxs-lookup"><span data-stu-id="a72ea-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span></span> <span data-ttu-id="a72ea-108">You can easily scale up the VM, if needed, and stop it when not in use.</span><span class="sxs-lookup"><span data-stu-id="a72ea-108">You can easily scale up the VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="a72ea-109">So this resource is both elastic and cost-efficient.</span><span class="sxs-lookup"><span data-stu-id="a72ea-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="a72ea-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="a72ea-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="a72ea-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span><span class="sxs-lookup"><span data-stu-id="a72ea-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span></span> <span data-ttu-id="a72ea-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span><span class="sxs-lookup"><span data-stu-id="a72ea-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="a72ea-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="a72ea-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="a72ea-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span><span class="sxs-lookup"><span data-stu-id="a72ea-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span></span> <span data-ttu-id="a72ea-115">The statistics included are discussed in the next but one section.</span><span class="sxs-lookup"><span data-stu-id="a72ea-115">The statistics included are discussed in the next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a72ea-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a72ea-116">Prerequisites</span></span>
<span data-ttu-id="a72ea-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="a72ea-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span></span>

* <span data-ttu-id="a72ea-118">An **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-118">An **Azure subscription**.</span></span> <span data-ttu-id="a72ea-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a72ea-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="a72ea-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="a72ea-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="a72ea-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="a72ea-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="a72ea-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span><span class="sxs-lookup"><span data-stu-id="a72ea-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="a72ea-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="a72ea-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="a72ea-124">An **AzureML account**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-124">An **AzureML account**.</span></span> <span data-ttu-id="a72ea-125">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="a72ea-125">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="a72ea-126">There is a free usage tier to help you get started.</span><span class="sxs-lookup"><span data-stu-id="a72ea-126">There is a free usage tier to help you get started.</span></span>

## <a name="download-the-spambase-dataset"></a><span data-ttu-id="a72ea-127">Download the spambase dataset</span><span class="sxs-lookup"><span data-stu-id="a72ea-127">Download the spambase dataset</span></span>
<span data-ttu-id="a72ea-128">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span><span class="sxs-lookup"><span data-stu-id="a72ea-128">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="a72ea-129">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span><span class="sxs-lookup"><span data-stu-id="a72ea-129">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="a72ea-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="a72ea-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="a72ea-131">This size DSVM is capable of handling the procedures in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="a72ea-131">This size DSVM is capable of handling the procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="a72ea-132">If you need more storage space, you can create additional disks and attach them to your VM.</span><span class="sxs-lookup"><span data-stu-id="a72ea-132">If you need more storage space, you can create additional disks and attach them to your VM.</span></span> <span data-ttu-id="a72ea-133">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span><span class="sxs-lookup"><span data-stu-id="a72ea-133">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span></span> <span data-ttu-id="a72ea-134">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a72ea-134">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a72ea-135">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="a72ea-135">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span></span> <span data-ttu-id="a72ea-136">So these procedures can be done entirely from the VM itself.</span><span class="sxs-lookup"><span data-stu-id="a72ea-136">So these procedures can be done entirely from the VM itself.</span></span> <span data-ttu-id="a72ea-137">Another option to increase storage is to use [Azure files](../storage/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a72ea-137">Another option to increase storage is to use [Azure files](../storage/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="a72ea-138">To download the data, open a terminal window and run this command:</span><span class="sxs-lookup"><span data-stu-id="a72ea-138">To download the data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="a72ea-139">The downloaded file does not have a header row, so let's create another file that does have a header.</span><span class="sxs-lookup"><span data-stu-id="a72ea-139">The downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="a72ea-140">Run this command to create a file with the appropriate headers:</span><span class="sxs-lookup"><span data-stu-id="a72ea-140">Run this command to create a file with the appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="a72ea-141">Then concatenate the two files together with the command:</span><span class="sxs-lookup"><span data-stu-id="a72ea-141">Then concatenate the two files together with the command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="a72ea-142">The dataset has several types of statistics on each email:</span><span class="sxs-lookup"><span data-stu-id="a72ea-142">The dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="a72ea-143">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span><span class="sxs-lookup"><span data-stu-id="a72ea-143">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span></span> <span data-ttu-id="a72ea-144">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span><span class="sxs-lookup"><span data-stu-id="a72ea-144">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span></span>
* <span data-ttu-id="a72ea-145">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="a72ea-145">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span></span>
* <span data-ttu-id="a72ea-146">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span><span class="sxs-lookup"><span data-stu-id="a72ea-146">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="a72ea-147">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span><span class="sxs-lookup"><span data-stu-id="a72ea-147">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="a72ea-148">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span><span class="sxs-lookup"><span data-stu-id="a72ea-148">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="a72ea-149">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span><span class="sxs-lookup"><span data-stu-id="a72ea-149">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-the-dataset-with-microsoft-r-open"></a><span data-ttu-id="a72ea-150">Explore the dataset with Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="a72ea-150">Explore the dataset with Microsoft R Open</span></span>
<span data-ttu-id="a72ea-151">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span><span class="sxs-lookup"><span data-stu-id="a72ea-151">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="a72ea-152">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span><span class="sxs-lookup"><span data-stu-id="a72ea-152">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="a72ea-153">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span><span class="sxs-lookup"><span data-stu-id="a72ea-153">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span></span>

<span data-ttu-id="a72ea-154">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span><span class="sxs-lookup"><span data-stu-id="a72ea-154">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span></span> <span data-ttu-id="a72ea-155">From the git command line, run:</span><span class="sxs-lookup"><span data-stu-id="a72ea-155">From the git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="a72ea-156">Open a terminal window and start a new R session with the R interactive console.</span><span class="sxs-lookup"><span data-stu-id="a72ea-156">Open a terminal window and start a new R session with the R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="a72ea-157">You can also use RStudio for the following procedures.</span><span class="sxs-lookup"><span data-stu-id="a72ea-157">You can also use RStudio for the following procedures.</span></span> <span data-ttu-id="a72ea-158">To install RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="a72ea-158">To install RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="a72ea-159">To import the data and set up the environment, run:</span><span class="sxs-lookup"><span data-stu-id="a72ea-159">To import the data and set up the environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="a72ea-160">To see summary statistics about each column:</span><span class="sxs-lookup"><span data-stu-id="a72ea-160">To see summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="a72ea-161">For a different view of the data:</span><span class="sxs-lookup"><span data-stu-id="a72ea-161">For a different view of the data:</span></span>

    str(data)

<span data-ttu-id="a72ea-162">This shows you the type of each variable and the first few values in the dataset.</span><span class="sxs-lookup"><span data-stu-id="a72ea-162">This shows you the type of each variable and the first few values in the dataset.</span></span>

<span data-ttu-id="a72ea-163">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span><span class="sxs-lookup"><span data-stu-id="a72ea-163">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="a72ea-164">To set its type:</span><span class="sxs-lookup"><span data-stu-id="a72ea-164">To set its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="a72ea-165">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span><span class="sxs-lookup"><span data-stu-id="a72ea-165">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span></span> <span data-ttu-id="a72ea-166">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span><span class="sxs-lookup"><span data-stu-id="a72ea-166">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span></span> <span data-ttu-id="a72ea-167">Let's plot those frequencies here with the following commands:</span><span class="sxs-lookup"><span data-stu-id="a72ea-167">Let's plot those frequencies here with the following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="a72ea-168">Since the zero bar is skewing the plot, let's get rid of it:</span><span class="sxs-lookup"><span data-stu-id="a72ea-168">Since the zero bar is skewing the plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="a72ea-169">There is a non-trivial density above 1 that looks interesting.</span><span class="sxs-lookup"><span data-stu-id="a72ea-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="a72ea-170">Let's look at just that data:</span><span class="sxs-lookup"><span data-stu-id="a72ea-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="a72ea-171">Then split it by spam vs ham:</span><span class="sxs-lookup"><span data-stu-id="a72ea-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="a72ea-172">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span><span class="sxs-lookup"><span data-stu-id="a72ea-172">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="a72ea-173">Train and test an ML model</span><span class="sxs-lookup"><span data-stu-id="a72ea-173">Train and test an ML model</span></span>
<span data-ttu-id="a72ea-174">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span><span class="sxs-lookup"><span data-stu-id="a72ea-174">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span></span> <span data-ttu-id="a72ea-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span><span class="sxs-lookup"><span data-stu-id="a72ea-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="a72ea-176">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="a72ea-176">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span></span>
>
>

<span data-ttu-id="a72ea-177">First, let's split the dataset into training and test sets:</span><span class="sxs-lookup"><span data-stu-id="a72ea-177">First, let's split the dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="a72ea-178">And then create a decision tree to classify the emails.</span><span class="sxs-lookup"><span data-stu-id="a72ea-178">And then create a decision tree to classify the emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="a72ea-179">Here is the result:</span><span class="sxs-lookup"><span data-stu-id="a72ea-179">Here is the result:</span></span>

![1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="a72ea-181">To determine how well it performs on the training set, use the following code:</span><span class="sxs-lookup"><span data-stu-id="a72ea-181">To determine how well it performs on the training set, use the following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="a72ea-182">To determine how well it performs on the test set:</span><span class="sxs-lookup"><span data-stu-id="a72ea-182">To determine how well it performs on the test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="a72ea-183">Let's also try a random forest model.</span><span class="sxs-lookup"><span data-stu-id="a72ea-183">Let's also try a random forest model.</span></span> <span data-ttu-id="a72ea-184">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span><span class="sxs-lookup"><span data-stu-id="a72ea-184">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span></span> <span data-ttu-id="a72ea-185">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span><span class="sxs-lookup"><span data-stu-id="a72ea-185">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-to-azure-ml"></a><span data-ttu-id="a72ea-186">Deploy a model to Azure ML</span><span class="sxs-lookup"><span data-stu-id="a72ea-186">Deploy a model to Azure ML</span></span>
<span data-ttu-id="a72ea-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span><span class="sxs-lookup"><span data-stu-id="a72ea-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span></span> <span data-ttu-id="a72ea-188">One of the nice features of AzureML is its ability to publish any R function as a web service.</span><span class="sxs-lookup"><span data-stu-id="a72ea-188">One of the nice features of AzureML is its ability to publish any R function as a web service.</span></span> <span data-ttu-id="a72ea-189">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="a72ea-189">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span></span>

<span data-ttu-id="a72ea-190">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="a72ea-190">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span></span> <span data-ttu-id="a72ea-191">You need your workspace ID and an authorization token to sign in.</span><span class="sxs-lookup"><span data-stu-id="a72ea-191">You need your workspace ID and an authorization token to sign in.</span></span> <span data-ttu-id="a72ea-192">To find these values and initialize the AzureML variables with them:</span><span class="sxs-lookup"><span data-stu-id="a72ea-192">To find these values and initialize the AzureML variables with them:</span></span>

<span data-ttu-id="a72ea-193">Select **Settings** on the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="a72ea-193">Select **Settings** on the left-hand menu.</span></span> <span data-ttu-id="a72ea-194">Note your **WORKSPACE ID**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="a72ea-195">![2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="a72ea-195">![2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="a72ea-196">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="a72ea-196">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="a72ea-197">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span><span class="sxs-lookup"><span data-stu-id="a72ea-197">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="a72ea-198">Let's simplify the model to make this demonstration easier to implement.</span><span class="sxs-lookup"><span data-stu-id="a72ea-198">Let's simplify the model to make this demonstration easier to implement.</span></span> <span data-ttu-id="a72ea-199">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span><span class="sxs-lookup"><span data-stu-id="a72ea-199">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="a72ea-200">We need a prediction function that takes the features as an input and returns the predicted values:</span><span class="sxs-lookup"><span data-stu-id="a72ea-200">We need a prediction function that takes the features as an input and returns the predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="a72ea-201">Publish the predictSpam function to AzureML using the **publishWebService** function:</span><span class="sxs-lookup"><span data-stu-id="a72ea-201">Publish the predictSpam function to AzureML using the **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="a72ea-202">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="a72ea-202">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span></span>

<span data-ttu-id="a72ea-203">View details of the published web service, including its API endpoint and access keys with the command:</span><span class="sxs-lookup"><span data-stu-id="a72ea-203">View details of the published web service, including its API endpoint and access keys with the command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="a72ea-204">To try it out on the first 10 rows of the test set:</span><span class="sxs-lookup"><span data-stu-id="a72ea-204">To try it out on the first 10 rows of the test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="a72ea-205">Use other tools available</span><span class="sxs-lookup"><span data-stu-id="a72ea-205">Use other tools available</span></span>
<span data-ttu-id="a72ea-206">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span><span class="sxs-lookup"><span data-stu-id="a72ea-206">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span></span>

* <span data-ttu-id="a72ea-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="a72ea-207">XGBoost</span></span>
* <span data-ttu-id="a72ea-208">Python</span><span class="sxs-lookup"><span data-stu-id="a72ea-208">Python</span></span>
* <span data-ttu-id="a72ea-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="a72ea-209">Jupyterhub</span></span>
* <span data-ttu-id="a72ea-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="a72ea-210">Rattle</span></span>
* <span data-ttu-id="a72ea-211">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="a72ea-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="a72ea-212">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a72ea-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="a72ea-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="a72ea-213">XGBoost</span></span>
<span data-ttu-id="a72ea-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span><span class="sxs-lookup"><span data-stu-id="a72ea-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

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

<span data-ttu-id="a72ea-215">XGBoost can also call from python or a command line.</span><span class="sxs-lookup"><span data-stu-id="a72ea-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="a72ea-216">Python</span><span class="sxs-lookup"><span data-stu-id="a72ea-216">Python</span></span>
<span data-ttu-id="a72ea-217">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span><span class="sxs-lookup"><span data-stu-id="a72ea-217">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="a72ea-218">The Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span><span class="sxs-lookup"><span data-stu-id="a72ea-218">The Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="a72ea-219">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span><span class="sxs-lookup"><span data-stu-id="a72ea-219">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="a72ea-220">To make predictions:</span><span class="sxs-lookup"><span data-stu-id="a72ea-220">To make predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="a72ea-221">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span><span class="sxs-lookup"><span data-stu-id="a72ea-221">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="a72ea-222">To publish the model to AzureML:</span><span class="sxs-lookup"><span data-stu-id="a72ea-222">To publish the model to AzureML:</span></span>

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
> <span data-ttu-id="a72ea-223">This is only available for python 2.7 and is not yet supported on 3.5.</span><span class="sxs-lookup"><span data-stu-id="a72ea-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="a72ea-224">Run with **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="a72ea-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="a72ea-225">Jupyterhub</span></span>
<span data-ttu-id="a72ea-226">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span><span class="sxs-lookup"><span data-stu-id="a72ea-226">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="a72ea-227">The Jupyter notebook is accessed through JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="a72ea-227">The Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="a72ea-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="a72ea-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="a72ea-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="a72ea-230">Several sample notebooks are already installed on the VM:</span><span class="sxs-lookup"><span data-stu-id="a72ea-230">Several sample notebooks are already installed on the VM:</span></span>

* <span data-ttu-id="a72ea-231">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span><span class="sxs-lookup"><span data-stu-id="a72ea-231">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="a72ea-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span><span class="sxs-lookup"><span data-stu-id="a72ea-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="a72ea-233">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span><span class="sxs-lookup"><span data-stu-id="a72ea-233">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="a72ea-234">The Julia language is also available from the command line on the Linux Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="a72ea-234">The Julia language is also available from the command line on the Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="a72ea-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="a72ea-235">Rattle</span></span>
<span data-ttu-id="a72ea-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span><span class="sxs-lookup"><span data-stu-id="a72ea-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="a72ea-237">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span><span class="sxs-lookup"><span data-stu-id="a72ea-237">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="a72ea-238">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span><span class="sxs-lookup"><span data-stu-id="a72ea-238">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="a72ea-239">Install and start Rattle with the following commands:</span><span class="sxs-lookup"><span data-stu-id="a72ea-239">Install and start Rattle with the following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="a72ea-240">Installation is not required on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="a72ea-240">Installation is not required on the DSVM.</span></span> <span data-ttu-id="a72ea-241">But Rattle may prompt you to install additional packages when it loads.</span><span class="sxs-lookup"><span data-stu-id="a72ea-241">But Rattle may prompt you to install additional packages when it loads.</span></span>
>
>

<span data-ttu-id="a72ea-242">Rattle uses a tab-based interface.</span><span class="sxs-lookup"><span data-stu-id="a72ea-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="a72ea-243">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span><span class="sxs-lookup"><span data-stu-id="a72ea-243">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="a72ea-244">The data science process flows from left to right through the tabs.</span><span class="sxs-lookup"><span data-stu-id="a72ea-244">The data science process flows from left to right through the tabs.</span></span> <span data-ttu-id="a72ea-245">But the last tab contains a log of the R commands run by Rattle.</span><span class="sxs-lookup"><span data-stu-id="a72ea-245">But the last tab contains a log of the R commands run by Rattle.</span></span>

<span data-ttu-id="a72ea-246">To load and configure the dataset:</span><span class="sxs-lookup"><span data-stu-id="a72ea-246">To load and configure the dataset:</span></span>

* <span data-ttu-id="a72ea-247">To load the file, select the **Data** tab, then</span><span class="sxs-lookup"><span data-stu-id="a72ea-247">To load the file, select the **Data** tab, then</span></span>
* <span data-ttu-id="a72ea-248">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-248">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="a72ea-249">To load the file.</span><span class="sxs-lookup"><span data-stu-id="a72ea-249">To load the file.</span></span> <span data-ttu-id="a72ea-250">select **Execute** in the top row of buttons.</span><span class="sxs-lookup"><span data-stu-id="a72ea-250">select **Execute** in the top row of buttons.</span></span> <span data-ttu-id="a72ea-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span><span class="sxs-lookup"><span data-stu-id="a72ea-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span></span>
* <span data-ttu-id="a72ea-252">Rattle has correctly identified the **spam** column as the target.</span><span class="sxs-lookup"><span data-stu-id="a72ea-252">Rattle has correctly identified the **spam** column as the target.</span></span> <span data-ttu-id="a72ea-253">Select the spam column, then set the **Target Data Type** to **Categoric**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-253">Select the spam column, then set the **Target Data Type** to **Categoric**.</span></span>

<span data-ttu-id="a72ea-254">To explore the data:</span><span class="sxs-lookup"><span data-stu-id="a72ea-254">To explore the data:</span></span>

* <span data-ttu-id="a72ea-255">Select the **Explore** tab.</span><span class="sxs-lookup"><span data-stu-id="a72ea-255">Select the **Explore** tab.</span></span>
* <span data-ttu-id="a72ea-256">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span><span class="sxs-lookup"><span data-stu-id="a72ea-256">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span></span>
* <span data-ttu-id="a72ea-257">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-257">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="a72ea-258">The **Explore** tab also allows you to generate many insightful plots.</span><span class="sxs-lookup"><span data-stu-id="a72ea-258">The **Explore** tab also allows you to generate many insightful plots.</span></span> <span data-ttu-id="a72ea-259">To plot a histogram of the data:</span><span class="sxs-lookup"><span data-stu-id="a72ea-259">To plot a histogram of the data:</span></span>

* <span data-ttu-id="a72ea-260">Select **Distributions**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-260">Select **Distributions**.</span></span>
* <span data-ttu-id="a72ea-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="a72ea-262">Select **Execute**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-262">Select **Execute**.</span></span> <span data-ttu-id="a72ea-263">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span><span class="sxs-lookup"><span data-stu-id="a72ea-263">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="a72ea-264">The Correlation plots are also interesting.</span><span class="sxs-lookup"><span data-stu-id="a72ea-264">The Correlation plots are also interesting.</span></span> <span data-ttu-id="a72ea-265">To create one:</span><span class="sxs-lookup"><span data-stu-id="a72ea-265">To create one:</span></span>

* <span data-ttu-id="a72ea-266">Choose **Correlation** as the **Type**, then</span><span class="sxs-lookup"><span data-stu-id="a72ea-266">Choose **Correlation** as the **Type**, then</span></span>
* <span data-ttu-id="a72ea-267">Select **Execute**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-267">Select **Execute**.</span></span>
* <span data-ttu-id="a72ea-268">Rattle warns you that it recommends a maximum of 40 variables.</span><span class="sxs-lookup"><span data-stu-id="a72ea-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="a72ea-269">Select **Yes** to view the plot.</span><span class="sxs-lookup"><span data-stu-id="a72ea-269">Select **Yes** to view the plot.</span></span>

<span data-ttu-id="a72ea-270">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span><span class="sxs-lookup"><span data-stu-id="a72ea-270">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span></span> <span data-ttu-id="a72ea-271">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span><span class="sxs-lookup"><span data-stu-id="a72ea-271">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span></span>

<span data-ttu-id="a72ea-272">The numeric values for the correlations between words are available in the Explore window.</span><span class="sxs-lookup"><span data-stu-id="a72ea-272">The numeric values for the correlations between words are available in the Explore window.</span></span> <span data-ttu-id="a72ea-273">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span><span class="sxs-lookup"><span data-stu-id="a72ea-273">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="a72ea-274">Rattle can transform the dataset to handle some common issues.</span><span class="sxs-lookup"><span data-stu-id="a72ea-274">Rattle can transform the dataset to handle some common issues.</span></span> <span data-ttu-id="a72ea-275">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span><span class="sxs-lookup"><span data-stu-id="a72ea-275">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="a72ea-276">Rattle can also identify association rules between observations and/or variables.</span><span class="sxs-lookup"><span data-stu-id="a72ea-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="a72ea-277">These tabs are out of scope for this introductory walkthrough.</span><span class="sxs-lookup"><span data-stu-id="a72ea-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="a72ea-278">Rattle can also perform cluster analysis.</span><span class="sxs-lookup"><span data-stu-id="a72ea-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="a72ea-279">Let's exclude some features to make the output easier to read.</span><span class="sxs-lookup"><span data-stu-id="a72ea-279">Let's exclude some features to make the output easier to read.</span></span> <span data-ttu-id="a72ea-280">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span><span class="sxs-lookup"><span data-stu-id="a72ea-280">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span></span>

* <span data-ttu-id="a72ea-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="a72ea-281">word_freq_hp</span></span>
* <span data-ttu-id="a72ea-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="a72ea-282">word_freq_technology</span></span>
* <span data-ttu-id="a72ea-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="a72ea-283">word_freq_george</span></span>
* <span data-ttu-id="a72ea-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="a72ea-284">word_freq_remove</span></span>
* <span data-ttu-id="a72ea-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="a72ea-285">word_freq_your</span></span>
* <span data-ttu-id="a72ea-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="a72ea-286">word_freq_dollar</span></span>
* <span data-ttu-id="a72ea-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="a72ea-287">word_freq_money</span></span>
* <span data-ttu-id="a72ea-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="a72ea-288">capital_run_length_longest</span></span>
* <span data-ttu-id="a72ea-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="a72ea-289">word_freq_business</span></span>
* <span data-ttu-id="a72ea-290">spam</span><span class="sxs-lookup"><span data-stu-id="a72ea-290">spam</span></span>

<span data-ttu-id="a72ea-291">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span><span class="sxs-lookup"><span data-stu-id="a72ea-291">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span></span> <span data-ttu-id="a72ea-292">Then **Execute**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-292">Then **Execute**.</span></span> <span data-ttu-id="a72ea-293">The results are displayed in the output window.</span><span class="sxs-lookup"><span data-stu-id="a72ea-293">The results are displayed in the output window.</span></span> <span data-ttu-id="a72ea-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span><span class="sxs-lookup"><span data-stu-id="a72ea-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="a72ea-295">To build a simple decision tree machine learning model:</span><span class="sxs-lookup"><span data-stu-id="a72ea-295">To build a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="a72ea-296">Select the **Model** tab,</span><span class="sxs-lookup"><span data-stu-id="a72ea-296">Select the **Model** tab,</span></span>
* <span data-ttu-id="a72ea-297">Choose **Tree** as the **Type**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-297">Choose **Tree** as the **Type**.</span></span>
* <span data-ttu-id="a72ea-298">Select **Execute** to display the tree in text form in the output window.</span><span class="sxs-lookup"><span data-stu-id="a72ea-298">Select **Execute** to display the tree in text form in the output window.</span></span>
* <span data-ttu-id="a72ea-299">Select the **Draw** button to view a graphical version.</span><span class="sxs-lookup"><span data-stu-id="a72ea-299">Select the **Draw** button to view a graphical version.</span></span> <span data-ttu-id="a72ea-300">This looks quite similar to the tree we obtained earlier using *rpart*.</span><span class="sxs-lookup"><span data-stu-id="a72ea-300">This looks quite similar to the tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="a72ea-301">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span><span class="sxs-lookup"><span data-stu-id="a72ea-301">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="a72ea-302">Here is the procedure:</span><span class="sxs-lookup"><span data-stu-id="a72ea-302">Here is the procedure:</span></span>

* <span data-ttu-id="a72ea-303">Choose **All** for the **Type**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-303">Choose **All** for the **Type**.</span></span>
* <span data-ttu-id="a72ea-304">Select **Execute**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-304">Select **Execute**.</span></span>
* <span data-ttu-id="a72ea-305">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span><span class="sxs-lookup"><span data-stu-id="a72ea-305">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span></span>
* <span data-ttu-id="a72ea-306">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span><span class="sxs-lookup"><span data-stu-id="a72ea-306">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span></span>
* <span data-ttu-id="a72ea-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span><span class="sxs-lookup"><span data-stu-id="a72ea-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="a72ea-308">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span><span class="sxs-lookup"><span data-stu-id="a72ea-308">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span></span> <span data-ttu-id="a72ea-309">You can select the **Export** button to save it.</span><span class="sxs-lookup"><span data-stu-id="a72ea-309">You can select the **Export** button to save it.</span></span>

> [!NOTE]
> <span data-ttu-id="a72ea-310">There is a bug in current release of Rattle.</span><span class="sxs-lookup"><span data-stu-id="a72ea-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="a72ea-311">To modify the script or use it to repeat your steps later, you must insert a # character in front of \*Export this log ... \* in the text of the log.</span><span class="sxs-lookup"><span data-stu-id="a72ea-311">To modify the script or use it to repeat your steps later, you must insert a # character in front of \*Export this log ... \* in the text of the log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="a72ea-312">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="a72ea-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="a72ea-313">The DSVM comes with PostgreSQL installed.</span><span class="sxs-lookup"><span data-stu-id="a72ea-313">The DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="a72ea-314">PostgreSQL is a sophisticated, open-source relational database.</span><span class="sxs-lookup"><span data-stu-id="a72ea-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="a72ea-315">This section shows how to load our spam dataset into PostgreSQL and then query it.</span><span class="sxs-lookup"><span data-stu-id="a72ea-315">This section shows how to load our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="a72ea-316">Before you can load the data, you need to allow password authentication from the localhost.</span><span class="sxs-lookup"><span data-stu-id="a72ea-316">Before you can load the data, you need to allow password authentication from the localhost.</span></span> <span data-ttu-id="a72ea-317">At a command prompt:</span><span class="sxs-lookup"><span data-stu-id="a72ea-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="a72ea-318">Near the bottom of the config file are several lines that detail the allowed connections:</span><span class="sxs-lookup"><span data-stu-id="a72ea-318">Near the bottom of the config file are several lines that detail the allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="a72ea-319">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span><span class="sxs-lookup"><span data-stu-id="a72ea-319">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="a72ea-320">And restart the postgres service:</span><span class="sxs-lookup"><span data-stu-id="a72ea-320">And restart the postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="a72ea-321">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span><span class="sxs-lookup"><span data-stu-id="a72ea-321">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="a72ea-322">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span><span class="sxs-lookup"><span data-stu-id="a72ea-322">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="a72ea-323">Then log in to psql as your user:</span><span class="sxs-lookup"><span data-stu-id="a72ea-323">Then log in to psql as your user:</span></span>

    psql

<span data-ttu-id="a72ea-324">And import the data into a new database:</span><span class="sxs-lookup"><span data-stu-id="a72ea-324">And import the data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="a72ea-325">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span><span class="sxs-lookup"><span data-stu-id="a72ea-325">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="a72ea-326">To get started, launch Squirrel SQL from the Applications menu.</span><span class="sxs-lookup"><span data-stu-id="a72ea-326">To get started, launch Squirrel SQL from the Applications menu.</span></span> <span data-ttu-id="a72ea-327">To set up the driver:</span><span class="sxs-lookup"><span data-stu-id="a72ea-327">To set up the driver:</span></span>

* <span data-ttu-id="a72ea-328">Select **Windows**, then **View Drivers**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="a72ea-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="a72ea-330">Select **Extra Class Path**, then **Add**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="a72ea-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span><span class="sxs-lookup"><span data-stu-id="a72ea-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span></span>
* <span data-ttu-id="a72ea-332">Select **Open**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-332">Select **Open**.</span></span>
* <span data-ttu-id="a72ea-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="a72ea-334">To set up the connection to the local server:</span><span class="sxs-lookup"><span data-stu-id="a72ea-334">To set up the connection to the local server:</span></span>

* <span data-ttu-id="a72ea-335">Select **Windows**, then **View Aliases.**</span><span class="sxs-lookup"><span data-stu-id="a72ea-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="a72ea-336">Choose the **+** button to make a new alias.</span><span class="sxs-lookup"><span data-stu-id="a72ea-336">Choose the **+** button to make a new alias.</span></span>
* <span data-ttu-id="a72ea-337">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span><span class="sxs-lookup"><span data-stu-id="a72ea-337">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span></span>
* <span data-ttu-id="a72ea-338">Set the URL to *jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="a72ea-338">Set the URL to *jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="a72ea-339">Enter your *username* and *password*.</span><span class="sxs-lookup"><span data-stu-id="a72ea-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="a72ea-340">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-340">Click **OK**.</span></span>
* <span data-ttu-id="a72ea-341">To open the **Connection** window, double-click the ***Spam database*** alias.</span><span class="sxs-lookup"><span data-stu-id="a72ea-341">To open the **Connection** window, double-click the ***Spam database*** alias.</span></span>
* <span data-ttu-id="a72ea-342">Select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a72ea-342">Select **Connect**.</span></span>

<span data-ttu-id="a72ea-343">To run some queries:</span><span class="sxs-lookup"><span data-stu-id="a72ea-343">To run some queries:</span></span>

* <span data-ttu-id="a72ea-344">Select the **SQL** tab.</span><span class="sxs-lookup"><span data-stu-id="a72ea-344">Select the **SQL** tab.</span></span>
* <span data-ttu-id="a72ea-345">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span><span class="sxs-lookup"><span data-stu-id="a72ea-345">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span></span>
* <span data-ttu-id="a72ea-346">Press **Ctrl-Enter** to run it.</span><span class="sxs-lookup"><span data-stu-id="a72ea-346">Press **Ctrl-Enter** to run it.</span></span> <span data-ttu-id="a72ea-347">By default Squirrel SQL returns the first 100 rows from your query.</span><span class="sxs-lookup"><span data-stu-id="a72ea-347">By default Squirrel SQL returns the first 100 rows from your query.</span></span>

<span data-ttu-id="a72ea-348">There are many more queries you could run to explore this data.</span><span class="sxs-lookup"><span data-stu-id="a72ea-348">There are many more queries you could run to explore this data.</span></span> <span data-ttu-id="a72ea-349">For example, how does the frequency of the word *make* differ between spam and ham?</span><span class="sxs-lookup"><span data-stu-id="a72ea-349">For example, how does the frequency of the word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="a72ea-350">Or what are the characteristics of email that frequently contain *3d*?</span><span class="sxs-lookup"><span data-stu-id="a72ea-350">Or what are the characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="a72ea-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span><span class="sxs-lookup"><span data-stu-id="a72ea-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span></span>

<span data-ttu-id="a72ea-352">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="a72ea-352">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="a72ea-353">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a72ea-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="a72ea-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span><span class="sxs-lookup"><span data-stu-id="a72ea-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="a72ea-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="a72ea-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="a72ea-356">To connect to the data warehouse and create the table, run the following command from a command prompt:</span><span class="sxs-lookup"><span data-stu-id="a72ea-356">To connect to the data warehouse and create the table, run the following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="a72ea-357">Then at the sqlcmd prompt:</span><span class="sxs-lookup"><span data-stu-id="a72ea-357">Then at the sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="a72ea-358">Copy data with bcp:</span><span class="sxs-lookup"><span data-stu-id="a72ea-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="a72ea-359">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span><span class="sxs-lookup"><span data-stu-id="a72ea-359">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span></span>
>
>

<span data-ttu-id="a72ea-360">And query with sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="a72ea-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="a72ea-361">You could also query with Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="a72ea-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="a72ea-362">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="a72ea-362">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a72ea-363">Next steps</span><span class="sxs-lookup"><span data-stu-id="a72ea-363">Next steps</span></span>
<span data-ttu-id="a72ea-364">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="a72ea-364">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="a72ea-365">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="a72ea-365">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="a72ea-366">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span><span class="sxs-lookup"><span data-stu-id="a72ea-366">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>



