---
title: Use Azure Toolkit for IntelliJ to remote-debug applications on Spark clusters| Microsoft Docs
description: Learn how use HDInsight Tools in Azure Toolkit for IntelliJ to remotely debug applications running on HDInsight Spark clusters.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: fdad5aa2bd9533401b477b4eda26bb5b8981312a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555060"
---
# <a name="use-hdinsight-tools-in-azure-toolkit-for-intellij-to-debug-spark-applications-remotely-on-hdinsight-spark-cluster"></a><span data-ttu-id="cb73e-103">Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="cb73e-103">Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark cluster</span></span>
<span data-ttu-id="cb73e-104">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span><span class="sxs-lookup"><span data-stu-id="cb73e-104">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="cb73e-105">To do so, you must perform the following high-level steps:</span><span class="sxs-lookup"><span data-stu-id="cb73e-105">To do so, you must perform the following high-level steps:</span></span>

1. <span data-ttu-id="cb73e-106">Create a site-to-site or point-to-site Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="cb73e-106">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="cb73e-107">The steps in this document assume that you use a site-to-site network.</span><span class="sxs-lookup"><span data-stu-id="cb73e-107">The steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="cb73e-108">Create a Spark cluster in Azure HDInsight that is part of the site-to-site Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="cb73e-108">Create a Spark cluster in Azure HDInsight that is part of the site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="cb73e-109">Verify the connectivity between the cluster headnode and your desktop.</span><span class="sxs-lookup"><span data-stu-id="cb73e-109">Verify the connectivity between the cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="cb73e-110">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span><span class="sxs-lookup"><span data-stu-id="cb73e-110">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="cb73e-111">Run and debug the application.</span><span class="sxs-lookup"><span data-stu-id="cb73e-111">Run and debug the application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb73e-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cb73e-112">Prerequisites</span></span>
* <span data-ttu-id="cb73e-113">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="cb73e-113">An Azure subscription.</span></span> <span data-ttu-id="cb73e-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="cb73e-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="cb73e-115">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb73e-115">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="cb73e-116">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="cb73e-116">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="cb73e-117">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="cb73e-117">Oracle Java Development kit.</span></span> <span data-ttu-id="cb73e-118">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="cb73e-118">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="cb73e-119">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="cb73e-119">IntelliJ IDEA.</span></span> <span data-ttu-id="cb73e-120">This article uses version 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="cb73e-120">This article uses version 15.0.1.</span></span> <span data-ttu-id="cb73e-121">You can install it from [here](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="cb73e-121">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="cb73e-122">HDInsight Tools in Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="cb73e-122">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="cb73e-123">HDInsight tools for IntelliJ are available as part of the Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="cb73e-123">HDInsight tools for IntelliJ are available as part of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="cb73e-124">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="cb73e-124">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="cb73e-125">Log into your Azure Subscription from IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="cb73e-125">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="cb73e-126">Follow the instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md#log-into-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="cb73e-126">Follow the instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md#log-into-your-azure-subscription).</span></span>
* <span data-ttu-id="cb73e-127">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span><span class="sxs-lookup"><span data-stu-id="cb73e-127">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="cb73e-128">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-128">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="cb73e-129">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-129">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="cb73e-130">Step 1: Create an Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="cb73e-130">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="cb73e-131">Follow the instructions from the below links to create an Azure Virtual Network and then verify the connectivity between the desktop and Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="cb73e-131">Follow the instructions from the below links to create an Azure Virtual Network and then verify the connectivity between the desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="cb73e-132">Create a VNet with a site-to-site VPN connection using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cb73e-132">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="cb73e-133">Create a VNet with a site-to-site VPN connection using PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb73e-133">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="cb73e-134">Configure a point-to-site connection to a virtual network using PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb73e-134">Configure a point-to-site connection to a virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="cb73e-135">Step 2: Create an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="cb73e-135">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="cb73e-136">You should also create an Apache Spark cluster on Azure HDInsight that is part of the Azure Virtual Network that you created.</span><span class="sxs-lookup"><span data-stu-id="cb73e-136">You should also create an Apache Spark cluster on Azure HDInsight that is part of the Azure Virtual Network that you created.</span></span> <span data-ttu-id="cb73e-137">Use the information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="cb73e-137">Use the information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="cb73e-138">As part of optional configuration, select the Azure Virtual Network that you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="cb73e-138">As part of optional configuration, select the Azure Virtual Network that you created in the previous step.</span></span>

