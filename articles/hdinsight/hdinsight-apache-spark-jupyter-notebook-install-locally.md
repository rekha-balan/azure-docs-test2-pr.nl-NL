---
title: Install Jupyter notebook locally and connect to an Azure Spark cluster | Microsoft Docs
description: Learn about how to install Jupyter notebook locally on your computer and connect it to an Apache Spark cluster on Azure HDInsight.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2017
ms.author: nitinme
ms.openlocfilehash: 32168d50754ca3fb68a36c789d00c28bdd2ee673
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555232"
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="512bc-103">Install Jupyter notebook on your computer and connect to Apache Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="512bc-103">Install Jupyter notebook on your computer and connect to Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="512bc-104">In this article you will learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="512bc-104">In this article you will learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="512bc-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span><span class="sxs-lookup"><span data-stu-id="512bc-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="512bc-106">For a list of reasons and challenges, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="512bc-106">For a list of reasons and challenges, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="512bc-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span><span class="sxs-lookup"><span data-stu-id="512bc-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="512bc-108">Install Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="512bc-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="512bc-109">Install the PySpark and Spark kernels with the Spark magic</span><span class="sxs-lookup"><span data-stu-id="512bc-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="512bc-110">Configure Spark magic to access Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="512bc-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="512bc-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="512bc-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="512bc-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="512bc-112">Prerequisites</span></span>
<span data-ttu-id="512bc-113">The prerequisites listed here are not for installing Jupyter.</span><span class="sxs-lookup"><span data-stu-id="512bc-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="512bc-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span><span class="sxs-lookup"><span data-stu-id="512bc-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="512bc-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="512bc-115">An Azure subscription.</span></span> <span data-ttu-id="512bc-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="512bc-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="512bc-117">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="512bc-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="512bc-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="512bc-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="512bc-119">Install Jupyter notebook on your computer</span><span class="sxs-lookup"><span data-stu-id="512bc-119">Install Jupyter notebook on your computer</span></span>
<span data-ttu-id="512bc-120">You  must install Python before you can install Jupyter notebooks.</span><span class="sxs-lookup"><span data-stu-id="512bc-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="512bc-121">Both Python and Jupyter are available as part of the [Ananconda distribution](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="512bc-121">Both Python and Jupyter are available as part of the [Ananconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="512bc-122">When you install Anaconda, you actually install a distribution of Python.</span><span class="sxs-lookup"><span data-stu-id="512bc-122">When you install Anaconda, you actually install a distribution of Python.</span></span> <span data-ttu-id="512bc-123">Once Anaconda is installed, you add the Jupyter installation by running a command.</span><span class="sxs-lookup"><span data-stu-id="512bc-123">Once Anaconda is installed, you add the Jupyter installation by running a command.</span></span> <span data-ttu-id="512bc-124">This section provides the instructions that you must follow.</span><span class="sxs-lookup"><span data-stu-id="512bc-124">This section provides the instructions that you must follow.</span></span>

1. <span data-ttu-id="512bc-125">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span><span class="sxs-lookup"><span data-stu-id="512bc-125">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="512bc-126">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span><span class="sxs-lookup"><span data-stu-id="512bc-126">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
2. <span data-ttu-id="512bc-127">Run the following command to install Jupyter.</span><span class="sxs-lookup"><span data-stu-id="512bc-127">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="512bc-128">For more information on installting Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="512bc-128">For more information on installting Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="512bc-129">Install the kernels and Spark magic</span><span class="sxs-lookup"><span data-stu-id="512bc-129">Install the kernels and Spark magic</span></span>
<span data-ttu-id="512bc-130">For instructions on how to install the Spark magic, the PySpark and Spark kernels, see the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="512bc-130">For instructions on how to install the Spark magic, the PySpark and Spark kernels, see the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span>

<span data-ttu-id="512bc-131">For clusters v3.4, please install sparkmagic 0.5.0 by executing `pip install sparkmagic==0.2.3`.</span><span class="sxs-lookup"><span data-stu-id="512bc-131">For clusters v3.4, please install sparkmagic 0.5.0 by executing `pip install sparkmagic==0.2.3`.</span></span>

