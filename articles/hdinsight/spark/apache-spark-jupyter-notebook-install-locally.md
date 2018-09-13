---
title: Install Jupyter locally and connect to Spark in Azure HDInsight
description: Learn how to install Jupyter notebook locally on your computer and connect it to an Apache Spark cluster.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 11/28/2017
ms.author: jasonh
ms.openlocfilehash: 83e9596f37850ef5b26b530cd4424a024355fc8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865904"
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a><span data-ttu-id="7ca63-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ca63-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span></span>

<span data-ttu-id="7ca63-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7ca63-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="7ca63-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span><span class="sxs-lookup"><span data-stu-id="7ca63-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="7ca63-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="7ca63-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="7ca63-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span><span class="sxs-lookup"><span data-stu-id="7ca63-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="7ca63-108">Install Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="7ca63-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="7ca63-109">Install the PySpark and Spark kernels with the Spark magic</span><span class="sxs-lookup"><span data-stu-id="7ca63-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="7ca63-110">Configure Spark magic to access Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ca63-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="7ca63-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="7ca63-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ca63-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7ca63-112">Prerequisites</span></span>
<span data-ttu-id="7ca63-113">The prerequisites listed here are not for installing Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7ca63-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="7ca63-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span><span class="sxs-lookup"><span data-stu-id="7ca63-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="7ca63-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7ca63-115">An Azure subscription.</span></span> <span data-ttu-id="7ca63-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7ca63-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7ca63-117">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ca63-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="7ca63-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7ca63-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="7ca63-119">Install Jupyter notebook on your computer</span><span class="sxs-lookup"><span data-stu-id="7ca63-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="7ca63-120">You  must install Python before you can install Jupyter notebooks.</span><span class="sxs-lookup"><span data-stu-id="7ca63-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="7ca63-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="7ca63-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="7ca63-122">When you install Anaconda, you install a distribution of Python.</span><span class="sxs-lookup"><span data-stu-id="7ca63-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="7ca63-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span><span class="sxs-lookup"><span data-stu-id="7ca63-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="7ca63-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span><span class="sxs-lookup"><span data-stu-id="7ca63-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="7ca63-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span><span class="sxs-lookup"><span data-stu-id="7ca63-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
1. <span data-ttu-id="7ca63-126">Run the following command to install Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7ca63-126">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="7ca63-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="7ca63-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="7ca63-128">Install the kernels and Spark magic</span><span class="sxs-lookup"><span data-stu-id="7ca63-128">Install the kernels and Spark magic</span></span>

<span data-ttu-id="7ca63-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="7ca63-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="7ca63-130">The first step in the Spark magic documentation asks you to install Spark magic.</span><span class="sxs-lookup"><span data-stu-id="7ca63-130">The first step in the Spark magic documentation asks you to install Spark magic.</span></span> <span data-ttu-id="7ca63-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span><span class="sxs-lookup"><span data-stu-id="7ca63-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span></span> <span data-ttu-id="7ca63-132">After that, follow the remaining steps in the Spark magic documentation.</span><span class="sxs-lookup"><span data-stu-id="7ca63-132">After that, follow the remaining steps in the Spark magic documentation.</span></span> <span data-ttu-id="7ca63-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span><span class="sxs-lookup"><span data-stu-id="7ca63-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span></span>

* <span data-ttu-id="7ca63-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="7ca63-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="7ca63-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="7ca63-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a><span data-ttu-id="7ca63-136">Configure Spark magic to connect to HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="7ca63-136">Configure Spark magic to connect to HDInsight Spark cluster</span></span>

<span data-ttu-id="7ca63-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ca63-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="7ca63-138">The Jupyter configuration information is typically stored in the users home directory.</span><span class="sxs-lookup"><span data-stu-id="7ca63-138">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="7ca63-139">To locate your home directory on any OS platform, type the following commands.</span><span class="sxs-lookup"><span data-stu-id="7ca63-139">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="7ca63-140">Start the Python shell.</span><span class="sxs-lookup"><span data-stu-id="7ca63-140">Start the Python shell.</span></span> <span data-ttu-id="7ca63-141">On a command window, type the following:</span><span class="sxs-lookup"><span data-stu-id="7ca63-141">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="7ca63-142">On the Python shell, enter the following command to find out the home directory.</span><span class="sxs-lookup"><span data-stu-id="7ca63-142">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

1. <span data-ttu-id="7ca63-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="7ca63-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
1. <span data-ttu-id="7ca63-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span><span class="sxs-lookup"><span data-stu-id="7ca63-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

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

1. <span data-ttu-id="7ca63-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span><span class="sxs-lookup"><span data-stu-id="7ca63-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="7ca63-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span><span class="sxs-lookup"><span data-stu-id="7ca63-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span></span>

