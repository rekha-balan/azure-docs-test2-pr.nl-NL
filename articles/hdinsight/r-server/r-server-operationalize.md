---
title: Operationalize ML Services on HDInsight - Azure
description: Learn how to operationalize ML Services in Azure HDInsight.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 06/27/2018
ms.openlocfilehash: 0a275405530c60c5e2f08a2af120382f81c2b6f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870651"
---
# <a name="operationalize-ml-services-cluster-on-azure-hdinsight"></a><span data-ttu-id="b5606-103">Operationalize ML Services cluster on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5606-103">Operationalize ML Services cluster on Azure HDInsight</span></span>

<span data-ttu-id="b5606-104">After you have used ML Services cluster in HDInsight to complete your data modeling, you can operationalize the model to make predictions.</span><span class="sxs-lookup"><span data-stu-id="b5606-104">After you have used ML Services cluster in HDInsight to complete your data modeling, you can operationalize the model to make predictions.</span></span> <span data-ttu-id="b5606-105">This article provides instructions on how to perform this task.</span><span class="sxs-lookup"><span data-stu-id="b5606-105">This article provides instructions on how to perform this task.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5606-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b5606-106">Prerequisites</span></span>

* <span data-ttu-id="b5606-107">**An ML Services cluster on HDInsight**: For instructions, see [Get started with ML Services on HDInsight](r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b5606-107">**An ML Services cluster on HDInsight**: For instructions, see [Get started with ML Services on HDInsight](r-server-get-started.md).</span></span>

* <span data-ttu-id="b5606-108">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span><span class="sxs-lookup"><span data-stu-id="b5606-108">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span></span> <span data-ttu-id="b5606-109">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b5606-109">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="operationalize-ml-services-cluster-with-one-box-configuration"></a><span data-ttu-id="b5606-110">Operationalize ML Services cluster with one-box configuration</span><span class="sxs-lookup"><span data-stu-id="b5606-110">Operationalize ML Services cluster with one-box configuration</span></span>

> [!NOTE]
> <span data-ttu-id="b5606-111">The steps below are applicable to R Server 9.0 and ML Server 9.1.</span><span class="sxs-lookup"><span data-stu-id="b5606-111">The steps below are applicable to R Server 9.0 and ML Server 9.1.</span></span> <span data-ttu-id="b5606-112">For ML Server 9.3, refer to [Use the administration tool to manage the operationalization configuration](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch).</span><span class="sxs-lookup"><span data-stu-id="b5606-112">For ML Server 9.3, refer to [Use the administration tool to manage the operationalization configuration](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch).</span></span>

1. <span data-ttu-id="b5606-113">SSH into the edge node.</span><span class="sxs-lookup"><span data-stu-id="b5606-113">SSH into the edge node.</span></span>

        ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

    <span data-ttu-id="b5606-114">For instructions on how to use SSH with Azure HDInsight, see [Use SSH with HDInsight.](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b5606-114">For instructions on how to use SSH with Azure HDInsight, see [Use SSH with HDInsight.](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="b5606-115">Change directory for the relevant version and sudo the dot net dll:</span><span class="sxs-lookup"><span data-stu-id="b5606-115">Change directory for the relevant version and sudo the dot net dll:</span></span> 

    - <span data-ttu-id="b5606-116">For Microsoft ML Server 9.1:</span><span class="sxs-lookup"><span data-stu-id="b5606-116">For Microsoft ML Server 9.1:</span></span>

            cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0
            sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

    - <span data-ttu-id="b5606-117">For Microsoft R Server 9.0:</span><span class="sxs-lookup"><span data-stu-id="b5606-117">For Microsoft R Server 9.0:</span></span>

            cd /usr/lib64/microsoft-deployr/9.0.1
            sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

1. <span data-ttu-id="b5606-118">You are presented with the options to choose from.</span><span class="sxs-lookup"><span data-stu-id="b5606-118">You are presented with the options to choose from.</span></span> <span data-ttu-id="b5606-119">Choose the first option, as shown in the following screenshot, to **Configure ML Server for Operationalization**.</span><span class="sxs-lookup"><span data-stu-id="b5606-119">Choose the first option, as shown in the following screenshot, to **Configure ML Server for Operationalization**.</span></span>

    ![one box op](./media/r-server-operationalize/admin-util-one-box-1.png)

1. <span data-ttu-id="b5606-121">You are now presented with the option to choose how you want to operationalize ML Server.</span><span class="sxs-lookup"><span data-stu-id="b5606-121">You are now presented with the option to choose how you want to operationalize ML Server.</span></span> <span data-ttu-id="b5606-122">From the presented options, choose the first one by entering **A**.</span><span class="sxs-lookup"><span data-stu-id="b5606-122">From the presented options, choose the first one by entering **A**.</span></span>

    ![one box op](./media/r-server-operationalize/admin-util-one-box-2.png)

1. <span data-ttu-id="b5606-124">When prompted, enter and reenter the password for a local admin user.</span><span class="sxs-lookup"><span data-stu-id="b5606-124">When prompted, enter and reenter the password for a local admin user.</span></span>

1. <span data-ttu-id="b5606-125">You should see outputs suggesting that the operation was successful.</span><span class="sxs-lookup"><span data-stu-id="b5606-125">You should see outputs suggesting that the operation was successful.</span></span> <span data-ttu-id="b5606-126">You are also prompted to select another option from the menu.</span><span class="sxs-lookup"><span data-stu-id="b5606-126">You are also prompted to select another option from the menu.</span></span> <span data-ttu-id="b5606-127">Select E to go back to the main menu.</span><span class="sxs-lookup"><span data-stu-id="b5606-127">Select E to go back to the main menu.</span></span>

    ![one box op](./media/r-server-operationalize/admin-util-one-box-3.png)

1. <span data-ttu-id="b5606-129">Optionally, you can perform diagnostic checks by running a diagnostic test as follows:</span><span class="sxs-lookup"><span data-stu-id="b5606-129">Optionally, you can perform diagnostic checks by running a diagnostic test as follows:</span></span>

    <span data-ttu-id="b5606-130">a.</span><span class="sxs-lookup"><span data-stu-id="b5606-130">a.</span></span> <span data-ttu-id="b5606-131">From the main menu, select **6** to run diagnostic tests.</span><span class="sxs-lookup"><span data-stu-id="b5606-131">From the main menu, select **6** to run diagnostic tests.</span></span>

    ![one box op](./media/r-server-operationalize/diagnostic-1.png)

    <span data-ttu-id="b5606-133">b.</span><span class="sxs-lookup"><span data-stu-id="b5606-133">b.</span></span> <span data-ttu-id="b5606-134">From the Diagnostic Tests menu, select **A**. When prompted, enter the password that you provided for the local admin user.</span><span class="sxs-lookup"><span data-stu-id="b5606-134">From the Diagnostic Tests menu, select **A**. When prompted, enter the password that you provided for the local admin user.</span></span>

    ![one box op](./media/r-server-operationalize/diagnostic-2.png)

    <span data-ttu-id="b5606-136">c.</span><span class="sxs-lookup"><span data-stu-id="b5606-136">c.</span></span> <span data-ttu-id="b5606-137">Verify that the output shows that overall health is a pass.</span><span class="sxs-lookup"><span data-stu-id="b5606-137">Verify that the output shows that overall health is a pass.</span></span>

    ![one box op](./media/r-server-operationalize/diagnostic-3.png)

    <span data-ttu-id="b5606-139">d.</span><span class="sxs-lookup"><span data-stu-id="b5606-139">d.</span></span> <span data-ttu-id="b5606-140">From the menu options presented, enter **E** to return to the main menu and then enter **8** to exit the admin utility.</span><span class="sxs-lookup"><span data-stu-id="b5606-140">From the menu options presented, enter **E** to return to the main menu and then enter **8** to exit the admin utility.</span></span>

### <a name="long-delays-when-consuming-web-service-on-spark"></a><span data-ttu-id="b5606-141">Long delays when consuming web service on Spark</span><span class="sxs-lookup"><span data-stu-id="b5606-141">Long delays when consuming web service on Spark</span></span>

<span data-ttu-id="b5606-142">If you encounter long delays when trying to consume a web service created with mrsdeploy functions in a Spark compute context, you may need to add some missing folders.</span><span class="sxs-lookup"><span data-stu-id="b5606-142">If you encounter long delays when trying to consume a web service created with mrsdeploy functions in a Spark compute context, you may need to add some missing folders.</span></span> <span data-ttu-id="b5606-143">The Spark application belongs to a user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span><span class="sxs-lookup"><span data-stu-id="b5606-143">The Spark application belongs to a user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="b5606-144">To work around this issue:</span><span class="sxs-lookup"><span data-stu-id="b5606-144">To work around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="b5606-145">At this stage, the configuration for operationalization is complete.</span><span class="sxs-lookup"><span data-stu-id="b5606-145">At this stage, the configuration for operationalization is complete.</span></span> <span data-ttu-id="b5606-146">Now you can use the `mrsdeploy` package on your RClient to connect to the operationalization on edge node and start using its features like [remote execution](https://docs.microsoft.com/machine-learning-server/r/how-to-execute-code-remotely) and [web-services](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services).</span><span class="sxs-lookup"><span data-stu-id="b5606-146">Now you can use the `mrsdeploy` package on your RClient to connect to the operationalization on edge node and start using its features like [remote execution](https://docs.microsoft.com/machine-learning-server/r/how-to-execute-code-remotely) and [web-services](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services).</span></span> <span data-ttu-id="b5606-147">Depending on whether your cluster is set up on a virtual network or not, you may need to set up port forward tunneling through SSH login.</span><span class="sxs-lookup"><span data-stu-id="b5606-147">Depending on whether your cluster is set up on a virtual network or not, you may need to set up port forward tunneling through SSH login.</span></span> <span data-ttu-id="b5606-148">The following sections explain how to set up this tunnel.</span><span class="sxs-lookup"><span data-stu-id="b5606-148">The following sections explain how to set up this tunnel.</span></span>

### <a name="ml-services-cluster-on-virtual-network"></a><span data-ttu-id="b5606-149">ML Services cluster on virtual network</span><span class="sxs-lookup"><span data-stu-id="b5606-149">ML Services cluster on virtual network</span></span>

<span data-ttu-id="b5606-150">Make sure you allow traffic through port 12800 to the edge node.</span><span class="sxs-lookup"><span data-stu-id="b5606-150">Make sure you allow traffic through port 12800 to the edge node.</span></span> <span data-ttu-id="b5606-151">That way, you can use the edge node to connect to the Operationalization feature.</span><span class="sxs-lookup"><span data-stu-id="b5606-151">That way, you can use the edge node to connect to the Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="b5606-152">If the `remoteLogin()` cannot connect to the edge node, but you can SSH to the edge node, then you need to verify whether the rule to allow traffic on port 12800 has been set properly or not.</span><span class="sxs-lookup"><span data-stu-id="b5606-152">If the `remoteLogin()` cannot connect to the edge node, but you can SSH to the edge node, then you need to verify whether the rule to allow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="b5606-153">If you continue to face the issue, you can work around it by setting up port forward tunneling through SSH.</span><span class="sxs-lookup"><span data-stu-id="b5606-153">If you continue to face the issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="b5606-154">For instructions, see the following section:</span><span class="sxs-lookup"><span data-stu-id="b5606-154">For instructions, see the following section:</span></span>

### <a name="ml-services-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="b5606-155">ML Services cluster not set up on virtual network</span><span class="sxs-lookup"><span data-stu-id="b5606-155">ML Services cluster not set up on virtual network</span></span>

<span data-ttu-id="b5606-156">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span><span class="sxs-lookup"><span data-stu-id="b5606-156">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="b5606-157">Once your SSH session is active, the traffic from your local machine's port 12800 is forwarded to the edge node's port 12800 through SSH session.</span><span class="sxs-lookup"><span data-stu-id="b5606-157">Once your SSH session is active, the traffic from your local machine's port 12800 is forwarded to the edge node's port 12800 through SSH session.</span></span> <span data-ttu-id="b5606-158">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span><span class="sxs-lookup"><span data-stu-id="b5606-158">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="b5606-159">This logs into the edge node's operationalization through port forwarding.</span><span class="sxs-lookup"><span data-stu-id="b5606-159">This logs into the edge node's operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="scale-operationalized-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="b5606-160">Scale operationalized compute nodes on HDInsight worker nodes</span><span class="sxs-lookup"><span data-stu-id="b5606-160">Scale operationalized compute nodes on HDInsight worker nodes</span></span>

<span data-ttu-id="b5606-161">To scale the compute nodes, you first decommission the worker nodes and then configure compute nodes on the decommissioned worker nodes.</span><span class="sxs-lookup"><span data-stu-id="b5606-161">To scale the compute nodes, you first decommission the worker nodes and then configure compute nodes on the decommissioned worker nodes.</span></span>

### <a name="step-1-decommission-the-worker-nodes"></a><span data-ttu-id="b5606-162">Step 1: Decommission the worker nodes</span><span class="sxs-lookup"><span data-stu-id="b5606-162">Step 1: Decommission the worker nodes</span></span>

<span data-ttu-id="b5606-163">ML Services cluster is not managed through YARN.</span><span class="sxs-lookup"><span data-stu-id="b5606-163">ML Services cluster is not managed through YARN.</span></span> <span data-ttu-id="b5606-164">If the worker nodes are not decommissioned, the YARN Resource Manager does not work as expected because it is not aware of the resources being taken up by the server.</span><span class="sxs-lookup"><span data-stu-id="b5606-164">If the worker nodes are not decommissioned, the YARN Resource Manager does not work as expected because it is not aware of the resources being taken up by the server.</span></span> <span data-ttu-id="b5606-165">In order to avoid this situation, we recommend decommissioning the worker nodes before you scale out the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="b5606-165">In order to avoid this situation, we recommend decommissioning the worker nodes before you scale out the compute nodes.</span></span>

<span data-ttu-id="b5606-166">Follow these steps to decommission worker nodes:</span><span class="sxs-lookup"><span data-stu-id="b5606-166">Follow these steps to decommission worker nodes:</span></span>

1. <span data-ttu-id="b5606-167">Log in to the cluster's Ambari console and click on **Hosts** tab.</span><span class="sxs-lookup"><span data-stu-id="b5606-167">Log in to the cluster's Ambari console and click on **Hosts** tab.</span></span>

1. <span data-ttu-id="b5606-168">Select worker nodes (to be decommissioned).</span><span class="sxs-lookup"><span data-stu-id="b5606-168">Select worker nodes (to be decommissioned).</span></span>

1. <span data-ttu-id="b5606-169">Click  **Actions** > **Selected Hosts** > **Hosts** > **Turn ON Maintenance Mode**.</span><span class="sxs-lookup"><span data-stu-id="b5606-169">Click  **Actions** > **Selected Hosts** > **Hosts** > **Turn ON Maintenance Mode**.</span></span> <span data-ttu-id="b5606-170">For example, in the following image we have selected wn3 and wn4 to decommission.</span><span class="sxs-lookup"><span data-stu-id="b5606-170">For example, in the following image we have selected wn3 and wn4 to decommission.</span></span>  

   ![decommission worker nodes](./media/r-server-operationalize/get-started-operationalization.png)  

* <span data-ttu-id="b5606-172">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**.</span><span class="sxs-lookup"><span data-stu-id="b5606-172">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**.</span></span>
* <span data-ttu-id="b5606-173">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**.</span><span class="sxs-lookup"><span data-stu-id="b5606-173">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**.</span></span>
* <span data-ttu-id="b5606-174">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**.</span><span class="sxs-lookup"><span data-stu-id="b5606-174">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**.</span></span>
* <span data-ttu-id="b5606-175">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**.</span><span class="sxs-lookup"><span data-stu-id="b5606-175">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**.</span></span>
* <span data-ttu-id="b5606-176">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**.</span><span class="sxs-lookup"><span data-stu-id="b5606-176">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**.</span></span>
* <span data-ttu-id="b5606-177">Unselect the worker nodes and select the head nodes.</span><span class="sxs-lookup"><span data-stu-id="b5606-177">Unselect the worker nodes and select the head nodes.</span></span>
* <span data-ttu-id="b5606-178">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**.</span><span class="sxs-lookup"><span data-stu-id="b5606-178">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**.</span></span>

### <a name="step-2-configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="b5606-179">Step 2: Configure compute nodes on each decommissioned worker node(s)</span><span class="sxs-lookup"><span data-stu-id="b5606-179">Step 2: Configure compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="b5606-180">SSH into each decommissioned worker node.</span><span class="sxs-lookup"><span data-stu-id="b5606-180">SSH into each decommissioned worker node.</span></span>

1. <span data-ttu-id="b5606-181">Run admin utility using the relevant DLL for the ML Services cluster that you have.</span><span class="sxs-lookup"><span data-stu-id="b5606-181">Run admin utility using the relevant DLL for the ML Services cluster that you have.</span></span> <span data-ttu-id="b5606-182">For ML Server 9.1, run the following:</span><span class="sxs-lookup"><span data-stu-id="b5606-182">For ML Server 9.1, run the following:</span></span>

        dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

1. <span data-ttu-id="b5606-183">Enter **1** to select option **Configure ML Server for Operationalization**.</span><span class="sxs-lookup"><span data-stu-id="b5606-183">Enter **1** to select option **Configure ML Server for Operationalization**.</span></span>

1. <span data-ttu-id="b5606-184">Enter **C** to select option `C. Compute node`.</span><span class="sxs-lookup"><span data-stu-id="b5606-184">Enter **C** to select option `C. Compute node`.</span></span> <span data-ttu-id="b5606-185">This configures the compute node on the worker node.</span><span class="sxs-lookup"><span data-stu-id="b5606-185">This configures the compute node on the worker node.</span></span>

1. <span data-ttu-id="b5606-186">Exit the Admin Utility.</span><span class="sxs-lookup"><span data-stu-id="b5606-186">Exit the Admin Utility.</span></span>

### <a name="step-3-add-compute-nodes-details-on-web-node"></a><span data-ttu-id="b5606-187">Step 3: Add compute nodes details on web node</span><span class="sxs-lookup"><span data-stu-id="b5606-187">Step 3: Add compute nodes details on web node</span></span>

<span data-ttu-id="b5606-188">Once all decommissioned worker nodes are configured to run compute node, come back on the edge node and add decommissioned worker nodes' IP addresses in the ML Server web node's configuration:</span><span class="sxs-lookup"><span data-stu-id="b5606-188">Once all decommissioned worker nodes are configured to run compute node, come back on the edge node and add decommissioned worker nodes' IP addresses in the ML Server web node's configuration:</span></span>

1. <span data-ttu-id="b5606-189">SSH into the edge node.</span><span class="sxs-lookup"><span data-stu-id="b5606-189">SSH into the edge node.</span></span>

1. <span data-ttu-id="b5606-190">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="b5606-190">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>

1. <span data-ttu-id="b5606-191">Look for the "Uris" section, and add worker node's IP and port details.</span><span class="sxs-lookup"><span data-stu-id="b5606-191">Look for the "Uris" section, and add worker node's IP and port details.</span></span>

       "Uris": {
         "Description": "Update 'Values' section to point to your backend machines. Using HTTPS is highly recommended",
         "Values": [
           "http://localhost:12805", "http://[worker-node1-ip]:12805", "http://[workder-node2-ip]:12805"
         ]
       }

## <a name="next-steps"></a><span data-ttu-id="b5606-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5606-192">Next steps</span></span>

* [<span data-ttu-id="b5606-193">Manage ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5606-193">Manage ML Services cluster on HDInsight</span></span>](r-server-hdinsight-manage.md)
* [<span data-ttu-id="b5606-194">Compute context options for ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5606-194">Compute context options for ML Services cluster on HDInsight</span></span>](r-server-compute-contexts.md)
* [<span data-ttu-id="b5606-195">Azure Storage options for ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5606-195">Azure Storage options for ML Services cluster on HDInsight</span></span>](r-server-storage.md)