<span data-ttu-id="512bc-132">For clusters v3.5, please install sparkmagic 0.8.4 by executing `pip install sparkmagic==0.8.4`.</span><span class="sxs-lookup"><span data-stu-id="512bc-132">For clusters v3.5, please install sparkmagic 0.8.4 by executing `pip install sparkmagic==0.8.4`.</span></span>

## <a name="configure-spark-magic-to-access-the-hdinsight-spark-cluster"></a><span data-ttu-id="512bc-133">Configure Spark magic to access the HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="512bc-133">Configure Spark magic to access the HDInsight Spark cluster</span></span>
<span data-ttu-id="512bc-134">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="512bc-134">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="512bc-135">The Jupyter configuration information is typically stored in the users home directory.</span><span class="sxs-lookup"><span data-stu-id="512bc-135">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="512bc-136">To locate your home directory on any OS platform, type the following commands.</span><span class="sxs-lookup"><span data-stu-id="512bc-136">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="512bc-137">Start the Python shell.</span><span class="sxs-lookup"><span data-stu-id="512bc-137">Start the Python shell.</span></span> <span data-ttu-id="512bc-138">On a command window, type the following:</span><span class="sxs-lookup"><span data-stu-id="512bc-138">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="512bc-139">On the Python shell, enter the following command to find out the home directory.</span><span class="sxs-lookup"><span data-stu-id="512bc-139">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="512bc-140">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="512bc-140">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="512bc-141">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span><span class="sxs-lookup"><span data-stu-id="512bc-141">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. <span data-ttu-id="512bc-142">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span><span class="sxs-lookup"><span data-stu-id="512bc-142">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="512bc-143">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actualy password.</span><span class="sxs-lookup"><span data-stu-id="512bc-143">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actualy password.</span></span> <span data-ttu-id="512bc-144">A simple Python snippet to run from your command prompt would be:</span><span class="sxs-lookup"><span data-stu-id="512bc-144">A simple Python snippet to run from your command prompt would be:</span></span>

        python -c "import base64; print(base64.b64encode('{YOURPASSWORD}'))"

5. <span data-ttu-id="512bc-145">Configure the right Heartbeat settings in `config.json`.</span><span class="sxs-lookup"><span data-stu-id="512bc-145">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="512bc-146">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span><span class="sxs-lookup"><span data-stu-id="512bc-146">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="512bc-147">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="512bc-147">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="512bc-148">For `sparkmagic 0.5.0` (clusters v3.4), include:</span><span class="sxs-lookup"><span data-stu-id="512bc-148">For `sparkmagic 0.5.0` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="512bc-149">For `sparkmagic 0.8.4` (clusters v3.5), include:</span><span class="sxs-lookup"><span data-stu-id="512bc-149">For `sparkmagic 0.8.4` (clusters v3.5), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="512bc-150">Heartbeats are sent to ensure that sessions are not leaked.</span><span class="sxs-lookup"><span data-stu-id="512bc-150">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="512bc-151">Note that when a computer goes to sleep or is shut down, the hearbeat will not be sent, resulting in the session being cleaned up.</span><span class="sxs-lookup"><span data-stu-id="512bc-151">Note that when a computer goes to sleep or is shut down, the hearbeat will not be sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="512bc-152">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="512bc-152">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="512bc-153">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span><span class="sxs-lookup"><span data-stu-id="512bc-153">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