## <a name="step-3-verify-the-connectivity-between-the-cluster-headnode-and-your-desktop"></a><span data-ttu-id="cb73e-139">Step 3: Verify the connectivity between the cluster headnode and your desktop</span><span class="sxs-lookup"><span data-stu-id="cb73e-139">Step 3: Verify the connectivity between the cluster headnode and your desktop</span></span>
1. <span data-ttu-id="cb73e-140">Get the IP address of the headnode.</span><span class="sxs-lookup"><span data-stu-id="cb73e-140">Get the IP address of the headnode.</span></span> <span data-ttu-id="cb73e-141">Open Ambari UI for the cluster.</span><span class="sxs-lookup"><span data-stu-id="cb73e-141">Open Ambari UI for the cluster.</span></span> <span data-ttu-id="cb73e-142">From the cluster blade, click **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-142">From the cluster blade, click **Dashboard**.</span></span>
   
    ![Find headnode IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/launch-ambari-ui.png)
2. <span data-ttu-id="cb73e-144">From the Ambari UI, from the top-right corner, click **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-144">From the Ambari UI, from the top-right corner, click **Hosts**.</span></span>
   
    ![Find headnode IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/ambari-hosts.png)
3. <span data-ttu-id="cb73e-146">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span><span class="sxs-lookup"><span data-stu-id="cb73e-146">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="cb73e-147">The headnodes have the **hn**\* prefix.</span><span class="sxs-lookup"><span data-stu-id="cb73e-147">The headnodes have the **hn**\* prefix.</span></span> <span data-ttu-id="cb73e-148">Click the first headnode.</span><span class="sxs-lookup"><span data-stu-id="cb73e-148">Click the first headnode.</span></span>
   
    ![Find headnode IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/cluster-headnodes.png)
4. <span data-ttu-id="cb73e-150">At the bottom of the page that opens, from the **Summary** box, copy the IP address of the headnode and the host name.</span><span class="sxs-lookup"><span data-stu-id="cb73e-150">At the bottom of the page that opens, from the **Summary** box, copy the IP address of the headnode and the host name.</span></span>
   
    ![Find headnode IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/headnode-ip-address.png)
5. <span data-ttu-id="cb73e-152">Include the IP address and the host name of the headnode to the **hosts** file on the computer from where you want to run and remotely debug the Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="cb73e-152">Include the IP address and the host name of the headnode to the **hosts** file on the computer from where you want to run and remotely debug the Spark jobs.</span></span> <span data-ttu-id="cb73e-153">This will enable you to communicate with the headnode using the IP address as well as the hostname.</span><span class="sxs-lookup"><span data-stu-id="cb73e-153">This will enable you to communicate with the headnode using the IP address as well as the hostname.</span></span>
   
   1. <span data-ttu-id="cb73e-154">Open a notepad with elevated permissions.</span><span class="sxs-lookup"><span data-stu-id="cb73e-154">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="cb73e-155">From the file menu, click **Open** and then navigate to the location of the hosts file.</span><span class="sxs-lookup"><span data-stu-id="cb73e-155">From the file menu, click **Open** and then navigate to the location of the hosts file.</span></span> <span data-ttu-id="cb73e-156">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="cb73e-156">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="cb73e-157">Add the following to the **hosts** file.</span><span class="sxs-lookup"><span data-stu-id="cb73e-157">Add the following to the **hosts** file.</span></span>
      
           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
      
           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="cb73e-158">From the computer that you connected to the Azure Virtual Network that is used by the HDInsight cluster, verify that you can ping both the headnodes using the IP address as well as the hostname.</span><span class="sxs-lookup"><span data-stu-id="cb73e-158">From the computer that you connected to the Azure Virtual Network that is used by the HDInsight cluster, verify that you can ping both the headnodes using the IP address as well as the hostname.</span></span>
