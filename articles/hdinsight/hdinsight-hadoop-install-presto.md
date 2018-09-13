---
title: Install Presto on Azure HDInsight Linux clusters
description: Learn how to install Presto and Airpal on Linux-based HDInsight Hadoop clusters using Script Actions.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/21/2018
ms.author: jasonh
ms.openlocfilehash: 1569b5931a24048fa7a88c4a546bbf88547208d1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856712"
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="f0ce5-103">Install and use Presto on HDInsight Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="f0ce5-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="f0ce5-104">In this document, you learn how to install Presto on HDInsight Hadoop clusters by using Script Action.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-104">In this document, you learn how to install Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="f0ce5-105">You also learn how to install Airpal on an existing Presto HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-105">You also learn how to install Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0ce5-106">The steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-106">The steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="f0ce5-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f0ce5-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="f0ce5-109">What is Presto?</span><span class="sxs-lookup"><span data-stu-id="f0ce5-109">What is Presto?</span></span>
<span data-ttu-id="f0ce5-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="f0ce5-111">Presto is suitable for interactive querying of petabytes of data.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="f0ce5-112">For more information on the components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-112">For more information on the components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="f0ce5-113">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-113">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
> 
> <span data-ttu-id="f0ce5-114">Custom components, such as Presto, receive commercially reasonable support to help you to further troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-114">Custom components, such as Presto, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="f0ce5-115">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-115">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="f0ce5-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="f0ce5-117">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-117">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="f0ce5-118">Install Presto using script action</span><span class="sxs-lookup"><span data-stu-id="f0ce5-118">Install Presto using script action</span></span>

<span data-ttu-id="f0ce5-119">This section provides instructions on how to use the sample script when creating a new cluster by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-119">This section provides instructions on how to use the sample script when creating a new cluster by using the Azure portal.</span></span> 

