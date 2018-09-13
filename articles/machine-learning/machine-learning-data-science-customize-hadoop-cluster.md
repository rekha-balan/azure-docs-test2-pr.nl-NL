---
title: Customize Hadoop clusters for the Team Data Science Process | Microsoft Docs
description: Popular Python modules made available in custom Azure HDInsight Hadoop clusters.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 7f8414c954aa7e601092f5ae658a8ff24f526f66
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670705"
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-the-team-data-science-process"></a><span data-ttu-id="02dc3-103">Customize Azure HDInsight Hadoop clusters for the Team Data Science Process</span><span class="sxs-lookup"><span data-stu-id="02dc3-103">Customize Azure HDInsight Hadoop clusters for the Team Data Science Process</span></span>
<span data-ttu-id="02dc3-104">This article describes how to customize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when the cluster is provisioned as an HDInsight service.</span><span class="sxs-lookup"><span data-stu-id="02dc3-104">This article describes how to customize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when the cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="02dc3-105">It also shows how to access the headnode to submit custom jobs to the cluster.</span><span class="sxs-lookup"><span data-stu-id="02dc3-105">It also shows how to access the headnode to submit custom jobs to the cluster.</span></span> <span data-ttu-id="02dc3-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed to process Hive records in the cluster.</span><span class="sxs-lookup"><span data-stu-id="02dc3-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed to process Hive records in the cluster.</span></span> <span data-ttu-id="02dc3-107">For instructions on the procedures used in this scenario, see [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="02dc3-107">For instructions on the procedures used in this scenario, see [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="02dc3-108">The following menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02dc3-108">The following menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a><span data-ttu-id="02dc3-109">Customize Azure HDInsight Hadoop Cluster</span><span class="sxs-lookup"><span data-stu-id="02dc3-109">Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="02dc3-110">To create a customized HDInsight Hadoop cluster, start by logging on to [**Azure classic portal**](https://manage.windowsazure.com/), click **New** at the left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** to bring up the **Cluster Details** window.</span><span class="sxs-lookup"><span data-stu-id="02dc3-110">To create a customized HDInsight Hadoop cluster, start by logging on to [**Azure classic portal**](https://manage.windowsazure.com/), click **New** at the left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** to bring up the **Cluster Details** window.</span></span> 

![Create workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="02dc3-112">Input the name of the cluster to be created on configuration page 1, and accept default values for the other fields.</span><span class="sxs-lookup"><span data-stu-id="02dc3-112">Input the name of the cluster to be created on configuration page 1, and accept default values for the other fields.</span></span> <span data-ttu-id="02dc3-113">Click the arrow to go to the next configuration page.</span><span class="sxs-lookup"><span data-stu-id="02dc3-113">Click the arrow to go to the next configuration page.</span></span> 

![Create workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="02dc3-115">On configuration page 2, input the number of **DATA NODES**, select the **REGION/VIRTUAL NETWORK**, and select the sizes of the **HEAD NODE** and the **DATA NODE**.</span><span class="sxs-lookup"><span data-stu-id="02dc3-115">On configuration page 2, input the number of **DATA NODES**, select the **REGION/VIRTUAL NETWORK**, and select the sizes of the **HEAD NODE** and the **DATA NODE**.</span></span> <span data-ttu-id="02dc3-116">Click the arrow to go to the next configuration page.</span><span class="sxs-lookup"><span data-stu-id="02dc3-116">Click the arrow to go to the next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="02dc3-117">The **REGION/VIRTUAL NETWORK** has to be the same as the region of the storage account that is going to be used for the HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="02dc3-117">The **REGION/VIRTUAL NETWORK** has to be the same as the region of the storage account that is going to be used for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="02dc3-118">Otherwise, in the fourth configuration page, the storage account will not appear on the dropdown list of **ACCOUNT NAME**.</span><span class="sxs-lookup"><span data-stu-id="02dc3-118">Otherwise, in the fourth configuration page, the storage account will not appear on the dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Create workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="02dc3-120">On configuration page 3, provide a user name and password for the HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="02dc3-120">On configuration page 3, provide a user name and password for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="02dc3-121">**Do not** select the *Enter the Hive/Oozie Metastore*.</span><span class="sxs-lookup"><span data-stu-id="02dc3-121">**Do not** select the *Enter the Hive/Oozie Metastore*.</span></span> <span data-ttu-id="02dc3-122">Then, click the arrow to go to the next configuration page.</span><span class="sxs-lookup"><span data-stu-id="02dc3-122">Then, click the arrow to go to the next configuration page.</span></span> 

![Create workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="02dc3-124">On configuration page 4, specify the storage account name, the default container of the HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="02dc3-124">On configuration page 4, specify the storage account name, the default container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="02dc3-125">If you select *Create default container* in the **DEFAULT CONTAINER** dropdown list, a container with the same name as the cluster will be created.</span><span class="sxs-lookup"><span data-stu-id="02dc3-125">If you select *Create default container* in the **DEFAULT CONTAINER** dropdown list, a container with the same name as the cluster will be created.</span></span> <span data-ttu-id="02dc3-126">Click the arrow to go to the last configuration page.</span><span class="sxs-lookup"><span data-stu-id="02dc3-126">Click the arrow to go to the last configuration page.</span></span>

![Create workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="02dc3-128">On the final **Script Actions** configuration page, click **add script action** button, and fill the text fields with the following values.</span><span class="sxs-lookup"><span data-stu-id="02dc3-128">On the final **Script Actions** configuration page, click **add script action** button, and fill the text fields with the following values.</span></span>

* <span data-ttu-id="02dc3-129">**NAME** - any string as the name of this script action</span><span class="sxs-lookup"><span data-stu-id="02dc3-129">**NAME** - any string as the name of this script action</span></span>
* <span data-ttu-id="02dc3-130">**NODE TYPE** - select **All nodes**</span><span class="sxs-lookup"><span data-stu-id="02dc3-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="02dc3-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="02dc3-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="02dc3-132">*publicscripts* is a public container in the storage account</span><span class="sxs-lookup"><span data-stu-id="02dc3-132">*publicscripts* is a public container in the storage account</span></span> 
  * <span data-ttu-id="02dc3-133">*getgoing* we use to share PowerShell script files to facilitate users' work in Azure</span><span class="sxs-lookup"><span data-stu-id="02dc3-133">*getgoing* we use to share PowerShell script files to facilitate users' work in Azure</span></span>
* <span data-ttu-id="02dc3-134">**PARAMETERS** - (leave blank)</span><span class="sxs-lookup"><span data-stu-id="02dc3-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="02dc3-135">Finally, click the check mark to start the creation of the customized HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="02dc3-135">Finally, click the check mark to start the creation of the customized HDInsight Hadoop cluster.</span></span> 

![Create workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a> <span data-ttu-id="02dc3-137">Access the Head Node of Hadoop Cluster</span><span class="sxs-lookup"><span data-stu-id="02dc3-137">Access the Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="02dc3-138">You must enable remote access to the Hadoop cluster in Azure before you can access the head node of the Hadoop cluster through RDP.</span><span class="sxs-lookup"><span data-stu-id="02dc3-138">You must enable remote access to the Hadoop cluster in Azure before you can access the head node of the Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="02dc3-139">Log in to the [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on the left, select your Hadoop cluster from the list of clusters, click the **CONFIGURATION** tab, and then click the **ENABLE REMOTE** icon at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="02dc3-139">Log in to the [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on the left, select your Hadoop cluster from the list of clusters, click the **CONFIGURATION** tab, and then click the **ENABLE REMOTE** icon at the bottom of the page.</span></span>
   
    ![Create workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="02dc3-141">In the **Configure Remote Desktop** window, enter the USER NAME and PASSWORD fields, and select the expiration date for remote access.</span><span class="sxs-lookup"><span data-stu-id="02dc3-141">In the **Configure Remote Desktop** window, enter the USER NAME and PASSWORD fields, and select the expiration date for remote access.</span></span> <span data-ttu-id="02dc3-142">Then click the check mark to enable the remote access to the head node of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="02dc3-142">Then click the check mark to enable the remote access to the head node of the Hadoop cluster.</span></span>
   
    ![Create workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="02dc3-144">The user name and password for the remote access are not the user name and password that you use when you created the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="02dc3-144">The user name and password for the remote access are not the user name and password that you use when you created the Hadoop cluster.</span></span> <span data-ttu-id="02dc3-145">This is a separate set of credentials.</span><span class="sxs-lookup"><span data-stu-id="02dc3-145">This is a separate set of credentials.</span></span> <span data-ttu-id="02dc3-146">Also, the expiration date of the remote access has to be within 7 days from the current date.</span><span class="sxs-lookup"><span data-stu-id="02dc3-146">Also, the expiration date of the remote access has to be within 7 days from the current date.</span></span>
> 
> 

<span data-ttu-id="02dc3-147">After remote access is enabled, click **CONNECT** at the bottom of the page to remote into the head node.</span><span class="sxs-lookup"><span data-stu-id="02dc3-147">After remote access is enabled, click **CONNECT** at the bottom of the page to remote into the head node.</span></span> <span data-ttu-id="02dc3-148">You log on to the head node of the Hadoop cluster by entering the credentials for the remote access user that you specified earlier.</span><span class="sxs-lookup"><span data-stu-id="02dc3-148">You log on to the head node of the Hadoop cluster by entering the credentials for the remote access user that you specified earlier.</span></span>

![Create workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="02dc3-150">The next steps in the advanced analytics process are mapped in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from the data with Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="02dc3-150">The next steps in the advanced analytics process are mapped in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

<span data-ttu-id="02dc3-151">See [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how to access the Python modules that are included in Anaconda from the head node of the cluster in user-defined functions (UDFs) that are used to process Hive records stored in the cluster.</span><span class="sxs-lookup"><span data-stu-id="02dc3-151">See [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how to access the Python modules that are included in Anaconda from the head node of the cluster in user-defined functions (UDFs) that are used to process Hive records stored in the cluster.</span></span>