7. <span data-ttu-id="cb73e-159">SSH into the cluster headnode using the instructions at [Connect to an HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cb73e-159">SSH into the cluster headnode using the instructions at [Connect to an HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="cb73e-160">From the cluster headnode, ping the IP address of the desktop computer.</span><span class="sxs-lookup"><span data-stu-id="cb73e-160">From the cluster headnode, ping the IP address of the desktop computer.</span></span> <span data-ttu-id="cb73e-161">You should test connectivity to both the IP addresses assigned to the computer, one for the network connection and the other for the Azure Virtual Network that the computer is connected to.</span><span class="sxs-lookup"><span data-stu-id="cb73e-161">You should test connectivity to both the IP addresses assigned to the computer, one for the network connection and the other for the Azure Virtual Network that the computer is connected to.</span></span>
8. <span data-ttu-id="cb73e-162">Repeat the steps for the other headnode as well.</span><span class="sxs-lookup"><span data-stu-id="cb73e-162">Repeat the steps for the other headnode as well.</span></span> 

## <a name="step-4-create-a-spark-scala-application-using-the-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="cb73e-163">Step 4: Create a Spark Scala application using the HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span><span class="sxs-lookup"><span data-stu-id="cb73e-163">Step 4: Create a Spark Scala application using the HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="cb73e-164">Launch IntelliJ IDEA and create a new project.</span><span class="sxs-lookup"><span data-stu-id="cb73e-164">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="cb73e-165">In the new project dialog box, make the following choices, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-165">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)
   
   * <span data-ttu-id="cb73e-167">From the left pane, select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-167">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="cb73e-168">From the right pane, select **Spark on HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-168">From the right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="cb73e-169">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-169">Click **Next**.</span></span>
2. <span data-ttu-id="cb73e-170">In the next window, provide the project details.</span><span class="sxs-lookup"><span data-stu-id="cb73e-170">In the next window, provide the project details.</span></span>
   
   * <span data-ttu-id="cb73e-171">Provide a project name and project location.</span><span class="sxs-lookup"><span data-stu-id="cb73e-171">Provide a project name and project location.</span></span>
   * <span data-ttu-id="cb73e-172">For **Project SDK**, make sure you provide a Java version greater than 7.</span><span class="sxs-lookup"><span data-stu-id="cb73e-172">For **Project SDK**, make sure you provide a Java version greater than 7.</span></span>
   * <span data-ttu-id="cb73e-173">For **Scala SDK**, click **Create**, click **Download**, and then select the version of Scala to use.</span><span class="sxs-lookup"><span data-stu-id="cb73e-173">For **Scala SDK**, click **Create**, click **Download**, and then select the version of Scala to use.</span></span> <span data-ttu-id="cb73e-174">**Make sure you do not use version 2.11.x**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-174">**Make sure you do not use version 2.11.x**.</span></span> <span data-ttu-id="cb73e-175">This sample uses version **2.10.6**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-175">This sample uses version **2.10.6**.</span></span>
     
       ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/hdi-scala-version.png)
   * <span data-ttu-id="cb73e-177">For **Spark SDK**, download and use the SDK from [here](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cb73e-177">For **Spark SDK**, download and use the SDK from [here](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span> <span data-ttu-id="cb73e-178">You can also ignore this and use the [Spark Maven repository](http://mvnrepository.com/search?q=spark) instead, however please make sure you have the right maven repository installed to develop your Spark applications.</span><span class="sxs-lookup"><span data-stu-id="cb73e-178">You can also ignore this and use the [Spark Maven repository](http://mvnrepository.com/search?q=spark) instead, however please make sure you have the right maven repository installed to develop your Spark applications.</span></span> <span data-ttu-id="cb73e-179">(For example, you need to make sure you have the Spark Streaming part installed if you are using Spark Streaming; Also please make sure you are using the repository marked as Scala 2.10 - do not use the repository marked as Scala 2.11.)</span><span class="sxs-lookup"><span data-stu-id="cb73e-179">(For example, you need to make sure you have the Spark Streaming part installed if you are using Spark Streaming; Also please make sure you are using the repository marked as Scala 2.10 - do not use the repository marked as Scala 2.11.)</span></span>
     
       ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/hdi-scala-project-details.png)
   * <span data-ttu-id="cb73e-181">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-181">Click **Finish**.</span></span>
3. <span data-ttu-id="cb73e-182">The Spark project will automatically create an artifact for you.</span><span class="sxs-lookup"><span data-stu-id="cb73e-182">The Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="cb73e-183">To see the artifact, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="cb73e-183">To see the artifact, follow these steps.</span></span>
   
   1. <span data-ttu-id="cb73e-184">From the **File** menu, click **Project Structure**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-184">From the **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="cb73e-185">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span><span class="sxs-lookup"><span data-stu-id="cb73e-185">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span></span>
      
       ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/default-artifact.png)
      
      <span data-ttu-id="cb73e-187">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span><span class="sxs-lookup"><span data-stu-id="cb73e-187">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span></span>