1. <span data-ttu-id="7ca63-147">Configure the right Heartbeat settings in `config.json`.</span><span class="sxs-lookup"><span data-stu-id="7ca63-147">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="7ca63-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span><span class="sxs-lookup"><span data-stu-id="7ca63-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="7ca63-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="7ca63-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="7ca63-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span><span class="sxs-lookup"><span data-stu-id="7ca63-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="7ca63-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span><span class="sxs-lookup"><span data-stu-id="7ca63-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="7ca63-152">Heartbeats are sent to ensure that sessions are not leaked.</span><span class="sxs-lookup"><span data-stu-id="7ca63-152">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="7ca63-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span><span class="sxs-lookup"><span data-stu-id="7ca63-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="7ca63-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="7ca63-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="7ca63-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span><span class="sxs-lookup"><span data-stu-id="7ca63-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

1. <span data-ttu-id="7ca63-156">Start Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7ca63-156">Start Jupyter.</span></span> <span data-ttu-id="7ca63-157">Use the following command from the command prompt.</span><span class="sxs-lookup"><span data-stu-id="7ca63-157">Use the following command from the command prompt.</span></span>

        jupyter notebook

1. <span data-ttu-id="7ca63-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span><span class="sxs-lookup"><span data-stu-id="7ca63-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="7ca63-159">Perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="7ca63-159">Perform the following steps.</span></span>

    <span data-ttu-id="7ca63-160">a.</span><span class="sxs-lookup"><span data-stu-id="7ca63-160">a.</span></span> <span data-ttu-id="7ca63-161">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="7ca63-161">Create a new notebook.</span></span> <span data-ttu-id="7ca63-162">From the right-hand corner, click **New**.</span><span class="sxs-lookup"><span data-stu-id="7ca63-162">From the right-hand corner, click **New**.</span></span> <span data-ttu-id="7ca63-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span><span class="sxs-lookup"><span data-stu-id="7ca63-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="7ca63-164">Click **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="7ca63-164">Click **PySpark**.</span></span>

    <span data-ttu-id="7ca63-165">![Kernels in Jupyter notebook](./media/apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="7ca63-165">![Kernels in Jupyter notebook](./media/apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="7ca63-166">b.</span><span class="sxs-lookup"><span data-stu-id="7ca63-166">b.</span></span> <span data-ttu-id="7ca63-167">Run the following code snippet.</span><span class="sxs-lookup"><span data-stu-id="7ca63-167">Run the following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="7ca63-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span><span class="sxs-lookup"><span data-stu-id="7ca63-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="7ca63-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span><span class="sxs-lookup"><span data-stu-id="7ca63-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="7ca63-170">Why should I install Jupyter on my computer?</span><span class="sxs-lookup"><span data-stu-id="7ca63-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="7ca63-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ca63-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="7ca63-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span><span class="sxs-lookup"><span data-stu-id="7ca63-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="7ca63-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="7ca63-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="7ca63-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="7ca63-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="7ca63-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span><span class="sxs-lookup"><span data-stu-id="7ca63-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="7ca63-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span><span class="sxs-lookup"><span data-stu-id="7ca63-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="7ca63-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span><span class="sxs-lookup"><span data-stu-id="7ca63-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="7ca63-178">You can work with notebooks locally without even having a cluster up.</span><span class="sxs-lookup"><span data-stu-id="7ca63-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="7ca63-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span><span class="sxs-lookup"><span data-stu-id="7ca63-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="7ca63-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span><span class="sxs-lookup"><span data-stu-id="7ca63-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="7ca63-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span><span class="sxs-lookup"><span data-stu-id="7ca63-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="7ca63-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span><span class="sxs-lookup"><span data-stu-id="7ca63-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="7ca63-183">In such a situation, multiple Livy sessions are created.</span><span class="sxs-lookup"><span data-stu-id="7ca63-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="7ca63-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span><span class="sxs-lookup"><span data-stu-id="7ca63-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <a name="seealso"></a><span data-ttu-id="7ca63-185">See also</span><span class="sxs-lookup"><span data-stu-id="7ca63-185">See also</span></span>
* [<span data-ttu-id="7ca63-186">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ca63-186">Overview: Apache Spark on Azure HDInsight</span></span>](apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="7ca63-187">Scenarios</span><span class="sxs-lookup"><span data-stu-id="7ca63-187">Scenarios</span></span>
* [<span data-ttu-id="7ca63-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="7ca63-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](apache-spark-use-bi-tools.md)
* [<span data-ttu-id="7ca63-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="7ca63-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="7ca63-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="7ca63-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="7ca63-191">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ca63-191">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="7ca63-192">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="7ca63-192">Create and run applications</span></span>
* [<span data-ttu-id="7ca63-193">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="7ca63-193">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="7ca63-194">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="7ca63-194">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="7ca63-195">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="7ca63-195">Tools and extensions</span></span>
* [<span data-ttu-id="7ca63-196">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="7ca63-196">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="7ca63-197">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="7ca63-197">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="7ca63-198">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ca63-198">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="7ca63-199">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ca63-199">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="7ca63-200">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="7ca63-200">Use external packages with Jupyter notebooks</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="7ca63-201">Manage resources</span><span class="sxs-lookup"><span data-stu-id="7ca63-201">Manage resources</span></span>
* [<span data-ttu-id="7ca63-202">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ca63-202">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="7ca63-203">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ca63-203">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)