6. <span data-ttu-id="512bc-154">Start Jupyter.</span><span class="sxs-lookup"><span data-stu-id="512bc-154">Start Jupyter.</span></span> <span data-ttu-id="512bc-155">Use the following command from the command prompt.</span><span class="sxs-lookup"><span data-stu-id="512bc-155">Use the following command from the command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="512bc-156">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span><span class="sxs-lookup"><span data-stu-id="512bc-156">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="512bc-157">Perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="512bc-157">Perform the following steps.</span></span>

   1. <span data-ttu-id="512bc-158">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="512bc-158">Create a new notebook.</span></span> <span data-ttu-id="512bc-159">From the right hand corner, click **New**.</span><span class="sxs-lookup"><span data-stu-id="512bc-159">From the right hand corner, click **New**.</span></span> <span data-ttu-id="512bc-160">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span><span class="sxs-lookup"><span data-stu-id="512bc-160">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span>

       <span data-ttu-id="512bc-161">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Create a new Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="512bc-161">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Create a new Jupyter notebook")</span></span>

        <span data-ttu-id="512bc-162">Click **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="512bc-162">Click **PySpark**.</span></span>


    2. <span data-ttu-id="512bc-163">Run the following code snippet.</span><span class="sxs-lookup"><span data-stu-id="512bc-163">Run the following code snippet.</span></span>

            %%sql
            SELECT * FROM hivesampletable LIMIT 5

        <span data-ttu-id="512bc-164">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span><span class="sxs-lookup"><span data-stu-id="512bc-164">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="512bc-165">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span><span class="sxs-lookup"><span data-stu-id="512bc-165">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="512bc-166">Why should I install Jupyter on my computer?</span><span class="sxs-lookup"><span data-stu-id="512bc-166">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="512bc-167">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="512bc-167">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="512bc-168">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span><span class="sxs-lookup"><span data-stu-id="512bc-168">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="512bc-169">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="512bc-169">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="512bc-170">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="512bc-170">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="512bc-171">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span><span class="sxs-lookup"><span data-stu-id="512bc-171">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="512bc-172">You can use GitHub to implement a source control system and have version control for the notebooks.</span><span class="sxs-lookup"><span data-stu-id="512bc-172">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="512bc-173">You can also have a collaborative environment where multiple users can work with the same notebook.</span><span class="sxs-lookup"><span data-stu-id="512bc-173">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="512bc-174">You can work with notebooks locally without even having a cluster up.</span><span class="sxs-lookup"><span data-stu-id="512bc-174">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="512bc-175">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span><span class="sxs-lookup"><span data-stu-id="512bc-175">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="512bc-176">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span><span class="sxs-lookup"><span data-stu-id="512bc-176">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="512bc-177">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span><span class="sxs-lookup"><span data-stu-id="512bc-177">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="512bc-178">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span><span class="sxs-lookup"><span data-stu-id="512bc-178">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="512bc-179">In such a situation, multiple Livy sessions are created.</span><span class="sxs-lookup"><span data-stu-id="512bc-179">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="512bc-180">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span><span class="sxs-lookup"><span data-stu-id="512bc-180">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <a name="seealso"></a><span data-ttu-id="512bc-181">See also</span><span class="sxs-lookup"><span data-stu-id="512bc-181">See also</span></span>
* [<span data-ttu-id="512bc-182">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="512bc-182">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="512bc-183">Scenarios</span><span class="sxs-lookup"><span data-stu-id="512bc-183">Scenarios</span></span>
* [<span data-ttu-id="512bc-184">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="512bc-184">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="512bc-185">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="512bc-185">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="512bc-186">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="512bc-186">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="512bc-187">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="512bc-187">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="512bc-188">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="512bc-188">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="512bc-189">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="512bc-189">Create and run applications</span></span>
* [<span data-ttu-id="512bc-190">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="512bc-190">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="512bc-191">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="512bc-191">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="512bc-192">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="512bc-192">Tools and extensions</span></span>
* [<span data-ttu-id="512bc-193">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="512bc-193">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="512bc-194">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="512bc-194">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="512bc-195">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="512bc-195">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="512bc-196">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="512bc-196">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="512bc-197">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="512bc-197">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="512bc-198">Manage resources</span><span class="sxs-lookup"><span data-stu-id="512bc-198">Manage resources</span></span>
* [<span data-ttu-id="512bc-199">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="512bc-199">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="512bc-200">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="512bc-200">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