4. <span data-ttu-id="cb73e-188">In the **Project Structure** dialog box, click **Project**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-188">In the **Project Structure** dialog box, click **Project**.</span></span> <span data-ttu-id="cb73e-189">If the **Project SDK** is set to 1.8, make sure the **Project language level** is set to **7 - Diamonds, ARM, multi-catch, etc**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-189">If the **Project SDK** is set to 1.8, make sure the **Project language level** is set to **7 - Diamonds, ARM, multi-catch, etc**.</span></span>
   
    ![Set project language level](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/set-project-language-level.png)
5. <span data-ttu-id="cb73e-191">Add libraries to your project.</span><span class="sxs-lookup"><span data-stu-id="cb73e-191">Add libraries to your project.</span></span> <span data-ttu-id="cb73e-192">To add a library, right-click the project name in the project tree, and then click **Open Module Settings**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-192">To add a library, right-click the project name in the project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="cb73e-193">In the **Project Structure** dialog box, from the left pane, click **Libraries**, click the (+) symbol, and then click **From Maven**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-193">In the **Project Structure** dialog box, from the left pane, click **Libraries**, click the (+) symbol, and then click **From Maven**.</span></span> 
   
    ![Add library](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/add-library.png) 
   
    <span data-ttu-id="cb73e-195">In the **Download Library from Maven Repository** dialog box, search and add the following libraries.</span><span class="sxs-lookup"><span data-stu-id="cb73e-195">In the **Download Library from Maven Repository** dialog box, search and add the following libraries.</span></span>
   
   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
6. <span data-ttu-id="cb73e-196">Copy `yarn-site.xml` and `core-site.xml` from the cluster headnode and add it to the project.</span><span class="sxs-lookup"><span data-stu-id="cb73e-196">Copy `yarn-site.xml` and `core-site.xml` from the cluster headnode and add it to the project.</span></span> <span data-ttu-id="cb73e-197">Use the following commands to copy the files.</span><span class="sxs-lookup"><span data-stu-id="cb73e-197">Use the following commands to copy the files.</span></span> <span data-ttu-id="cb73e-198">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster headnodes.</span><span class="sxs-lookup"><span data-stu-id="cb73e-198">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster headnodes.</span></span>
   
        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .
   
    <span data-ttu-id="cb73e-199">Because we already added the cluster headnode IP address and hostnames fo the hosts file on the desktop, we can use the **scp** commands in the following manner.</span><span class="sxs-lookup"><span data-stu-id="cb73e-199">Because we already added the cluster headnode IP address and hostnames fo the hosts file on the desktop, we can use the **scp** commands in the following manner.</span></span>
   
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .
   
    <span data-ttu-id="cb73e-200">Add these files to your project by copying them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="cb73e-200">Add these files to your project by copying them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
7. <span data-ttu-id="cb73e-201">Update the `core-site.xml` to make the following changes.</span><span class="sxs-lookup"><span data-stu-id="cb73e-201">Update the `core-site.xml` to make the following changes.</span></span>
   
   1. <span data-ttu-id="cb73e-202">`core-site.xml` includes the encrypted key to the storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="cb73e-202">`core-site.xml` includes the encrypted key to the storage account associated with the cluster.</span></span> <span data-ttu-id="cb73e-203">In the `core-site.xml` that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span><span class="sxs-lookup"><span data-stu-id="cb73e-203">In the `core-site.xml` that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span></span> <span data-ttu-id="cb73e-204">See [Manage your storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cb73e-204">See [Manage your storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-account).</span></span>
      
           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="cb73e-205">Remove the following entries from the `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="cb73e-205">Remove the following entries from the `core-site.xml`.</span></span>
      
           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>
      
           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>
      
           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="cb73e-206">Save the file.</span><span class="sxs-lookup"><span data-stu-id="cb73e-206">Save the file.</span></span>
8. <span data-ttu-id="cb73e-207">Add the Main class for your application.</span><span class="sxs-lookup"><span data-stu-id="cb73e-207">Add the Main class for your application.</span></span> <span data-ttu-id="cb73e-208">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-208">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span></span>
   
    ![Add source code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/hdi-spark-scala-code.png)
9. <span data-ttu-id="cb73e-210">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-210">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>
   
    ![Add source code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/hdi-spark-scala-code-object.png)
10. <span data-ttu-id="cb73e-212">In the `MyClusterAppMain.scala` file, paste the following code.</span><span class="sxs-lookup"><span data-stu-id="cb73e-212">In the `MyClusterAppMain.scala` file, paste the following code.</span></span> <span data-ttu-id="cb73e-213">This code creates the Spark context and launches an `executeJob` method from the `SparkSample` object.</span><span class="sxs-lookup"><span data-stu-id="cb73e-213">This code creates the Spark context and launches an `executeJob` method from the `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasbs:///HVACOut")
          }
        }

