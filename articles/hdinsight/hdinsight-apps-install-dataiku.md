---
title: Install published application - Dataiku DDS - Azure HDInsight
description: Install and use the Dataiku DDS third-party Hadoop application.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: ashish
ms.openlocfilehash: 64a6f393498ca90675712747afc8f9befc4b932f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864321"
---
# <a name="install-published-application---dataiku-dds"></a><span data-ttu-id="d1917-103">Install published application - Dataiku DDS</span><span class="sxs-lookup"><span data-stu-id="d1917-103">Install published application - Dataiku DDS</span></span>

<span data-ttu-id="d1917-104">This article describes how to install and run the [Dataiku DDS](https://www.dataiku.com/) published Hadoop application on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1917-104">This article describes how to install and run the [Dataiku DDS](https://www.dataiku.com/) published Hadoop application on Azure HDInsight.</span></span> <span data-ttu-id="d1917-105">For an overview of the HDInsight application platform, and a list of available Independent Software Vendor (ISV) published applications, see [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d1917-105">For an overview of the HDInsight application platform, and a list of available Independent Software Vendor (ISV) published applications, see [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span></span> <span data-ttu-id="d1917-106">For instructions on installing your own application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d1917-106">For instructions on installing your own application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>

## <a name="about-dataiku-dss"></a><span data-ttu-id="d1917-107">About Dataiku DSS</span><span class="sxs-lookup"><span data-stu-id="d1917-107">About Dataiku DSS</span></span>

<span data-ttu-id="d1917-108">The Dataiku [Data Science Studio (DSS)](https://www.dataiku.com/dss/features/connectivity/), is a collaborative data science platform that enables data scientists to build and deliver analytical solutions.</span><span class="sxs-lookup"><span data-stu-id="d1917-108">The Dataiku [Data Science Studio (DSS)](https://www.dataiku.com/dss/features/connectivity/), is a collaborative data science platform that enables data scientists to build and deliver analytical solutions.</span></span> <span data-ttu-id="d1917-109">Offering DSS as an HDInsight application lets you use data science to build Big Data solutions and run them at enterprise grade and scale.</span><span class="sxs-lookup"><span data-stu-id="d1917-109">Offering DSS as an HDInsight application lets you use data science to build Big Data solutions and run them at enterprise grade and scale.</span></span>

<span data-ttu-id="d1917-110">You can use DSS to implement a complete analytical solution, beginning with data ingestion, preparation, and processing.</span><span class="sxs-lookup"><span data-stu-id="d1917-110">You can use DSS to implement a complete analytical solution, beginning with data ingestion, preparation, and processing.</span></span> <span data-ttu-id="d1917-111">A DSS solution can also include training and applying machine learning models, visualization, and then operationalizing.</span><span class="sxs-lookup"><span data-stu-id="d1917-111">A DSS solution can also include training and applying machine learning models, visualization, and then operationalizing.</span></span>

<span data-ttu-id="d1917-112">You can install DSS on HDInsight using Hadoop or Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="d1917-112">You can install DSS on HDInsight using Hadoop or Spark clusters.</span></span> <span data-ttu-id="d1917-113">You can install DSS on existing running clusters, or when creating new clusters.</span><span class="sxs-lookup"><span data-stu-id="d1917-113">You can install DSS on existing running clusters, or when creating new clusters.</span></span> <span data-ttu-id="d1917-114">DSS also supports using Azure Blob storage as a connector for reading data.</span><span class="sxs-lookup"><span data-stu-id="d1917-114">DSS also supports using Azure Blob storage as a connector for reading data.</span></span>

<span data-ttu-id="d1917-115">You can use DSS to build projects, which then can generate MapReduce or Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="d1917-115">You can use DSS to build projects, which then can generate MapReduce or Spark jobs.</span></span> <span data-ttu-id="d1917-116">These jobs are executed as regular MapReduce or Spark jobs on HDInsight, so you can scale the cluster on demand.</span><span class="sxs-lookup"><span data-stu-id="d1917-116">These jobs are executed as regular MapReduce or Spark jobs on HDInsight, so you can scale the cluster on demand.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1917-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d1917-117">Prerequisites</span></span>

<span data-ttu-id="d1917-118">To install this app on a new HDInsight cluster, or an existing cluster, you must have the following configuration:</span><span class="sxs-lookup"><span data-stu-id="d1917-118">To install this app on a new HDInsight cluster, or an existing cluster, you must have the following configuration:</span></span>

* <span data-ttu-id="d1917-119">Cluster tier(s): Standard, Premium</span><span class="sxs-lookup"><span data-stu-id="d1917-119">Cluster tier(s): Standard, Premium</span></span>
* <span data-ttu-id="d1917-120">Cluster type(s): Hadoop, Spark</span><span class="sxs-lookup"><span data-stu-id="d1917-120">Cluster type(s): Hadoop, Spark</span></span>
* <span data-ttu-id="d1917-121">Cluster version(s): 3.4, 3.5</span><span class="sxs-lookup"><span data-stu-id="d1917-121">Cluster version(s): 3.4, 3.5</span></span>

## <a name="install-the-dataiku-dss-published-application"></a><span data-ttu-id="d1917-122">Install the Dataiku DSS published application</span><span class="sxs-lookup"><span data-stu-id="d1917-122">Install the Dataiku DSS published application</span></span>

<span data-ttu-id="d1917-123">For step-by-step instructions on installing this and other available ISV applications, read [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d1917-123">For step-by-step instructions on installing this and other available ISV applications, read [Install third-party Hadoop applications](hdinsight-apps-install-applications.md).</span></span>

## <a name="launch-dataiku-dss"></a><span data-ttu-id="d1917-124">Launch Dataiku DSS</span><span class="sxs-lookup"><span data-stu-id="d1917-124">Launch Dataiku DSS</span></span>

1. <span data-ttu-id="d1917-125">After installation, you can launch DSS from your cluster in Azure portal by going to the **Settings** pane, then clicking **Applications** under the **General** category.</span><span class="sxs-lookup"><span data-stu-id="d1917-125">After installation, you can launch DSS from your cluster in Azure portal by going to the **Settings** pane, then clicking **Applications** under the **General** category.</span></span> <span data-ttu-id="d1917-126">The Installed Apps pane lists the installed applications.</span><span class="sxs-lookup"><span data-stu-id="d1917-126">The Installed Apps pane lists the installed applications.</span></span>

    ![Installed Dataiku DSS app](./media/hdinsight-apps-install-dataiku/app.png)

2. <span data-ttu-id="d1917-128">When you select DSS on HDInsight, you see a link to the web page, and the SSH endpoint path.</span><span class="sxs-lookup"><span data-stu-id="d1917-128">When you select DSS on HDInsight, you see a link to the web page, and the SSH endpoint path.</span></span> <span data-ttu-id="d1917-129">Select the WEBPAGE link.</span><span class="sxs-lookup"><span data-stu-id="d1917-129">Select the WEBPAGE link.</span></span>

3. <span data-ttu-id="d1917-130">On first launch, you are presented with a form to create a new Dataiku account for free, or to sign in to an existing account.</span><span class="sxs-lookup"><span data-stu-id="d1917-130">On first launch, you are presented with a form to create a new Dataiku account for free, or to sign in to an existing account.</span></span> <span data-ttu-id="d1917-131">You also have the option to start a free 2-week trial of [Enterprise Edition](https://www.dataiku.com/dss/editions/).</span><span class="sxs-lookup"><span data-stu-id="d1917-131">You also have the option to start a free 2-week trial of [Enterprise Edition](https://www.dataiku.com/dss/editions/).</span></span> <span data-ttu-id="d1917-132">From this point, you have the option of continuing with entering a license key for Enterprise Edition, or using the Community Edition.</span><span class="sxs-lookup"><span data-stu-id="d1917-132">From this point, you have the option of continuing with entering a license key for Enterprise Edition, or using the Community Edition.</span></span>

4. <span data-ttu-id="d1917-133">After completing your selected license option, you are presented with a login form.</span><span class="sxs-lookup"><span data-stu-id="d1917-133">After completing your selected license option, you are presented with a login form.</span></span> <span data-ttu-id="d1917-134">Enter the default credentials displayed prior to the login form.</span><span class="sxs-lookup"><span data-stu-id="d1917-134">Enter the default credentials displayed prior to the login form.</span></span>

<span data-ttu-id="d1917-135">The following steps provide a simple demonstration.</span><span class="sxs-lookup"><span data-stu-id="d1917-135">The following steps provide a simple demonstration.</span></span>

1. <span data-ttu-id="d1917-136">[Download the sample orders CSV](https://doc.dataiku.com/tutorials/data/101/haiku_shirt_sales.csv).</span><span class="sxs-lookup"><span data-stu-id="d1917-136">[Download the sample orders CSV](https://doc.dataiku.com/tutorials/data/101/haiku_shirt_sales.csv).</span></span>

2. <span data-ttu-id="d1917-137">From the DSS dashboard, select the **+** (New project) link on the left-hand menu to create a new project.</span><span class="sxs-lookup"><span data-stu-id="d1917-137">From the DSS dashboard, select the **+** (New project) link on the left-hand menu to create a new project.</span></span>

    ![New project link](./media/hdinsight-apps-install-dataiku/new-project.png)

3. <span data-ttu-id="d1917-139">In the New project form, type in a **Name**.</span><span class="sxs-lookup"><span data-stu-id="d1917-139">In the New project form, type in a **Name**.</span></span> <span data-ttu-id="d1917-140">The **Project Key** is automatically filled with a suggested value.</span><span class="sxs-lookup"><span data-stu-id="d1917-140">The **Project Key** is automatically filled with a suggested value.</span></span> <span data-ttu-id="d1917-141">In this case, enter "Orders".</span><span class="sxs-lookup"><span data-stu-id="d1917-141">In this case, enter "Orders".</span></span> <span data-ttu-id="d1917-142">Click **CREATE**.</span><span class="sxs-lookup"><span data-stu-id="d1917-142">Click **CREATE**.</span></span>

    ![New project form](./media/hdinsight-apps-install-dataiku/new-project-form.png)

4. <span data-ttu-id="d1917-144">Select **+ IMPORT YOUR FIRST DATASET** in your new project page.</span><span class="sxs-lookup"><span data-stu-id="d1917-144">Select **+ IMPORT YOUR FIRST DATASET** in your new project page.</span></span>

    ![File Upload](./media/hdinsight-apps-install-dataiku/import-dataset.png)

5. <span data-ttu-id="d1917-146">Select **Upload your files** under the **Files** dataset list.</span><span class="sxs-lookup"><span data-stu-id="d1917-146">Select **Upload your files** under the **Files** dataset list.</span></span> <span data-ttu-id="d1917-147">You are presented with the Upload dialog.</span><span class="sxs-lookup"><span data-stu-id="d1917-147">You are presented with the Upload dialog.</span></span> <span data-ttu-id="d1917-148">Click on Add a file, select the `haiku_shirt_sales.csv` file you downloaded, and validate.</span><span class="sxs-lookup"><span data-stu-id="d1917-148">Click on Add a file, select the `haiku_shirt_sales.csv` file you downloaded, and validate.</span></span>

6. <span data-ttu-id="d1917-149">The file is uploaded to DSS.</span><span class="sxs-lookup"><span data-stu-id="d1917-149">The file is uploaded to DSS.</span></span> <span data-ttu-id="d1917-150">Check if DSS detected the CSV format correctly by clicking on the Preview button.</span><span class="sxs-lookup"><span data-stu-id="d1917-150">Check if DSS detected the CSV format correctly by clicking on the Preview button.</span></span>

    ![File Upload](./media/hdinsight-apps-install-dataiku/preview.png)

7. <span data-ttu-id="d1917-152">The import is almost perfect.</span><span class="sxs-lookup"><span data-stu-id="d1917-152">The import is almost perfect.</span></span> <span data-ttu-id="d1917-153">The CSV file is using a Tab separator.</span><span class="sxs-lookup"><span data-stu-id="d1917-153">The CSV file is using a Tab separator.</span></span> <span data-ttu-id="d1917-154">You can see the data is in a tabular format, with columns called features, and lines that represent observations.</span><span class="sxs-lookup"><span data-stu-id="d1917-154">You can see the data is in a tabular format, with columns called features, and lines that represent observations.</span></span> <span data-ttu-id="d1917-155">The one error is that apparently the file contained a blank line between the header and the data.</span><span class="sxs-lookup"><span data-stu-id="d1917-155">The one error is that apparently the file contained a blank line between the header and the data.</span></span> <span data-ttu-id="d1917-156">To fix this error, enter `1` in the **Skip next lines** field.</span><span class="sxs-lookup"><span data-stu-id="d1917-156">To fix this error, enter `1` in the **Skip next lines** field.</span></span>

    ![Save](./media/hdinsight-apps-install-dataiku/skip-lines.png)

8. <span data-ttu-id="d1917-158">Give the new dataset a name.</span><span class="sxs-lookup"><span data-stu-id="d1917-158">Give the new dataset a name.</span></span> <span data-ttu-id="d1917-159">Enter **haiku_shirt_sales** in the field on top of the screen, then select the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="d1917-159">Enter **haiku_shirt_sales** in the field on top of the screen, then select the **Create** button.</span></span>

9. <span data-ttu-id="d1917-160">You see a tabular view of your data where you can start exploring it.</span><span class="sxs-lookup"><span data-stu-id="d1917-160">You see a tabular view of your data where you can start exploring it.</span></span> <span data-ttu-id="d1917-161">For each column, you should see that Dataiku Science Studio has detected a data type, in _blue_ - in this case, Text, Number, or Date (unparsed).</span><span class="sxs-lookup"><span data-stu-id="d1917-161">For each column, you should see that Dataiku Science Studio has detected a data type, in _blue_ - in this case, Text, Number, or Date (unparsed).</span></span> <span data-ttu-id="d1917-162">A gauge indicates the ratio of the column for which the values do not seem to match the type (in red) or are missing (blank).</span><span class="sxs-lookup"><span data-stu-id="d1917-162">A gauge indicates the ratio of the column for which the values do not seem to match the type (in red) or are missing (blank).</span></span> <span data-ttu-id="d1917-163">In this example dataset, the department has both empty values and invalid data.</span><span class="sxs-lookup"><span data-stu-id="d1917-163">In this example dataset, the department has both empty values and invalid data.</span></span>

    ![Tabular view](./media/hdinsight-apps-install-dataiku/viewing-dataset.png)

## <a name="data-manipulation"></a><span data-ttu-id="d1917-165">Data manipulation</span><span class="sxs-lookup"><span data-stu-id="d1917-165">Data manipulation</span></span>

<span data-ttu-id="d1917-166">Real-world data is almost always messy, and rarely is it neatly packaged.</span><span class="sxs-lookup"><span data-stu-id="d1917-166">Real-world data is almost always messy, and rarely is it neatly packaged.</span></span> <span data-ttu-id="d1917-167">Cleaning up data typically requires a chain of scripts and associated business logic.</span><span class="sxs-lookup"><span data-stu-id="d1917-167">Cleaning up data typically requires a chain of scripts and associated business logic.</span></span> <span data-ttu-id="d1917-168">Dataiku DSS provides a dedicated **Lab** tool to make this task more user-friendly.</span><span class="sxs-lookup"><span data-stu-id="d1917-168">Dataiku DSS provides a dedicated **Lab** tool to make this task more user-friendly.</span></span>

1. <span data-ttu-id="d1917-169">Click on **Lab** in the upper-right corner.</span><span class="sxs-lookup"><span data-stu-id="d1917-169">Click on **Lab** in the upper-right corner.</span></span>

    ![Lab button](./media/hdinsight-apps-install-dataiku/lab-button.png)

2. <span data-ttu-id="d1917-171">The Lab window opens.</span><span class="sxs-lookup"><span data-stu-id="d1917-171">The Lab window opens.</span></span> <span data-ttu-id="d1917-172">The lab is where you iteratively work on your dataset to get further into it.</span><span class="sxs-lookup"><span data-stu-id="d1917-172">The lab is where you iteratively work on your dataset to get further into it.</span></span> <span data-ttu-id="d1917-173">This tutorial demonstrates the Visual analysis aspect.</span><span class="sxs-lookup"><span data-stu-id="d1917-173">This tutorial demonstrates the Visual analysis aspect.</span></span> <span data-ttu-id="d1917-174">Select the **New** button below Visual analysis.</span><span class="sxs-lookup"><span data-stu-id="d1917-174">Select the **New** button below Visual analysis.</span></span> <span data-ttu-id="d1917-175">You are prompted to specify a name for your analysis.</span><span class="sxs-lookup"><span data-stu-id="d1917-175">You are prompted to specify a name for your analysis.</span></span> <span data-ttu-id="d1917-176">Leave the default name for now, then click **CREATE**.</span><span class="sxs-lookup"><span data-stu-id="d1917-176">Leave the default name for now, then click **CREATE**.</span></span>

    ![Create lab](./media/hdinsight-apps-install-dataiku/create-lab.png)

3. <span data-ttu-id="d1917-178">Select the **Quick columns stats** button on the upper-right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="d1917-178">Select the **Quick columns stats** button on the upper-right corner of the page.</span></span>

    ![Quick columns stats](./media/hdinsight-apps-install-dataiku/quick-column-stats.png)

4. <span data-ttu-id="d1917-180">You see statistics for data types and values displayed in timeline-based graphs under the **Columns quick view** pane.</span><span class="sxs-lookup"><span data-stu-id="d1917-180">You see statistics for data types and values displayed in timeline-based graphs under the **Columns quick view** pane.</span></span>

    ![Columns quick view](./media/hdinsight-apps-install-dataiku/columns-quick-view.png)

<span data-ttu-id="d1917-182">You can now explore DSS using the sample data.</span><span class="sxs-lookup"><span data-stu-id="d1917-182">You can now explore DSS using the sample data.</span></span> <span data-ttu-id="d1917-183">You can clean up and work with the data, and create new visualizations.</span><span class="sxs-lookup"><span data-stu-id="d1917-183">You can clean up and work with the data, and create new visualizations.</span></span>

<span data-ttu-id="d1917-184">For in-depth tutorials, read [Learn Dataiku DSS](https://www.dataiku.com/learn/).</span><span class="sxs-lookup"><span data-stu-id="d1917-184">For in-depth tutorials, read [Learn Dataiku DSS](https://www.dataiku.com/learn/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1917-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1917-185">Next steps</span></span>

* <span data-ttu-id="d1917-186">[Dataiku DSS documentation](https://doc.dataiku.com/dss/latest/).</span><span class="sxs-lookup"><span data-stu-id="d1917-186">[Dataiku DSS documentation](https://doc.dataiku.com/dss/latest/).</span></span>
* <span data-ttu-id="d1917-187">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to deploy an unpublished HDInsight application to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1917-187">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="d1917-188">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d1917-188">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="d1917-189">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="d1917-189">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="d1917-190">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): Learn how to use Script Action to install additional applications.</span><span class="sxs-lookup"><span data-stu-id="d1917-190">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): Learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="d1917-191">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): Learn how to use an empty edge node for accessing HDInsight clusters, and for testing and hosting HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="d1917-191">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): Learn how to use an empty edge node for accessing HDInsight clusters, and for testing and hosting HDInsight applications.</span></span>