1. <span data-ttu-id="f0ce5-120">Start provisioning a cluster by using the steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-120">Start provisioning a cluster by using the steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="f0ce5-121">Make sure you create the cluster using the **Custom** cluster creation flow.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-121">Make sure you create the cluster using the **Custom** cluster creation flow.</span></span> <span data-ttu-id="f0ce5-122">The cluster must meet the following requirements.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-122">The cluster must meet the following requirements.</span></span>

    * <span data-ttu-id="f0ce5-123">It must be a Hadoop cluster with HDInsight version 3.6.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-123">It must be a Hadoop cluster with HDInsight version 3.6.</span></span>

    * <span data-ttu-id="f0ce5-124">It must use Azure Storage as the data store.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-124">It must use Azure Storage as the data store.</span></span> <span data-ttu-id="f0ce5-125">Using Presto on a cluster that uses Azure Data Lake Store as the storage option is not yet supported.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-125">Using Presto on a cluster that uses Azure Data Lake Store as the storage option is not yet supported.</span></span> 

    ![HDInsight cluster creation using custom options](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="f0ce5-127">On the **Advanced settings** area, select **Script Actions**, and provide the information below:</span><span class="sxs-lookup"><span data-stu-id="f0ce5-127">On the **Advanced settings** area, select **Script Actions**, and provide the information below:</span></span>
   
   * <span data-ttu-id="f0ce5-128">**NAME**: Enter a friendly name for the script action.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-128">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="f0ce5-129">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="f0ce5-129">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="f0ce5-130">**HEAD**: Check this option</span><span class="sxs-lookup"><span data-stu-id="f0ce5-130">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="f0ce5-131">**WORKER**: Check this option</span><span class="sxs-lookup"><span data-stu-id="f0ce5-131">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="f0ce5-132">**ZOOKEEPER**: Clear this check box</span><span class="sxs-lookup"><span data-stu-id="f0ce5-132">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="f0ce5-133">**PARAMETERS**: Leave this field blank</span><span class="sxs-lookup"><span data-stu-id="f0ce5-133">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="f0ce5-134">At the bottom of the **Script Actions** area, click the **Select** button to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-134">At the bottom of the **Script Actions** area, click the **Select** button to save the configuration.</span></span> <span data-ttu-id="f0ce5-135">Finally, click  the **Select** button at the bottom of the **Advanced Settings** area to save the configuration information.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-135">Finally, click  the **Select** button at the bottom of the **Advanced Settings** area to save the configuration information.</span></span>

4. <span data-ttu-id="f0ce5-136">Continue provisioning the cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-136">Continue provisioning the cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0ce5-137">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-137">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="f0ce5-138">You can also apply script actions to already running clusters.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-138">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="f0ce5-139">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-139">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="f0ce5-140">Use Presto with HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0ce5-140">Use Presto with HDInsight</span></span>

<span data-ttu-id="f0ce5-141">To work with Presto in an HDInsight cluster, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="f0ce5-141">To work with Presto in an HDInsight cluster, use the following steps:</span></span>

1. <span data-ttu-id="f0ce5-142">Connect to the HDInsight cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="f0ce5-142">Connect to the HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="f0ce5-143">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-143">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="f0ce5-144">Start the Presto shell using the following command.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-144">Start the Presto shell using the following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="f0ce5-145">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-145">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="f0ce5-146">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-146">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="f0ce5-147">Hive connector is configured to use the default installed Hive installation, so all the tables from Hive will be automatically visible in Presto.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-147">Hive connector is configured to use the default installed Hive installation, so all the tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="f0ce5-148">For more information, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-148">For more information, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="f0ce5-149">Use Airpal with Presto</span><span class="sxs-lookup"><span data-stu-id="f0ce5-149">Use Airpal with Presto</span></span>

<span data-ttu-id="f0ce5-150">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-150">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="f0ce5-151">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-151">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="f0ce5-152">Use the following steps to install Airpal on the edge node:</span><span class="sxs-lookup"><span data-stu-id="f0ce5-152">Use the following steps to install Airpal on the edge node:</span></span>

1. <span data-ttu-id="f0ce5-153">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span><span class="sxs-lookup"><span data-stu-id="f0ce5-153">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="f0ce5-154">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-154">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f0ce5-155">Once you are connected, run the following command.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-155">Once you are connected, run the following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="f0ce5-156">You see output similar to the following JSON:</span><span class="sxs-lookup"><span data-stu-id="f0ce5-156">You see output similar to the following JSON:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="f0ce5-157">From the output, note the value for the **value** property.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-157">From the output, note the value for the **value** property.</span></span> <span data-ttu-id="f0ce5-158">You will need this value while installing Airpal on the cluster edgenode.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-158">You will need this value while installing Airpal on the cluster edgenode.</span></span> <span data-ttu-id="f0ce5-159">From the output above, the value that you will need is **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-159">From the output above, the value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="f0ce5-160">Use the template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** to create an HDInsight cluster edgenode and provide the values as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-160">Use the template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** to create an HDInsight cluster edgenode and provide the values as shown in the following screenshot.</span></span>

    ![HDInsight install Airpal on Presto cluster](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="f0ce5-162">Click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-162">Click **Purchase**.</span></span>

6. <span data-ttu-id="f0ce5-163">Once the changes are applied to the cluster configuration, you can access the Airpal web interface by using the following steps.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-163">Once the changes are applied to the cluster configuration, you can access the Airpal web interface by using the following steps.</span></span>

    1. <span data-ttu-id="f0ce5-164">From the cluster dialog, click **Applications**.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-164">From the cluster dialog, click **Applications**.</span></span>

        ![HDInsight launch Airpal on Presto cluster](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    2. <span data-ttu-id="f0ce5-166">From the **Installed Apps** area, click **Portal** against airpal.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-166">From the **Installed Apps** area, click **Portal** against airpal.</span></span>

        ![HDInsight launch Airpal on Presto cluster](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    3. <span data-ttu-id="f0ce5-168">When prompted, enter the admin credentials that you specified while creating the HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-168">When prompted, enter the admin credentials that you specified while creating the HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="f0ce5-169">Customize a Presto installation on HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="f0ce5-169">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="f0ce5-170">To customize the installation, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="f0ce5-170">To customize the installation, use the following steps:</span></span>

1. <span data-ttu-id="f0ce5-171">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span><span class="sxs-lookup"><span data-stu-id="f0ce5-171">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="f0ce5-172">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-172">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f0ce5-173">Make your configuration changes in the file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-173">Make your configuration changes in the file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="f0ce5-174">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-174">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="f0ce5-175">Stop and kill the current running instance of Presto.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-175">Stop and kill the current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="f0ce5-176">Start a new instance of Presto with the customization.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-176">Start a new instance of Presto with the customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="f0ce5-177">Wait for the new instance to be ready and note presto coordinator address.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-177">Wait for the new instance to be ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="f0ce5-178">Generate benchmark data for HDInsight clusters that run Presto</span><span class="sxs-lookup"><span data-stu-id="f0ce5-178">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="f0ce5-179">TPC-DS is the industry standard for measuring the performance of many decision support systems, including big data systems.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-179">TPC-DS is the industry standard for measuring the performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="f0ce5-180">You can use Presto to generate data and evaluate how it compares with your own HDInsight benchmark data.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-180">You can use Presto to generate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="f0ce5-181">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-181">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="f0ce5-182">See also</span><span class="sxs-lookup"><span data-stu-id="f0ce5-182">See also</span></span>
* <span data-ttu-id="f0ce5-183">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-183">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="f0ce5-184">Hue is a web UI that makes it easy to create, run, and save Pig and Hive jobs.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-184">Hue is a web UI that makes it easy to create, run, and save Pig and Hive jobs.</span></span>

* <span data-ttu-id="f0ce5-185">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-185">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="f0ce5-186">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-186">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="f0ce5-187">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-187">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="f0ce5-188">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f0ce5-188">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="f0ce5-189">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-189">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="f0ce5-190">Solr allows you to perform powerful search operations on stored data.</span><span class="sxs-lookup"><span data-stu-id="f0ce5-190">Solr allows you to perform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
