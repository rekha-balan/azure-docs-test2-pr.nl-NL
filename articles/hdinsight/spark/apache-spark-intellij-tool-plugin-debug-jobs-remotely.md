---
title: 'Azure Toolkit for IntelliJ: Debug applications remotely in HDInsight Spark '
description: Learn how use HDInsight Tools in Azure Toolkit for IntelliJ to remotely debug Spark applications that run on HDInsight clusters through VPN.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 11/28/2017
ms.openlocfilehash: bc1f1dd577231f5b22474f6cd3dc622480209dd9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871175"
---
# <a name="use-azure-toolkit-for-intellij-to-debug-spark-applications-remotely-in-hdinsight-through-vpn"></a><span data-ttu-id="b1d41-103">Use Azure Toolkit for IntelliJ to debug Spark applications remotely in HDInsight through VPN</span><span class="sxs-lookup"><span data-stu-id="b1d41-103">Use Azure Toolkit for IntelliJ to debug Spark applications remotely in HDInsight through VPN</span></span>

<span data-ttu-id="b1d41-104">We recommend debugging spark applications remotely through SSH.</span><span class="sxs-lookup"><span data-stu-id="b1d41-104">We recommend debugging spark applications remotely through SSH.</span></span> <span data-ttu-id="b1d41-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="b1d41-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="b1d41-106">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on an HDInsight Spark cluster, and then debug it remotely from your desktop computer.</span><span class="sxs-lookup"><span data-stu-id="b1d41-106">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on an HDInsight Spark cluster, and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="b1d41-107">To complete these tasks, you must perform the following high-level steps:</span><span class="sxs-lookup"><span data-stu-id="b1d41-107">To complete these tasks, you must perform the following high-level steps:</span></span>