1. <span data-ttu-id="cb73e-214">Repeat steps 8 and 9 above to add a new Scala object called `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="cb73e-214">Repeat steps 8 and 9 above to add a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="cb73e-215">To this class add the following code.</span><span class="sxs-lookup"><span data-stu-id="cb73e-215">To this class add the following code.</span></span> <span data-ttu-id="cb73e-216">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span><span class="sxs-lookup"><span data-stu-id="cb73e-216">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>
   
       import org.apache.spark.SparkContext
   
       object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)
   
           //find the rows which have only one digit in the 7th column in the CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)
   
           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
   
       }
2. <span data-ttu-id="cb73e-217">Repeat steps 8 and 9 above to add a new class called `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="cb73e-217">Repeat steps 8 and 9 above to add a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="cb73e-218">This class implements the Spark test framework that is used for debugging applications.</span><span class="sxs-lookup"><span data-stu-id="cb73e-218">This class implements the Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="cb73e-219">Add the following code to the `RemoteClusterDebugging` class.</span><span class="sxs-lookup"><span data-stu-id="cb73e-219">Add the following code to the `RemoteClusterDebugging` class.</span></span>
   
       import org.apache.spark.{SparkConf, SparkContext}
       import org.scalatest.FunSuite
   
       class RemoteClusterDebugging extends FunSuite {
   
         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasbs:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\WORK\IntelliJApps\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)
   
           SparkSample.executeJob(sc,
             "wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasbs:///HVACOut")
         }
       }
   
   <span data-ttu-id="cb73e-220">Couple of important things to note here:</span><span class="sxs-lookup"><span data-stu-id="cb73e-220">Couple of important things to note here:</span></span>
   
   * <span data-ttu-id="cb73e-221">For `.set("spark.yarn.jar", "wasbs:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span><span class="sxs-lookup"><span data-stu-id="cb73e-221">For `.set("spark.yarn.jar", "wasbs:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span></span>
   * <span data-ttu-id="cb73e-222">For `setJars`, specify the location where the artifact jar will be created.</span><span class="sxs-lookup"><span data-stu-id="cb73e-222">For `setJars`, specify the location where the artifact jar will be created.</span></span> <span data-ttu-id="cb73e-223">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="cb73e-223">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span> 
3. <span data-ttu-id="cb73e-224">In the `RemoteClusterDebugging` class, right-click the `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-224">In the `RemoteClusterDebugging` class, right-click the `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>
   
   ![Create remote configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/create-remote-config.png)
4. <span data-ttu-id="cb73e-226">In the dialog box, provide a name for the configuration, and select the **Test kind** as **Test name**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-226">In the dialog box, provide a name for the configuration, and select the **Test kind** as **Test name**.</span></span> <span data-ttu-id="cb73e-227">Leave all other values as default, click **Apply**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-227">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>
   
   ![Create remote configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/provide-config-value.png)
5. <span data-ttu-id="cb73e-229">You should now see a **Remote Run** configuration drop-down in the menu bar.</span><span class="sxs-lookup"><span data-stu-id="cb73e-229">You should now see a **Remote Run** configuration drop-down in the menu bar.</span></span> 
   
   ![Create remote configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/config-run.png)

## <a name="step-5-run-the-application-in-debug-mode"></a><span data-ttu-id="cb73e-231">Step 5: Run the application in debug mode</span><span class="sxs-lookup"><span data-stu-id="cb73e-231">Step 5: Run the application in debug mode</span></span>
1. <span data-ttu-id="cb73e-232">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to \`val rdd1'.</span><span class="sxs-lookup"><span data-stu-id="cb73e-232">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to \`val rdd1'.</span></span> <span data-ttu-id="cb73e-233">In the pop-up menu for creating a breakpoint, select **line in function executeJob**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-233">In the pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>
   
    ![Add a breakpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/create-breakpoint.png)
2. <span data-ttu-id="cb73e-235">Click the **Debug Run** button next to the **Remote Run** configuration drop-down to start running the application.</span><span class="sxs-lookup"><span data-stu-id="cb73e-235">Click the **Debug Run** button next to the **Remote Run** configuration drop-down to start running the application.</span></span>
   
    ![Run the program in debug mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-run-mode.png)
3. <span data-ttu-id="cb73e-237">When the program execution reaches the breakpoint, you should see a **Debugger** tab in the bottom pane.</span><span class="sxs-lookup"><span data-stu-id="cb73e-237">When the program execution reaches the breakpoint, you should see a **Debugger** tab in the bottom pane.</span></span>
   
    ![Run the program in debug mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-add-watch.png)
4. <span data-ttu-id="cb73e-239">Click the (**+**) icon to add a watch as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="cb73e-239">Click the (**+**) icon to add a watch as shown in the image below.</span></span> 
   
    ![Run the program in debug mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-add-watch-variable.png)
   
    <span data-ttu-id="cb73e-241">Here, because the application broke before the variable `rdd1` was created, using this watch we can see what are the first 5 rows in the variable `rdd`.</span><span class="sxs-lookup"><span data-stu-id="cb73e-241">Here, because the application broke before the variable `rdd1` was created, using this watch we can see what are the first 5 rows in the variable `rdd`.</span></span> <span data-ttu-id="cb73e-242">Press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="cb73e-242">Press **ENTER**.</span></span>
   
    ![Run the program in debug mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-add-watch-variable-value.png)
   
    <span data-ttu-id="cb73e-244">What you see in the image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span><span class="sxs-lookup"><span data-stu-id="cb73e-244">What you see in the image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="cb73e-245">For example, in the output shown in the image above, you can see that the first row of the output is a header.</span><span class="sxs-lookup"><span data-stu-id="cb73e-245">For example, in the output shown in the image above, you can see that the first row of the output is a header.</span></span> <span data-ttu-id="cb73e-246">Based on this, you can modify your application code to skip the header row if required.</span><span class="sxs-lookup"><span data-stu-id="cb73e-246">Based on this, you can modify your application code to skip the header row if required.</span></span>
5. <span data-ttu-id="cb73e-247">You can now click the **Resume Program** icon to proceed with your application run.</span><span class="sxs-lookup"><span data-stu-id="cb73e-247">You can now click the **Resume Program** icon to proceed with your application run.</span></span>
   
    ![Run the program in debug mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-continue-run.png)
6. <span data-ttu-id="cb73e-249">If the application completes successfully, you should see an output like the following.</span><span class="sxs-lookup"><span data-stu-id="cb73e-249">If the application completes successfully, you should see an output like the following.</span></span>
   
    ![Run the program in debug mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-complete.png)

## <a name="seealso"></a><span data-ttu-id="cb73e-251">See also</span><span class="sxs-lookup"><span data-stu-id="cb73e-251">See also</span></span>
* [<span data-ttu-id="cb73e-252">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb73e-252">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="cb73e-253">Scenarios</span><span class="sxs-lookup"><span data-stu-id="cb73e-253">Scenarios</span></span>
* [<span data-ttu-id="cb73e-254">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="cb73e-254">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="cb73e-255">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="cb73e-255">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="cb73e-256">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="cb73e-256">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="cb73e-257">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="cb73e-257">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="cb73e-258">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb73e-258">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="cb73e-259">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="cb73e-259">Create and run applications</span></span>
* [<span data-ttu-id="cb73e-260">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="cb73e-260">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="cb73e-261">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="cb73e-261">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="cb73e-262">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="cb73e-262">Tools and extensions</span></span>
* [<span data-ttu-id="cb73e-263">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="cb73e-263">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="cb73e-264">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span><span class="sxs-lookup"><span data-stu-id="cb73e-264">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="cb73e-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb73e-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="cb73e-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb73e-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="cb73e-267">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="cb73e-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="cb73e-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="cb73e-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="cb73e-269">Manage resources</span><span class="sxs-lookup"><span data-stu-id="cb73e-269">Manage resources</span></span>
* [<span data-ttu-id="cb73e-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb73e-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="cb73e-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb73e-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)