1. <span data-ttu-id="b1d41-108">Create a site-to-site or point-to-site Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="b1d41-108">Create a site-to-site or point-to-site Azure virtual network.</span></span> <span data-ttu-id="b1d41-109">The steps in this document assume that you use a site-to-site network.</span><span class="sxs-lookup"><span data-stu-id="b1d41-109">The steps in this document assume that you use a site-to-site network.</span></span>
1. <span data-ttu-id="b1d41-110">Create a Spark cluster in HDInsight that is part of the site-to-site virtual network.</span><span class="sxs-lookup"><span data-stu-id="b1d41-110">Create a Spark cluster in HDInsight that is part of the site-to-site virtual network.</span></span>
1. <span data-ttu-id="b1d41-111">Verify the connectivity between the cluster head node and your desktop.</span><span class="sxs-lookup"><span data-stu-id="b1d41-111">Verify the connectivity between the cluster head node and your desktop.</span></span>
1. <span data-ttu-id="b1d41-112">Create a Scala application in IntelliJ IDEA, and then configure it for remote debugging.</span><span class="sxs-lookup"><span data-stu-id="b1d41-112">Create a Scala application in IntelliJ IDEA, and then configure it for remote debugging.</span></span>
1. <span data-ttu-id="b1d41-113">Run and debug the application.</span><span class="sxs-lookup"><span data-stu-id="b1d41-113">Run and debug the application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1d41-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b1d41-114">Prerequisites</span></span>
* <span data-ttu-id="b1d41-115">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-115">**An Azure subscription**.</span></span> <span data-ttu-id="b1d41-116">For more information, see [Get a free trial of Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b1d41-116">For more information, see [Get a free trial of Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b1d41-117">**An Apache Spark cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-117">**An Apache Spark cluster in HDInsight**.</span></span> <span data-ttu-id="b1d41-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b1d41-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="b1d41-119">**Oracle Java development kit**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-119">**Oracle Java development kit**.</span></span> <span data-ttu-id="b1d41-120">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="b1d41-120">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="b1d41-121">**IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-121">**IntelliJ IDEA**.</span></span> <span data-ttu-id="b1d41-122">This article uses version 2017.1.</span><span class="sxs-lookup"><span data-stu-id="b1d41-122">This article uses version 2017.1.</span></span> <span data-ttu-id="b1d41-123">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="b1d41-123">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="b1d41-124">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-124">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="b1d41-125">HDInsight tools for IntelliJ are available as part of Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="b1d41-125">HDInsight tools for IntelliJ are available as part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="b1d41-126">For instructions on how to install Azure Toolkit, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="b1d41-126">For instructions on how to install Azure Toolkit, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="b1d41-127">**Sign in to your Azure Subscription from IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-127">**Sign in to your Azure Subscription from IntelliJ IDEA**.</span></span> <span data-ttu-id="b1d41-128">Follow the instructions in [Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster](apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="b1d41-128">Follow the instructions in [Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster](apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="b1d41-129">**Exception workaround**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-129">**Exception workaround**.</span></span> <span data-ttu-id="b1d41-130">While running the Spark Scala application for remote debugging on a Windows computer, you might get an exception.</span><span class="sxs-lookup"><span data-stu-id="b1d41-130">While running the Spark Scala application for remote debugging on a Windows computer, you might get an exception.</span></span> <span data-ttu-id="b1d41-131">This exception is explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) and occurs due to a missing WinUtils.exe file in Windows.</span><span class="sxs-lookup"><span data-stu-id="b1d41-131">This exception is explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) and occurs due to a missing WinUtils.exe file in Windows.</span></span> <span data-ttu-id="b1d41-132">To work around this error, you must [download the executable file](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location such as **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-132">To work around this error, you must [download the executable file](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="b1d41-133">Add an **HADOOP_HOME** environment variable, and then set the value of the variable to **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-133">Add an **HADOOP_HOME** environment variable, and then set the value of the variable to **C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="b1d41-134">Step 1: Create an Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="b1d41-134">Step 1: Create an Azure virtual network</span></span>
<span data-ttu-id="b1d41-135">Follow the instructions from the following links to create an Azure virtual network, and then verify the connectivity between your desktop computer and the virtual network:</span><span class="sxs-lookup"><span data-stu-id="b1d41-135">Follow the instructions from the following links to create an Azure virtual network, and then verify the connectivity between your desktop computer and the virtual network:</span></span>

* [<span data-ttu-id="b1d41-136">Create a VNet with a site-to-site VPN connection using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b1d41-136">Create a VNet with a site-to-site VPN connection using the Azure portal</span></span>](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="b1d41-137">Create a VNet with a site-to-site VPN connection using PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1d41-137">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="b1d41-138">Configure a point-to-site connection to a virtual network using PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1d41-138">Configure a point-to-site connection to a virtual network using PowerShell</span></span>](../../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="b1d41-139">Step 2: Create an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="b1d41-139">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="b1d41-140">We recommend that you also create an Apache Spark cluster in Azure HDInsight that is part of the Azure virtual network that you created.</span><span class="sxs-lookup"><span data-stu-id="b1d41-140">We recommend that you also create an Apache Spark cluster in Azure HDInsight that is part of the Azure virtual network that you created.</span></span> <span data-ttu-id="b1d41-141">Use the information available in [Create Linux-based clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b1d41-141">Use the information available in [Create Linux-based clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="b1d41-142">As part of optional configuration, select the Azure virtual network that you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="b1d41-142">As part of optional configuration, select the Azure virtual network that you created in the previous step.</span></span>

## <a name="step-3-verify-the-connectivity-between-the-cluster-head-node-and-your-desktop"></a><span data-ttu-id="b1d41-143">Step 3: Verify the connectivity between the cluster head node and your desktop</span><span class="sxs-lookup"><span data-stu-id="b1d41-143">Step 3: Verify the connectivity between the cluster head node and your desktop</span></span>
1. <span data-ttu-id="b1d41-144">Get the IP address of the head node.</span><span class="sxs-lookup"><span data-stu-id="b1d41-144">Get the IP address of the head node.</span></span> <span data-ttu-id="b1d41-145">Open Ambari UI for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1d41-145">Open Ambari UI for the cluster.</span></span> <span data-ttu-id="b1d41-146">From the cluster blade, select **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-146">From the cluster blade, select **Dashboard**.</span></span>

    ![Select Dashboard in Ambari](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/launch-ambari-ui.png)
1. <span data-ttu-id="b1d41-148">From the Ambari UI, select **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-148">From the Ambari UI, select **Hosts**.</span></span>

    ![Select Hosts in Ambari](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/ambari-hosts.png)
1. <span data-ttu-id="b1d41-150">You see a list of head nodes, worker nodes, and zookeeper nodes.</span><span class="sxs-lookup"><span data-stu-id="b1d41-150">You see a list of head nodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="b1d41-151">The head nodes have an **hn**\* prefix.</span><span class="sxs-lookup"><span data-stu-id="b1d41-151">The head nodes have an **hn**\* prefix.</span></span> <span data-ttu-id="b1d41-152">Select the first head node.</span><span class="sxs-lookup"><span data-stu-id="b1d41-152">Select the first head node.</span></span>

    ![Find the head node in Ambari](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/cluster-headnodes.png)
1. <span data-ttu-id="b1d41-154">From the **Summary** pane at the bottom of the page that opens, copy the **IP Address** of the head node and the **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-154">From the **Summary** pane at the bottom of the page that opens, copy the **IP Address** of the head node and the **Hostname**.</span></span>

    ![Find the IP address in Ambari](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/headnode-ip-address.png)
1. <span data-ttu-id="b1d41-156">Add the IP address and the hostname of the head node to the **hosts** file on the computer where you want to run and remotely debug the Spark job.</span><span class="sxs-lookup"><span data-stu-id="b1d41-156">Add the IP address and the hostname of the head node to the **hosts** file on the computer where you want to run and remotely debug the Spark job.</span></span> <span data-ttu-id="b1d41-157">This enables you to communicate with the head node by using the IP address, as well as the hostname.</span><span class="sxs-lookup"><span data-stu-id="b1d41-157">This enables you to communicate with the head node by using the IP address, as well as the hostname.</span></span>

   <span data-ttu-id="b1d41-158">a.</span><span class="sxs-lookup"><span data-stu-id="b1d41-158">a.</span></span> <span data-ttu-id="b1d41-159">Open a Notepad file with elevated permissions.</span><span class="sxs-lookup"><span data-stu-id="b1d41-159">Open a Notepad file with elevated permissions.</span></span> <span data-ttu-id="b1d41-160">From the **File** menu, select **Open**, and then find the location of the hosts file.</span><span class="sxs-lookup"><span data-stu-id="b1d41-160">From the **File** menu, select **Open**, and then find the location of the hosts file.</span></span> <span data-ttu-id="b1d41-161">On a Windows computer, the location is **C:\Windows\System32\Drivers\etc\hosts**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-161">On a Windows computer, the location is **C:\Windows\System32\Drivers\etc\hosts**.</span></span>

   <span data-ttu-id="b1d41-162">b.</span><span class="sxs-lookup"><span data-stu-id="b1d41-162">b.</span></span> <span data-ttu-id="b1d41-163">Add the following information to the **hosts** file:</span><span class="sxs-lookup"><span data-stu-id="b1d41-163">Add the following information to the **hosts** file:</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
1. <span data-ttu-id="b1d41-164">From the computer that you connected to the Azure virtual network that is used by the HDInsight cluster, verify that you can ping the head nodes by using the IP address, as well as the hostname.</span><span class="sxs-lookup"><span data-stu-id="b1d41-164">From the computer that you connected to the Azure virtual network that is used by the HDInsight cluster, verify that you can ping the head nodes by using the IP address, as well as the hostname.</span></span>
1. <span data-ttu-id="b1d41-165">Use SSH to connect to the cluster head node by following the instructions in [Connect to an HDInsight cluster using SSH](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b1d41-165">Use SSH to connect to the cluster head node by following the instructions in [Connect to an HDInsight cluster using SSH](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="b1d41-166">From the cluster head node, ping the IP address of the desktop computer.</span><span class="sxs-lookup"><span data-stu-id="b1d41-166">From the cluster head node, ping the IP address of the desktop computer.</span></span> <span data-ttu-id="b1d41-167">Test the connectivity to both IP addresses assigned to the computer:</span><span class="sxs-lookup"><span data-stu-id="b1d41-167">Test the connectivity to both IP addresses assigned to the computer:</span></span>

    - <span data-ttu-id="b1d41-168">One for the network connection</span><span class="sxs-lookup"><span data-stu-id="b1d41-168">One for the network connection</span></span>
    - <span data-ttu-id="b1d41-169">One for the Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="b1d41-169">One for the Azure virtual network</span></span>

1. <span data-ttu-id="b1d41-170">Repeat the steps for the other head node.</span><span class="sxs-lookup"><span data-stu-id="b1d41-170">Repeat the steps for the other head node.</span></span>

## <a name="step-4-create-a-spark-scala-application-by-using-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="b1d41-171">Step 4: Create a Spark Scala application by using HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span><span class="sxs-lookup"><span data-stu-id="b1d41-171">Step 4: Create a Spark Scala application by using HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="b1d41-172">Open IntelliJ IDEA and create a new project.</span><span class="sxs-lookup"><span data-stu-id="b1d41-172">Open IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="b1d41-173">In the **New Project** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="b1d41-173">In the **New Project** dialog box, do the following:</span></span>

    ![Select the new project template in IntelliJ IDEA](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/create-hdi-scala-app.png)

    <span data-ttu-id="b1d41-175">a.</span><span class="sxs-lookup"><span data-stu-id="b1d41-175">a.</span></span> <span data-ttu-id="b1d41-176">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-176">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

    <span data-ttu-id="b1d41-177">b.</span><span class="sxs-lookup"><span data-stu-id="b1d41-177">b.</span></span> <span data-ttu-id="b1d41-178">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-178">Select **Next**.</span></span>
1. <span data-ttu-id="b1d41-179">In the next **New Project** dialog box, do the following, and then select **Finish**:</span><span class="sxs-lookup"><span data-stu-id="b1d41-179">In the next **New Project** dialog box, do the following, and then select **Finish**:</span></span>

    - <span data-ttu-id="b1d41-180">Enter a project name and location.</span><span class="sxs-lookup"><span data-stu-id="b1d41-180">Enter a project name and location.</span></span>

    - <span data-ttu-id="b1d41-181">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span><span class="sxs-lookup"><span data-stu-id="b1d41-181">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

    - <span data-ttu-id="b1d41-182">In the **Spark version** drop-down list, the Scala project creation wizard integrates the proper version for the Spark SDK and the Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="b1d41-182">In the **Spark version** drop-down list, the Scala project creation wizard integrates the proper version for the Spark SDK and the Scala SDK.</span></span> <span data-ttu-id="b1d41-183">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-183">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="b1d41-184">Otherwise, select **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-184">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="b1d41-185">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-185">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>
  
   ![Select the project SDK and Spark version](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/hdi-scala-project-details.png)
  
1. <span data-ttu-id="b1d41-187">The Spark project automatically creates an artifact for you.</span><span class="sxs-lookup"><span data-stu-id="b1d41-187">The Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="b1d41-188">To view the artifact, do the following:</span><span class="sxs-lookup"><span data-stu-id="b1d41-188">To view the artifact, do the following:</span></span>

    <span data-ttu-id="b1d41-189">a.</span><span class="sxs-lookup"><span data-stu-id="b1d41-189">a.</span></span> <span data-ttu-id="b1d41-190">From the **File** menu, select **Project Structure**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-190">From the **File** menu, select **Project Structure**.</span></span>

    <span data-ttu-id="b1d41-191">b.</span><span class="sxs-lookup"><span data-stu-id="b1d41-191">b.</span></span> <span data-ttu-id="b1d41-192">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span><span class="sxs-lookup"><span data-stu-id="b1d41-192">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span></span> <span data-ttu-id="b1d41-193">You can also create your own artifact by selecting the plus sign (**+**).</span><span class="sxs-lookup"><span data-stu-id="b1d41-193">You can also create your own artifact by selecting the plus sign (**+**).</span></span>

   ![Create JAR](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/default-artifact.png)


1. <span data-ttu-id="b1d41-195">Add libraries to your project.</span><span class="sxs-lookup"><span data-stu-id="b1d41-195">Add libraries to your project.</span></span> <span data-ttu-id="b1d41-196">To add a library, do the following:</span><span class="sxs-lookup"><span data-stu-id="b1d41-196">To add a library, do the following:</span></span>

    <span data-ttu-id="b1d41-197">a.</span><span class="sxs-lookup"><span data-stu-id="b1d41-197">a.</span></span> <span data-ttu-id="b1d41-198">Right-click the project name in the project tree, and then select **Open Module Settings**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-198">Right-click the project name in the project tree, and then select **Open Module Settings**.</span></span> 

    <span data-ttu-id="b1d41-199">b.</span><span class="sxs-lookup"><span data-stu-id="b1d41-199">b.</span></span> <span data-ttu-id="b1d41-200">In the **Project Structure** dialog box, select **Libraries**, select the (**+**) symbol, and then select **From Maven**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-200">In the **Project Structure** dialog box, select **Libraries**, select the (**+**) symbol, and then select **From Maven**.</span></span>

    ![Add a library](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/add-library.png)

    <span data-ttu-id="b1d41-202">c.</span><span class="sxs-lookup"><span data-stu-id="b1d41-202">c.</span></span> <span data-ttu-id="b1d41-203">In the **Download Library from Maven Repository** dialog box, search for and add the following libraries:</span><span class="sxs-lookup"><span data-stu-id="b1d41-203">In the **Download Library from Maven Repository** dialog box, search for and add the following libraries:</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
1. <span data-ttu-id="b1d41-204">Copy `yarn-site.xml` and `core-site.xml` from the cluster head node and add them to the project.</span><span class="sxs-lookup"><span data-stu-id="b1d41-204">Copy `yarn-site.xml` and `core-site.xml` from the cluster head node and add them to the project.</span></span> <span data-ttu-id="b1d41-205">Use the following commands to copy the files.</span><span class="sxs-lookup"><span data-stu-id="b1d41-205">Use the following commands to copy the files.</span></span> <span data-ttu-id="b1d41-206">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster head nodes:</span><span class="sxs-lookup"><span data-stu-id="b1d41-206">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster head nodes:</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="b1d41-207">Because we already added the cluster head node IP address and hostnames for the hosts file on the desktop, we can use the `scp` commands in the following manner:</span><span class="sxs-lookup"><span data-stu-id="b1d41-207">Because we already added the cluster head node IP address and hostnames for the hosts file on the desktop, we can use the `scp` commands in the following manner:</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="b1d41-208">To add these files to your project, copy them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="b1d41-208">To add these files to your project, copy them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
1. <span data-ttu-id="b1d41-209">Update the `core-site.xml` file to make the following changes:</span><span class="sxs-lookup"><span data-stu-id="b1d41-209">Update the `core-site.xml` file to make the following changes:</span></span>

   <span data-ttu-id="b1d41-210">a.</span><span class="sxs-lookup"><span data-stu-id="b1d41-210">a.</span></span> <span data-ttu-id="b1d41-211">Replace the encrypted key.</span><span class="sxs-lookup"><span data-stu-id="b1d41-211">Replace the encrypted key.</span></span> <span data-ttu-id="b1d41-212">The `core-site.xml` file includes the encrypted key to the storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1d41-212">The `core-site.xml` file includes the encrypted key to the storage account associated with the cluster.</span></span> <span data-ttu-id="b1d41-213">In the `core-site.xml` file that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span><span class="sxs-lookup"><span data-stu-id="b1d41-213">In the `core-site.xml` file that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span></span> <span data-ttu-id="b1d41-214">For more information, see [Manage your storage access keys](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b1d41-214">For more information, see [Manage your storage access keys](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   <span data-ttu-id="b1d41-215">b.</span><span class="sxs-lookup"><span data-stu-id="b1d41-215">b.</span></span> <span data-ttu-id="b1d41-216">Remove the following entries from `core-site.xml`:</span><span class="sxs-lookup"><span data-stu-id="b1d41-216">Remove the following entries from `core-site.xml`:</span></span>

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
   <span data-ttu-id="b1d41-217">c.</span><span class="sxs-lookup"><span data-stu-id="b1d41-217">c.</span></span> <span data-ttu-id="b1d41-218">Save the file.</span><span class="sxs-lookup"><span data-stu-id="b1d41-218">Save the file.</span></span>
1. <span data-ttu-id="b1d41-219">Add the main class for your application.</span><span class="sxs-lookup"><span data-stu-id="b1d41-219">Add the main class for your application.</span></span> <span data-ttu-id="b1d41-220">From the **Project Explorer**, right-click **src**, point to **New**, and then select **Scala class**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-220">From the **Project Explorer**, right-click **src**, point to **New**, and then select **Scala class**.</span></span>

    ![Select the main class](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/hdi-spark-scala-code.png)
1. <span data-ttu-id="b1d41-222">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-222">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span></span>

    ![Create new Scala class](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/hdi-spark-scala-code-object.png)
1. <span data-ttu-id="b1d41-224">In the `MyClusterAppMain.scala` file, paste the following code.</span><span class="sxs-lookup"><span data-stu-id="b1d41-224">In the `MyClusterAppMain.scala` file, paste the following code.</span></span> <span data-ttu-id="b1d41-225">This code creates the Spark context and opens an `executeJob` method from the `SparkSample` object.</span><span class="sxs-lookup"><span data-stu-id="b1d41-225">This code creates the Spark context and opens an `executeJob` method from the `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

1. <span data-ttu-id="b1d41-226">Repeat steps 8 and 9 to add a new Scala object called `*SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="b1d41-226">Repeat steps 8 and 9 to add a new Scala object called `*SparkSample`.</span></span> <span data-ttu-id="b1d41-227">Add the following code to this class.</span><span class="sxs-lookup"><span data-stu-id="b1d41-227">Add the following code to this class.</span></span> <span data-ttu-id="b1d41-228">This code reads the data from the HVAC.csv (available in all HDInsight Spark clusters).</span><span class="sxs-lookup"><span data-stu-id="b1d41-228">This code reads the data from the HVAC.csv (available in all HDInsight Spark clusters).</span></span> <span data-ttu-id="b1d41-229">It retrieves the rows that only have one digit in the seventh column in the CSV file, and then writes the output to **/HVACOut** under the default storage container for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b1d41-229">It retrieves the rows that only have one digit in the seventh column in the CSV file, and then writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

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
1. <span data-ttu-id="b1d41-230">Repeat steps 8 and 9 to add a new class called `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="b1d41-230">Repeat steps 8 and 9 to add a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="b1d41-231">This class implements the Spark test framework that is used to debug the applications.</span><span class="sxs-lookup"><span data-stu-id="b1d41-231">This class implements the Spark test framework that is used to debug the applications.</span></span> <span data-ttu-id="b1d41-232">Add the following code to the `RemoteClusterDebugging` class:</span><span class="sxs-lookup"><span data-stu-id="b1d41-232">Add the following code to the `RemoteClusterDebugging` class:</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="b1d41-233">There are a couple of important things to note:</span><span class="sxs-lookup"><span data-stu-id="b1d41-233">There are a couple of important things to note:</span></span>

      * <span data-ttu-id="b1d41-234">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span><span class="sxs-lookup"><span data-stu-id="b1d41-234">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span></span>
      * <span data-ttu-id="b1d41-235">For `setJars`, specify the location where the artifact JAR is created.</span><span class="sxs-lookup"><span data-stu-id="b1d41-235">For `setJars`, specify the location where the artifact JAR is created.</span></span> <span data-ttu-id="b1d41-236">Typically, it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="b1d41-236">Typically, it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
1. <span data-ttu-id="b1d41-237">In the`*RemoteClusterDebugging` class, right-click the `test` keyword, and then select **Create RemoteClusterDebugging Configuration**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-237">In the`*RemoteClusterDebugging` class, right-click the `test` keyword, and then select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Create a remote configuration](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/create-remote-config.png)

1. <span data-ttu-id="b1d41-239">In the **Create RemoteClusterDebugging Configuration** dialog box, provide a name for the configuration, and then select **Test kind** as the **Test name**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-239">In the **Create RemoteClusterDebugging Configuration** dialog box, provide a name for the configuration, and then select **Test kind** as the **Test name**.</span></span> <span data-ttu-id="b1d41-240">Leave all the other values as the default settings.</span><span class="sxs-lookup"><span data-stu-id="b1d41-240">Leave all the other values as the default settings.</span></span> <span data-ttu-id="b1d41-241">Select **Apply**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-241">Select **Apply**, and then select **OK**.</span></span>

    ![Add the configuration details](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/provide-config-value.png)
1. <span data-ttu-id="b1d41-243">You should now see a **Remote run** configuration drop-down list in the menu bar.</span><span class="sxs-lookup"><span data-stu-id="b1d41-243">You should now see a **Remote run** configuration drop-down list in the menu bar.</span></span>

    ![The Remote run drop-down list](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/config-run.png)

## <a name="step-5-run-the-application-in-debug-mode"></a><span data-ttu-id="b1d41-245">Step 5: Run the application in debug mode</span><span class="sxs-lookup"><span data-stu-id="b1d41-245">Step 5: Run the application in debug mode</span></span>
1. <span data-ttu-id="b1d41-246">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to `val rdd1`.</span><span class="sxs-lookup"><span data-stu-id="b1d41-246">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to `val rdd1`.</span></span> <span data-ttu-id="b1d41-247">In the **Create Breakpoint for** pop-up menu, select **line in function executeJob**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-247">In the **Create Breakpoint for** pop-up menu, select **line in function executeJob**.</span></span>

    ![Add a breakpoint](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/create-breakpoint.png)
1. <span data-ttu-id="b1d41-249">To run the application, select the **Debug Run** button next to the **Remote Run** configuration drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b1d41-249">To run the application, select the **Debug Run** button next to the **Remote Run** configuration drop-down list.</span></span>

    ![Select the Debug Run button](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-run-mode.png)
1. <span data-ttu-id="b1d41-251">When the program execution reaches the breakpoint, you see a **Debugger** tab in the bottom pane.</span><span class="sxs-lookup"><span data-stu-id="b1d41-251">When the program execution reaches the breakpoint, you see a **Debugger** tab in the bottom pane.</span></span>

    ![View the Debugger tab](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-add-watch.png)
1. <span data-ttu-id="b1d41-253">To add a watch, select the (**+**) icon.</span><span class="sxs-lookup"><span data-stu-id="b1d41-253">To add a watch, select the (**+**) icon.</span></span>

    ![Select the + icon](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-add-watch-variable.png)

    <span data-ttu-id="b1d41-255">In this example, the application broke before the variable `rdd1` was created.</span><span class="sxs-lookup"><span data-stu-id="b1d41-255">In this example, the application broke before the variable `rdd1` was created.</span></span> <span data-ttu-id="b1d41-256">By using this watch, we can see the first five rows in the variable `rdd`.</span><span class="sxs-lookup"><span data-stu-id="b1d41-256">By using this watch, we can see the first five rows in the variable `rdd`.</span></span> <span data-ttu-id="b1d41-257">Select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b1d41-257">Select **Enter**.</span></span>

    ![Run the program in debug mode](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-add-watch-variable-value.png)

    <span data-ttu-id="b1d41-259">What you see in the previous image is that at runtime, you might query terabytes of data and debug how your application progresses.</span><span class="sxs-lookup"><span data-stu-id="b1d41-259">What you see in the previous image is that at runtime, you might query terabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="b1d41-260">For example, in the output shown in the previous image, you can see that the first row of the output is a header.</span><span class="sxs-lookup"><span data-stu-id="b1d41-260">For example, in the output shown in the previous image, you can see that the first row of the output is a header.</span></span> <span data-ttu-id="b1d41-261">Based on this output, you can modify your application code to skip the header row, if necessary.</span><span class="sxs-lookup"><span data-stu-id="b1d41-261">Based on this output, you can modify your application code to skip the header row, if necessary.</span></span>
1. <span data-ttu-id="b1d41-262">You can now select the **Resume Program** icon to proceed with your application run.</span><span class="sxs-lookup"><span data-stu-id="b1d41-262">You can now select the **Resume Program** icon to proceed with your application run.</span></span>

    ![Select Resume Program](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-continue-run.png)
1. <span data-ttu-id="b1d41-264">If the application finishes successfully, you should see output like the following:</span><span class="sxs-lookup"><span data-stu-id="b1d41-264">If the application finishes successfully, you should see output like the following:</span></span>

    ![Console output](./media/apache-spark-intellij-tool-plugin-debug-jobs-remotely/debug-complete.png)

## <a name="seealso"></a><span data-ttu-id="b1d41-266">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1d41-266">Next steps</span></span>
* [<span data-ttu-id="b1d41-267">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1d41-267">Overview: Apache Spark on Azure HDInsight</span></span>](apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="b1d41-268">Demo</span><span class="sxs-lookup"><span data-stu-id="b1d41-268">Demo</span></span>
* <span data-ttu-id="b1d41-269">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="b1d41-269">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="b1d41-270">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="b1d41-270">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="b1d41-271">Scenarios</span><span class="sxs-lookup"><span data-stu-id="b1d41-271">Scenarios</span></span>
* [<span data-ttu-id="b1d41-272">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="b1d41-272">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b1d41-273">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="b1d41-273">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b1d41-274">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="b1d41-274">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b1d41-275">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1d41-275">Website log analysis using Spark in HDInsight</span></span>](../hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b1d41-276">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="b1d41-276">Create and run applications</span></span>
* [<span data-ttu-id="b1d41-277">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="b1d41-277">Create a standalone application using Scala</span></span>](../hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b1d41-278">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="b1d41-278">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b1d41-279">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="b1d41-279">Tools and extensions</span></span>
* [<span data-ttu-id="b1d41-280">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="b1d41-280">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b1d41-281">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span><span class="sxs-lookup"><span data-stu-id="b1d41-281">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="b1d41-282">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="b1d41-282">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](../hadoop/hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="b1d41-283">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span><span class="sxs-lookup"><span data-stu-id="b1d41-283">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](../hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="b1d41-284">Use Zeppelin notebooks with a Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1d41-284">Use Zeppelin notebooks with a Spark cluster in HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b1d41-285">Kernels available for Jupyter notebook in a Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1d41-285">Kernels available for Jupyter notebook in a Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b1d41-286">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="b1d41-286">Use external packages with Jupyter notebooks</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b1d41-287">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="b1d41-287">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b1d41-288">Manage resources</span><span class="sxs-lookup"><span data-stu-id="b1d41-288">Manage resources</span></span>
* [<span data-ttu-id="b1d41-289">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1d41-289">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="b1d41-290">Track and debug jobs that run on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1d41-290">Track and debug jobs that run on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)
