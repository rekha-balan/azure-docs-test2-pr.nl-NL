---
title: Azure HDInsight Tools - Use Visual Studio Code for Hive, LLAP or PySpark | Microsoft Docs
description: Learn how to use the Azure HDInsight Tools for Visual Studio Code to create and submit queries and scripts.
Keywords: VS Code,Azure HDInsight Tools,Hive,Python,PySpark,Spark,HDInsight,Hadoop,LLAP,Interactive Hive,Interactive Query
services: HDInsight
documentationcenter: ''
author: jejiang
ms.author: jejiang
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 10/27/2017
ms.openlocfilehash: 5cf3a18dc01ba5670e73aa93cb6c9aab2d5de660
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857481"
---
# <a name="use-azure-hdinsight-tools-for-visual-studio-code"></a><span data-ttu-id="bdd4b-103">Use Azure HDInsight Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bdd4b-103">Use Azure HDInsight Tools for Visual Studio Code</span></span>

<span data-ttu-id="bdd4b-104">Learn how to use the Azure HDInsight Tools for Visual Studio Code (VS Code) to create and submit Hive batch jobs, interactive Hive queries, and PySpark scripts.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-104">Learn how to use the Azure HDInsight Tools for Visual Studio Code (VS Code) to create and submit Hive batch jobs, interactive Hive queries, and PySpark scripts.</span></span> <span data-ttu-id="bdd4b-105">The Azure HDInsight Tools can be installed on the platforms that are supported by VS Code.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-105">The Azure HDInsight Tools can be installed on the platforms that are supported by VS Code.</span></span> <span data-ttu-id="bdd4b-106">These include Windows, Linux, and macOS.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-106">These include Windows, Linux, and macOS.</span></span> <span data-ttu-id="bdd4b-107">You can find the prerequisites for different platforms.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-107">You can find the prerequisites for different platforms.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bdd4b-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bdd4b-108">Prerequisites</span></span>

<span data-ttu-id="bdd4b-109">The following items are required for completing the steps in this article:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-109">The following items are required for completing the steps in this article:</span></span>

- <span data-ttu-id="bdd4b-110">A HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-110">A HDInsight cluster.</span></span> <span data-ttu-id="bdd4b-111">To create a cluster, see [Get started with HDInsight](hadoop/apache-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-111">To create a cluster, see [Get started with HDInsight](hadoop/apache-hadoop-linux-tutorial-get-started.md).</span></span>
- <span data-ttu-id="bdd4b-112">[Visual Studio Code](https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-112">[Visual Studio Code](https://www.visualstudio.com/products/code-vs.aspx).</span></span>
- <span data-ttu-id="bdd4b-113">[Mono](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-113">[Mono](http://www.mono-project.com/docs/getting-started/install/).</span></span> <span data-ttu-id="bdd4b-114">Mono is only required for Linux and macOS.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-114">Mono is only required for Linux and macOS.</span></span>

## <a name="install-the-hdinsight-tools"></a><span data-ttu-id="bdd4b-115">Install the HDInsight Tools</span><span class="sxs-lookup"><span data-stu-id="bdd4b-115">Install the HDInsight Tools</span></span>
   
<span data-ttu-id="bdd4b-116">After you have installed the prerequisites, you can install the Azure HDInsight Tools for VS Code.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-116">After you have installed the prerequisites, you can install the Azure HDInsight Tools for VS Code.</span></span> 

### <a name="to-install-azure-hdinsight-tools"></a><span data-ttu-id="bdd4b-117">To install Azure HDInsight Tools</span><span class="sxs-lookup"><span data-stu-id="bdd4b-117">To install Azure HDInsight Tools</span></span>

1. <span data-ttu-id="bdd4b-118">Open Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-118">Open Visual Studio Code.</span></span>

2. <span data-ttu-id="bdd4b-119">In the left pane, select **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-119">In the left pane, select **Extensions**.</span></span> <span data-ttu-id="bdd4b-120">In the search box, enter **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-120">In the search box, enter **HDInsight**.</span></span>

3. <span data-ttu-id="bdd4b-121">Next to **Azure HDInsight Tools**, select **Install**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-121">Next to **Azure HDInsight Tools**, select **Install**.</span></span> <span data-ttu-id="bdd4b-122">After a few seconds, the **Install** button changes to **Reload**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-122">After a few seconds, the **Install** button changes to **Reload**.</span></span>

4. <span data-ttu-id="bdd4b-123">Select **Reload** to activate the **Azure HDInsight Tools** extension.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-123">Select **Reload** to activate the **Azure HDInsight Tools** extension.</span></span>

5. <span data-ttu-id="bdd4b-124">Select **Reload Window** to confirm.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-124">Select **Reload Window** to confirm.</span></span> <span data-ttu-id="bdd4b-125">You can see **Azure HDInsight Tools** in the **Extensions** pane.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-125">You can see **Azure HDInsight Tools** in the **Extensions** pane.</span></span>

   ![HDInsight for Visual Studio Code Python install](./media/hdinsight-for-vscode/install-hdInsight-plugin.png)

## <a name="open-hdinsight-workspace"></a><span data-ttu-id="bdd4b-127">Open HDInsight workspace</span><span class="sxs-lookup"><span data-stu-id="bdd4b-127">Open HDInsight workspace</span></span>

<span data-ttu-id="bdd4b-128">Create a workspace in VS Code before you can connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-128">Create a workspace in VS Code before you can connect to Azure.</span></span>

### <a name="to-open-a-workspace"></a><span data-ttu-id="bdd4b-129">To open a workspace</span><span class="sxs-lookup"><span data-stu-id="bdd4b-129">To open a workspace</span></span>

1. <span data-ttu-id="bdd4b-130">On the **File** menu, select **Open Folder**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-130">On the **File** menu, select **Open Folder**.</span></span> <span data-ttu-id="bdd4b-131">Then designate an existing folder as your work folder or create a new one.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-131">Then designate an existing folder as your work folder or create a new one.</span></span> <span data-ttu-id="bdd4b-132">The folder appears in the left pane.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-132">The folder appears in the left pane.</span></span>

2. <span data-ttu-id="bdd4b-133">On the left pane, select the **New File** icon next to the work folder.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-133">On the left pane, select the **New File** icon next to the work folder.</span></span>

   ![New file](./media/hdinsight-for-vscode/new-file.png)

3. <span data-ttu-id="bdd4b-135">Name the new file with either the .hql (Hive queries) or the .py (Spark script) file extension.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-135">Name the new file with either the .hql (Hive queries) or the .py (Spark script) file extension.</span></span> 

## <a name="connect-to-hdinsight-cluster"></a><span data-ttu-id="bdd4b-136">Connect to HDInsight Cluster</span><span class="sxs-lookup"><span data-stu-id="bdd4b-136">Connect to HDInsight Cluster</span></span>

<span data-ttu-id="bdd4b-137">Before you can submit scripts to HDInsight clusters from VS Code, you need to either connect to your Azure account, or link a cluster (using Ambari username/password or domain joined account).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-137">Before you can submit scripts to HDInsight clusters from VS Code, you need to either connect to your Azure account, or link a cluster (using Ambari username/password or domain joined account).</span></span>

### <a name="to-connect-to-azure"></a><span data-ttu-id="bdd4b-138">To connect to Azure</span><span class="sxs-lookup"><span data-stu-id="bdd4b-138">To connect to Azure</span></span>

1. <span data-ttu-id="bdd4b-139">Create a new work folder and a new script file if you don't already have them.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-139">Create a new work folder and a new script file if you don't already have them.</span></span>

2. <span data-ttu-id="bdd4b-140">Right-click the script editor, and then, on the context menu, select **HDInsight: Login**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-140">Right-click the script editor, and then, on the context menu, select **HDInsight: Login**.</span></span> <span data-ttu-id="bdd4b-141">You can also enter **Ctrl+Shift+P**, and then enter **HDInsight: Login**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-141">You can also enter **Ctrl+Shift+P**, and then enter **HDInsight: Login**.</span></span>

    ![HDInsight Tools for Visual Studio Code login](./media/hdinsight-for-vscode/hdinsight-for-vscode-extension-login.png)

3. <span data-ttu-id="bdd4b-143">To sign in, follow the sign-in instructions in the **OUTPUT** pane.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-143">To sign in, follow the sign-in instructions in the **OUTPUT** pane.</span></span>
    + <span data-ttu-id="bdd4b-144">For global environment, HDInsight sign in will trigger Azure sign in process.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-144">For global environment, HDInsight sign in will trigger Azure sign in process.</span></span>

        ![Sign in instructions for azure](./media/hdinsight-for-vscode/hdi-azure-hdinsight-azure-signin.png)

    + <span data-ttu-id="bdd4b-146">For Other environments, follow the sign-in instructions.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-146">For Other environments, follow the sign-in instructions.</span></span>

        ![Sign in instructions for other environment](./media/hdinsight-for-vscode/hdi-azure-hdinsight-hdinsight-signin.png)

    <span data-ttu-id="bdd4b-148">After you're connected, your Azure account name is shown on the status bar at the bottom left of the VS Code window.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-148">After you're connected, your Azure account name is shown on the status bar at the bottom left of the VS Code window.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="bdd4b-149">Because of a known Azure authentication issue, you need to open a browser in private mode or incognito mode.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-149">Because of a known Azure authentication issue, you need to open a browser in private mode or incognito mode.</span></span> <span data-ttu-id="bdd4b-150">If your Azure account has two factors enabled, we recommended using phone authentication instead of PIN authentication.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-150">If your Azure account has two factors enabled, we recommended using phone authentication instead of PIN authentication.</span></span>
  

4. <span data-ttu-id="bdd4b-151">Right-click the script editor to open the context menu.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-151">Right-click the script editor to open the context menu.</span></span> <span data-ttu-id="bdd4b-152">From the context menu, you can perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-152">From the context menu, you can perform the following tasks:</span></span>

    - <span data-ttu-id="bdd4b-153">Log out</span><span class="sxs-lookup"><span data-stu-id="bdd4b-153">Log out</span></span>
    - <span data-ttu-id="bdd4b-154">List clusters</span><span class="sxs-lookup"><span data-stu-id="bdd4b-154">List clusters</span></span>
    - <span data-ttu-id="bdd4b-155">Set default clusters</span><span class="sxs-lookup"><span data-stu-id="bdd4b-155">Set default clusters</span></span>
    - <span data-ttu-id="bdd4b-156">Submit interactive Hive queries</span><span class="sxs-lookup"><span data-stu-id="bdd4b-156">Submit interactive Hive queries</span></span>
    - <span data-ttu-id="bdd4b-157">Submit Hive batch scripts</span><span class="sxs-lookup"><span data-stu-id="bdd4b-157">Submit Hive batch scripts</span></span>
    - <span data-ttu-id="bdd4b-158">Submit interactive PySpark queries</span><span class="sxs-lookup"><span data-stu-id="bdd4b-158">Submit interactive PySpark queries</span></span>
    - <span data-ttu-id="bdd4b-159">Submit PySpark batch scripts</span><span class="sxs-lookup"><span data-stu-id="bdd4b-159">Submit PySpark batch scripts</span></span>
    - <span data-ttu-id="bdd4b-160">Set configuration</span><span class="sxs-lookup"><span data-stu-id="bdd4b-160">Set configuration</span></span>

<h3 id="linkcluster"><span data-ttu-id="bdd4b-161">To link a cluster</span><span class="sxs-lookup"><span data-stu-id="bdd4b-161">To link a cluster</span></span></h3>

<span data-ttu-id="bdd4b-162">You can link a normal cluster by using Ambari managed username, also link a security hadoop cluster by using domain username (such as: user1@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-162">You can link a normal cluster by using Ambari managed username, also link a security hadoop cluster by using domain username (such as: user1@contoso.com).</span></span>
1. <span data-ttu-id="bdd4b-163">Open the command palette by selecting **CTRL+SHIFT+P**, and then enter **HDInsight: Link a Cluster**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-163">Open the command palette by selecting **CTRL+SHIFT+P**, and then enter **HDInsight: Link a Cluster**.</span></span>

   ![link cluster command](./media/hdinsight-for-vscode/link-cluster-command.png)

2. <span data-ttu-id="bdd4b-165">Enter HDInsight cluster URL -> input Username -> input Password -> select cluster type -> it shows success info if verification passed.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-165">Enter HDInsight cluster URL -> input Username -> input Password -> select cluster type -> it shows success info if verification passed.</span></span>
   
   ![link cluster dialog](./media/hdinsight-for-vscode/link-cluster-process.png)

   > [!NOTE]
   > <span data-ttu-id="bdd4b-167">The linked username and password are used if the cluster both logged in Azure subscription and Linked a cluster.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-167">The linked username and password are used if the cluster both logged in Azure subscription and Linked a cluster.</span></span> 
   
3. <span data-ttu-id="bdd4b-168">You can see a Linked cluster by using command **List Cluster**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-168">You can see a Linked cluster by using command **List Cluster**.</span></span> <span data-ttu-id="bdd4b-169">Now you can submit a script to this linked cluster.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-169">Now you can submit a script to this linked cluster.</span></span>

   ![linked cluster](./media/hdinsight-for-vscode/linked-cluster.png)

4. <span data-ttu-id="bdd4b-171">You also can unlink a cluster by inputting **HDInsight: Unlink a Cluster** from command palette.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-171">You also can unlink a cluster by inputting **HDInsight: Unlink a Cluster** from command palette.</span></span>


### <a name="to-link-a-generic-livy-endpoint"></a><span data-ttu-id="bdd4b-172">To link a generic livy endpoint</span><span class="sxs-lookup"><span data-stu-id="bdd4b-172">To link a generic livy endpoint</span></span>

1. <span data-ttu-id="bdd4b-173">Open the command palette by selecting **CTRL+SHIFT+P**, and then enter **HDInsight: Link a Cluster**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-173">Open the command palette by selecting **CTRL+SHIFT+P**, and then enter **HDInsight: Link a Cluster**.</span></span>
2. <span data-ttu-id="bdd4b-174">Select **Generic Livy Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-174">Select **Generic Livy Endpoint**.</span></span>
3. <span data-ttu-id="bdd4b-175">Enter the generic livy endpoint, for example: http://10.172.41.42:18080.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-175">Enter the generic livy endpoint, for example: http://10.172.41.42:18080.</span></span>
4. <span data-ttu-id="bdd4b-176">Select **Basic** when need authorization for the generic livy endpoint, otherwise, select **None**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-176">Select **Basic** when need authorization for the generic livy endpoint, otherwise, select **None**.</span></span>
5. <span data-ttu-id="bdd4b-177">Input user name when select **Basic** in step4.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-177">Input user name when select **Basic** in step4.</span></span>
6. <span data-ttu-id="bdd4b-178">Input password when select **Basic** in step4.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-178">Input password when select **Basic** in step4.</span></span>
7. <span data-ttu-id="bdd4b-179">The generic livy endpoint linked successfully.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-179">The generic livy endpoint linked successfully.</span></span>

   ![linked generic livy cluster](./media/hdinsight-for-vscode/link-cluster-process-generic-livy.png)

## <a name="list-hdinsight-clusters"></a><span data-ttu-id="bdd4b-181">List HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="bdd4b-181">List HDInsight clusters</span></span>

<span data-ttu-id="bdd4b-182">To test the connection, you can list your HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-182">To test the connection, you can list your HDInsight clusters:</span></span>

### <a name="to-list-hdinsight-clusters-under-your-azure-subscription"></a><span data-ttu-id="bdd4b-183">To list HDInsight clusters under your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="bdd4b-183">To list HDInsight clusters under your Azure subscription</span></span>
1. <span data-ttu-id="bdd4b-184">Open a workspace, and then connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-184">Open a workspace, and then connect to Azure.</span></span> <span data-ttu-id="bdd4b-185">For more information, see [Open HDInsight workspace](#open-hdinsight-workspace) and [Connect to Azure](#connect-to-hdinsight-cluster).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-185">For more information, see [Open HDInsight workspace](#open-hdinsight-workspace) and [Connect to Azure](#connect-to-hdinsight-cluster).</span></span>

2. <span data-ttu-id="bdd4b-186">Right-click the script editor, and then select **HDInsight: List Cluster** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-186">Right-click the script editor, and then select **HDInsight: List Cluster** from the context menu.</span></span> 

3. <span data-ttu-id="bdd4b-187">The Hive and Spark clusters appear in the **Output** pane.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-187">The Hive and Spark clusters appear in the **Output** pane.</span></span>

    ![Set a default cluster configuration](./media/hdinsight-for-vscode/list-cluster-result.png)

## <a name="set-a-default-cluster"></a><span data-ttu-id="bdd4b-189">Set a default cluster</span><span class="sxs-lookup"><span data-stu-id="bdd4b-189">Set a default cluster</span></span>
1. <span data-ttu-id="bdd4b-190">Open a workspace and connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-190">Open a workspace and connect to Azure.</span></span> <span data-ttu-id="bdd4b-191">See [Open HDInsight workspace](#open-hdinsight-workspace) and [Connect to Azure](#connect-to-hdinsight-cluster).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-191">See [Open HDInsight workspace](#open-hdinsight-workspace) and [Connect to Azure](#connect-to-hdinsight-cluster).</span></span>

2. <span data-ttu-id="bdd4b-192">Right-click the script editor, and then select **HDInsight: Set Default Cluster**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-192">Right-click the script editor, and then select **HDInsight: Set Default Cluster**.</span></span> 

3. <span data-ttu-id="bdd4b-193">Select a cluster as the default cluster for the current script file.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-193">Select a cluster as the default cluster for the current script file.</span></span> <span data-ttu-id="bdd4b-194">The tools automatically update the configuration file **.VSCode\settings.json**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-194">The tools automatically update the configuration file **.VSCode\settings.json**.</span></span> 

   ![Set default cluster configuration](./media/hdinsight-for-vscode/set-default-cluster-configuration.png)

## <a name="set-the-azure-environment"></a><span data-ttu-id="bdd4b-196">Set the Azure environment</span><span class="sxs-lookup"><span data-stu-id="bdd4b-196">Set the Azure environment</span></span>
1. <span data-ttu-id="bdd4b-197">Open the command palette by selecting **CTRL+SHIFT+P**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-197">Open the command palette by selecting **CTRL+SHIFT+P**.</span></span>

2. <span data-ttu-id="bdd4b-198">Enter **HDInsight: Set Azure Environment**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-198">Enter **HDInsight: Set Azure Environment**.</span></span>

3. <span data-ttu-id="bdd4b-199">Select one way from Azure and AzureChina as your default login entry.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-199">Select one way from Azure and AzureChina as your default login entry.</span></span>

4. <span data-ttu-id="bdd4b-200">Meanwhile, the tool has already saved your default login entry in **.VSCode\settings.json**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-200">Meanwhile, the tool has already saved your default login entry in **.VSCode\settings.json**.</span></span> <span data-ttu-id="bdd4b-201">You also directly update it in this configuration file.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-201">You also directly update it in this configuration file.</span></span> 

   ![Set default login entry configuration](./media/hdinsight-for-vscode/set-default-login-entry-configuration.png)

## <a name="submit-interactive-hive-queries-hive-batch-scripts"></a><span data-ttu-id="bdd4b-203">Submit interactive Hive queries, Hive batch scripts</span><span class="sxs-lookup"><span data-stu-id="bdd4b-203">Submit interactive Hive queries, Hive batch scripts</span></span>

<span data-ttu-id="bdd4b-204">With HDInsight Tools for VS Code, you can submit interactive Hive queries, Hive batch scripts to HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-204">With HDInsight Tools for VS Code, you can submit interactive Hive queries, Hive batch scripts to HDInsight clusters.</span></span>

1. <span data-ttu-id="bdd4b-205">Create a new work folder and a new Hive script file if you don't already have them.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-205">Create a new work folder and a new Hive script file if you don't already have them.</span></span>

2. <span data-ttu-id="bdd4b-206">Connect to your Azure account or link clusters.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-206">Connect to your Azure account or link clusters.</span></span>

3. <span data-ttu-id="bdd4b-207">Copy and paste the following code into your Hive file, and then save it.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-207">Copy and paste the following code into your Hive file, and then save it.</span></span>

    ```hiveql
    SELECT * FROM hivesampletable;
    ```
4. <span data-ttu-id="bdd4b-208">Right-click the script editor, select **HDInsight: Hive Interactive** to submit the query, or use shortcut **Ctrl + Alt + I**. Select **HDInsight: Hive Batch** to submit the script, or use shortcut **Ctrl + Alt + H**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-208">Right-click the script editor, select **HDInsight: Hive Interactive** to submit the query, or use shortcut **Ctrl + Alt + I**. Select **HDInsight: Hive Batch** to submit the script, or use shortcut **Ctrl + Alt + H**.</span></span> 

5. <span data-ttu-id="bdd4b-209">Select the cluster when need.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-209">Select the cluster when need.</span></span> <span data-ttu-id="bdd4b-210">The tools also allow you to submit a block of code instead of the whole script file using the context menu.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-210">The tools also allow you to submit a block of code instead of the whole script file using the context menu.</span></span> <span data-ttu-id="bdd4b-211">Soon after, the query results appear in a new tab.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-211">Soon after, the query results appear in a new tab.</span></span>

   ![Interactive Hive result](./media/hdinsight-for-vscode/interactive-hive-result.png)

    - <span data-ttu-id="bdd4b-213">**RESULTS** panel: You can save the whole result as CSV, JSON, or Excel file to local path, or just select multiple lines.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-213">**RESULTS** panel: You can save the whole result as CSV, JSON, or Excel file to local path, or just select multiple lines.</span></span>

    - <span data-ttu-id="bdd4b-214">**MESSAGES** panel: When you select **Line** number, it jumps to the first line of the running script.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-214">**MESSAGES** panel: When you select **Line** number, it jumps to the first line of the running script.</span></span>

## <a name="submit-interactive-pyspark-queries"></a><span data-ttu-id="bdd4b-215">Submit interactive PySpark queries</span><span class="sxs-lookup"><span data-stu-id="bdd4b-215">Submit interactive PySpark queries</span></span>

### <a name="to-submit-interactive-pyspark-queries-to-spark-clusters"></a><span data-ttu-id="bdd4b-216">To submit interactive PySpark queries to Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-216">To submit interactive PySpark queries to Spark clusters.</span></span>

1. <span data-ttu-id="bdd4b-217">Create a new work folder and a new script file with the .py extension if you don't already have them.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-217">Create a new work folder and a new script file with the .py extension if you don't already have them.</span></span>

2. <span data-ttu-id="bdd4b-218">Connect to your Azure account if you haven't yet done so.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-218">Connect to your Azure account if you haven't yet done so.</span></span>

3. <span data-ttu-id="bdd4b-219">Copy and paste the following code into the script file:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-219">Copy and paste the following code into the script file:</span></span>
   ```python
   from operator import add
   lines = spark.read.text("/HdiSamples/HdiSamples/FoodInspectionData/README").rdd.map(lambda r: r[0])
   counters = lines.flatMap(lambda x: x.split(' ')) \
                .map(lambda x: (x, 1)) \
                .reduceByKey(add)

   coll = counters.collect()
   sortedCollection = sorted(coll, key = lambda r: r[1], reverse = True)

   for i in range(0, 5):
        print(sortedCollection[i])
   ```
4. <span data-ttu-id="bdd4b-220">Highlight these scripts.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-220">Highlight these scripts.</span></span> <span data-ttu-id="bdd4b-221">Then right-click the script editor and select **HDInsight: PySpark Interactive**, or use shortcut **Ctrl + Alt + I**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-221">Then right-click the script editor and select **HDInsight: PySpark Interactive**, or use shortcut **Ctrl + Alt + I**.</span></span>

5. <span data-ttu-id="bdd4b-222">If you haven't already installed the **Python** extension in VS Code, select the **Install** button as shown in the following illustration:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-222">If you haven't already installed the **Python** extension in VS Code, select the **Install** button as shown in the following illustration:</span></span>

    ![HDInsight for Visual Studio Code Python install](./media/hdinsight-for-vscode/hdinsight-vscode-install-python.png)

6. <span data-ttu-id="bdd4b-224">Install the Python environment in your system if you haven't already.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-224">Install the Python environment in your system if you haven't already.</span></span> 
   - <span data-ttu-id="bdd4b-225">For Windows, download and install [Python](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-225">For Windows, download and install [Python](https://www.python.org/downloads/).</span></span> <span data-ttu-id="bdd4b-226">Then make sure `Python` and `pip` are in your system PATH.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-226">Then make sure `Python` and `pip` are in your system PATH.</span></span>

   - <span data-ttu-id="bdd4b-227">For instructions for macOS and Linux, see [Set up PySpark interactive environment for Visual Studio Code](set-up-pyspark-interactive-environment.md).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-227">For instructions for macOS and Linux, see [Set up PySpark interactive environment for Visual Studio Code](set-up-pyspark-interactive-environment.md).</span></span>

7. <span data-ttu-id="bdd4b-228">Select a cluster to which to submit your PySpark query.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-228">Select a cluster to which to submit your PySpark query.</span></span> <span data-ttu-id="bdd4b-229">Soon after, the query result is shown in the new right tab:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-229">Soon after, the query result is shown in the new right tab:</span></span>

   ![Submit Python job result](./media/hdinsight-for-vscode/pyspark-interactive-result.png) 
8. <span data-ttu-id="bdd4b-231">The tool also supports the **SQL Clause** query.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-231">The tool also supports the **SQL Clause** query.</span></span>

   <span data-ttu-id="bdd4b-232">![Submit Python job result](./media/hdinsight-for-vscode/pyspark-ineteractive-select-result.png) The submission status appears on the left of the bottom status bar when you're running queries.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-232">![Submit Python job result](./media/hdinsight-for-vscode/pyspark-ineteractive-select-result.png) The submission status appears on the left of the bottom status bar when you're running queries.</span></span> <span data-ttu-id="bdd4b-233">Don't submit other queries when the status is **PySpark Kernel (busy)**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-233">Don't submit other queries when the status is **PySpark Kernel (busy)**.</span></span> 

>[!NOTE]
><span data-ttu-id="bdd4b-234">The clusters can maintain session information.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-234">The clusters can maintain session information.</span></span> <span data-ttu-id="bdd4b-235">The defined variable, function and corresponding values are kept in the session, so they can be referenced across multiple service calls for the same cluster.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-235">The defined variable, function and corresponding values are kept in the session, so they can be referenced across multiple service calls for the same cluster.</span></span> 

### <a name="to-disable-environment-check"></a><span data-ttu-id="bdd4b-236">To disable environment check</span><span class="sxs-lookup"><span data-stu-id="bdd4b-236">To disable environment check</span></span>

<span data-ttu-id="bdd4b-237">By default, HDInsight tools will check environment and install dependent packages when submit interactive PySpark queries.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-237">By default, HDInsight tools will check environment and install dependent packages when submit interactive PySpark queries.</span></span> <span data-ttu-id="bdd4b-238">To disable environment check, set the **hdinsight.disablePysparkEnvironmentValidation** to **yes** under **USER SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-238">To disable environment check, set the **hdinsight.disablePysparkEnvironmentValidation** to **yes** under **USER SETTINGS**.</span></span>

   ![Set the environment check from settings](./media/hdinsight-for-vscode/hdi-azure-hdinsight-environment-check.png)

<span data-ttu-id="bdd4b-240">Alternatively, click **Disable Validation** button when the dialog pops.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-240">Alternatively, click **Disable Validation** button when the dialog pops.</span></span>

   ![Set the environment check from dialog](./media/hdinsight-for-vscode/hdi-azure-hdinsight-environment-check-dialog.png)

### <a name="pyspark3-is-not-supported-with-spark2223"></a><span data-ttu-id="bdd4b-242">PySpark3 is not supported with Spark2.2/2.3</span><span class="sxs-lookup"><span data-stu-id="bdd4b-242">PySpark3 is not supported with Spark2.2/2.3</span></span>

<span data-ttu-id="bdd4b-243">PySpark3 is not supported anymore with Spark 2.2 cluster and Spark2.3 cluster, only "PySpark" is supported for Python.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-243">PySpark3 is not supported anymore with Spark 2.2 cluster and Spark2.3 cluster, only "PySpark" is supported for Python.</span></span> <span data-ttu-id="bdd4b-244">It is known issue that submits to spark 2.2/2.3 fail with Python3.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-244">It is known issue that submits to spark 2.2/2.3 fail with Python3.</span></span>

   ![Submit to python3 get error](./media/hdinsight-for-vscode/hdi-azure-hdinsight-py3-error.png)

<span data-ttu-id="bdd4b-246">Follow the steps to use Python2.x:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-246">Follow the steps to use Python2.x:</span></span> 

1. <span data-ttu-id="bdd4b-247">Install Python 2.7 to local computer and add it to system path.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-247">Install Python 2.7 to local computer and add it to system path.</span></span>

2. <span data-ttu-id="bdd4b-248">Restart VSCode.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-248">Restart VSCode.</span></span>

3. <span data-ttu-id="bdd4b-249">Switch to Python 2 by clicking the **Python XXX** at the status bar then choose the target Python.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-249">Switch to Python 2 by clicking the **Python XXX** at the status bar then choose the target Python.</span></span>

   ![Select python version](./media/hdinsight-for-vscode/hdi-azure-hdinsight-select-python.png)

## <a name="submit-pyspark-batch-job"></a><span data-ttu-id="bdd4b-251">Submit PySpark batch job</span><span class="sxs-lookup"><span data-stu-id="bdd4b-251">Submit PySpark batch job</span></span>

1. <span data-ttu-id="bdd4b-252">Create a new work folder and a new script file with the .py extension if you don't already have them.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-252">Create a new work folder and a new script file with the .py extension if you don't already have them.</span></span>

2. <span data-ttu-id="bdd4b-253">Connect to your Azure account if you haven't already done so.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-253">Connect to your Azure account if you haven't already done so.</span></span>

3. <span data-ttu-id="bdd4b-254">Copy and paste the following code into the script file:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-254">Copy and paste the following code into the script file:</span></span>

    ```python
    from __future__ import print_function
    import sys
    from operator import add
    from pyspark.sql import SparkSession
    if __name__ == "__main__":
        spark = SparkSession\
            .builder\
            .appName("PythonWordCount")\
            .getOrCreate()
    
        lines = spark.read.text('/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv').rdd.map(lambda r: r[0])
        counts = lines.flatMap(lambda x: x.split(' '))\
                    .map(lambda x: (x, 1))\
                    .reduceByKey(add)
        output = counts.collect()
        for (word, count) in output:
            print("%s: %i" % (word, count))
        spark.stop()
    ```
4. <span data-ttu-id="bdd4b-255">Right-click the script editor, and then select **HDInsight: PySpark Batch**, or use shortcut **Ctrl + Alt + H**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-255">Right-click the script editor, and then select **HDInsight: PySpark Batch**, or use shortcut **Ctrl + Alt + H**.</span></span> 

5. <span data-ttu-id="bdd4b-256">Select a cluster to which to submit your PySpark job.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-256">Select a cluster to which to submit your PySpark job.</span></span> 

   ![Submit Python job result](./media/hdinsight-for-vscode/submit-pythonjob-result.png) 

<span data-ttu-id="bdd4b-258">After you submit a Python job, submission logs appear in the **OUTPUT** window in VS Code.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-258">After you submit a Python job, submission logs appear in the **OUTPUT** window in VS Code.</span></span> <span data-ttu-id="bdd4b-259">The **Spark UI URL** and **Yarn UI URL** are shown as well.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-259">The **Spark UI URL** and **Yarn UI URL** are shown as well.</span></span> <span data-ttu-id="bdd4b-260">You can open the URL in a web browser to track the job status.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-260">You can open the URL in a web browser to track the job status.</span></span>

## <a name="livy-configuration"></a><span data-ttu-id="bdd4b-261">Livy configuration</span><span class="sxs-lookup"><span data-stu-id="bdd4b-261">Livy configuration</span></span>

<span data-ttu-id="bdd4b-262">Livy configuration is supported, it could be set at the **.VSCode\settings.json** in work space folder.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-262">Livy configuration is supported, it could be set at the **.VSCode\settings.json** in work space folder.</span></span> <span data-ttu-id="bdd4b-263">Currently, livy configuration only supports Python script.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-263">Currently, livy configuration only supports Python script.</span></span> <span data-ttu-id="bdd4b-264">More details, see [Livy README](https://github.com/cloudera/livy/blob/master/README.rst ).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-264">More details, see [Livy README](https://github.com/cloudera/livy/blob/master/README.rst ).</span></span>

<a id="triggerlivyconf"></a><span data-ttu-id="bdd4b-265">**How to trigger livy configuration**</span><span class="sxs-lookup"><span data-stu-id="bdd4b-265">**How to trigger livy configuration**</span></span>
   
<span data-ttu-id="bdd4b-266">You can find on **File** menu, select **Preferences**, and choose **Settings** on context menu.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-266">You can find on **File** menu, select **Preferences**, and choose **Settings** on context menu.</span></span> <span data-ttu-id="bdd4b-267">Click **WORKSPACE SETTINGS** tab, you can start to set livy configuration.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-267">Click **WORKSPACE SETTINGS** tab, you can start to set livy configuration.</span></span>

<span data-ttu-id="bdd4b-268">You also can submit a file, notice the .vscode folder is added automatically to the work folder.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-268">You also can submit a file, notice the .vscode folder is added automatically to the work folder.</span></span> <span data-ttu-id="bdd4b-269">You can find the livy configuration by clicking **.vscode\settings.json**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-269">You can find the livy configuration by clicking **.vscode\settings.json**.</span></span>

+ <span data-ttu-id="bdd4b-270">The project settings:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-270">The project settings:</span></span>

    ![Livy configuration](./media/hdinsight-for-vscode/hdi-livyconfig.png)

>[!NOTE]
><span data-ttu-id="bdd4b-272">For settings **driverMomory** and **executorMomry**, set the value with unit, for example 1g or 1024m.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-272">For settings **driverMomory** and **executorMomry**, set the value with unit, for example 1g or 1024m.</span></span> 

+ <span data-ttu-id="bdd4b-273">The supported Livy configurations:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-273">The supported Livy configurations:</span></span>   

    <span data-ttu-id="bdd4b-274">**POST /batches** </span><span class="sxs-lookup"><span data-stu-id="bdd4b-274">**POST /batches** </span></span>  
    <span data-ttu-id="bdd4b-275">Request Body</span><span class="sxs-lookup"><span data-stu-id="bdd4b-275">Request Body</span></span>

    | <span data-ttu-id="bdd4b-276">name</span><span class="sxs-lookup"><span data-stu-id="bdd4b-276">name</span></span> | <span data-ttu-id="bdd4b-277">description</span><span class="sxs-lookup"><span data-stu-id="bdd4b-277">description</span></span> | <span data-ttu-id="bdd4b-278">type</span><span class="sxs-lookup"><span data-stu-id="bdd4b-278">type</span></span> | 
    | :- | :- | :- | 
    | <span data-ttu-id="bdd4b-279">file</span><span class="sxs-lookup"><span data-stu-id="bdd4b-279">file</span></span> | <span data-ttu-id="bdd4b-280">File containing the application to execute</span><span class="sxs-lookup"><span data-stu-id="bdd4b-280">File containing the application to execute</span></span> | <span data-ttu-id="bdd4b-281">path (required)</span><span class="sxs-lookup"><span data-stu-id="bdd4b-281">path (required)</span></span> | 
    | <span data-ttu-id="bdd4b-282">proxyUser</span><span class="sxs-lookup"><span data-stu-id="bdd4b-282">proxyUser</span></span> | <span data-ttu-id="bdd4b-283">User to impersonate when running the job</span><span class="sxs-lookup"><span data-stu-id="bdd4b-283">User to impersonate when running the job</span></span> | <span data-ttu-id="bdd4b-284">string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-284">string</span></span> | 
    | <span data-ttu-id="bdd4b-285">className</span><span class="sxs-lookup"><span data-stu-id="bdd4b-285">className</span></span> | <span data-ttu-id="bdd4b-286">Application Java/Spark main class</span><span class="sxs-lookup"><span data-stu-id="bdd4b-286">Application Java/Spark main class</span></span> | <span data-ttu-id="bdd4b-287">string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-287">string</span></span> |
    | <span data-ttu-id="bdd4b-288">args</span><span class="sxs-lookup"><span data-stu-id="bdd4b-288">args</span></span> | <span data-ttu-id="bdd4b-289">Command line arguments for the application</span><span class="sxs-lookup"><span data-stu-id="bdd4b-289">Command line arguments for the application</span></span> | <span data-ttu-id="bdd4b-290">list of strings</span><span class="sxs-lookup"><span data-stu-id="bdd4b-290">list of strings</span></span> | 
    | <span data-ttu-id="bdd4b-291">jars</span><span class="sxs-lookup"><span data-stu-id="bdd4b-291">jars</span></span> | <span data-ttu-id="bdd4b-292">jars to be used in this session</span><span class="sxs-lookup"><span data-stu-id="bdd4b-292">jars to be used in this session</span></span> | <span data-ttu-id="bdd4b-293">List of string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-293">List of string</span></span> | 
    | <span data-ttu-id="bdd4b-294">pyFiles</span><span class="sxs-lookup"><span data-stu-id="bdd4b-294">pyFiles</span></span> | <span data-ttu-id="bdd4b-295">Python files to be used in this session</span><span class="sxs-lookup"><span data-stu-id="bdd4b-295">Python files to be used in this session</span></span> | <span data-ttu-id="bdd4b-296">List of string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-296">List of string</span></span> |
    | <span data-ttu-id="bdd4b-297">files</span><span class="sxs-lookup"><span data-stu-id="bdd4b-297">files</span></span> | <span data-ttu-id="bdd4b-298">files to be used in this session</span><span class="sxs-lookup"><span data-stu-id="bdd4b-298">files to be used in this session</span></span> | <span data-ttu-id="bdd4b-299">List of string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-299">List of string</span></span> |
    | <span data-ttu-id="bdd4b-300">driverMemory</span><span class="sxs-lookup"><span data-stu-id="bdd4b-300">driverMemory</span></span> | <span data-ttu-id="bdd4b-301">Amount of memory to use for the driver process</span><span class="sxs-lookup"><span data-stu-id="bdd4b-301">Amount of memory to use for the driver process</span></span> | <span data-ttu-id="bdd4b-302">string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-302">string</span></span> |
    | <span data-ttu-id="bdd4b-303">driverCores</span><span class="sxs-lookup"><span data-stu-id="bdd4b-303">driverCores</span></span> | <span data-ttu-id="bdd4b-304">Number of cores to use for the driver process</span><span class="sxs-lookup"><span data-stu-id="bdd4b-304">Number of cores to use for the driver process</span></span> | <span data-ttu-id="bdd4b-305">int</span><span class="sxs-lookup"><span data-stu-id="bdd4b-305">int</span></span> |
    | <span data-ttu-id="bdd4b-306">executorMemory</span><span class="sxs-lookup"><span data-stu-id="bdd4b-306">executorMemory</span></span> | <span data-ttu-id="bdd4b-307">Amount of memory to use per executor process</span><span class="sxs-lookup"><span data-stu-id="bdd4b-307">Amount of memory to use per executor process</span></span> | <span data-ttu-id="bdd4b-308">string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-308">string</span></span> |
    | <span data-ttu-id="bdd4b-309">executorCores</span><span class="sxs-lookup"><span data-stu-id="bdd4b-309">executorCores</span></span> | <span data-ttu-id="bdd4b-310">Number of cores to use for each executor</span><span class="sxs-lookup"><span data-stu-id="bdd4b-310">Number of cores to use for each executor</span></span> | <span data-ttu-id="bdd4b-311">int</span><span class="sxs-lookup"><span data-stu-id="bdd4b-311">int</span></span> |
    | <span data-ttu-id="bdd4b-312">numExecutors</span><span class="sxs-lookup"><span data-stu-id="bdd4b-312">numExecutors</span></span> | <span data-ttu-id="bdd4b-313">Number of executors to launch for this session</span><span class="sxs-lookup"><span data-stu-id="bdd4b-313">Number of executors to launch for this session</span></span> | <span data-ttu-id="bdd4b-314">int</span><span class="sxs-lookup"><span data-stu-id="bdd4b-314">int</span></span> |
    | <span data-ttu-id="bdd4b-315">archives</span><span class="sxs-lookup"><span data-stu-id="bdd4b-315">archives</span></span> | <span data-ttu-id="bdd4b-316">Archives to be used in this session</span><span class="sxs-lookup"><span data-stu-id="bdd4b-316">Archives to be used in this session</span></span> | <span data-ttu-id="bdd4b-317">List of string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-317">List of string</span></span> |
    | <span data-ttu-id="bdd4b-318">queue</span><span class="sxs-lookup"><span data-stu-id="bdd4b-318">queue</span></span> | <span data-ttu-id="bdd4b-319">The name of the YARN queue to which submitted</span><span class="sxs-lookup"><span data-stu-id="bdd4b-319">The name of the YARN queue to which submitted</span></span> | <span data-ttu-id="bdd4b-320">string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-320">string</span></span> |
    | <span data-ttu-id="bdd4b-321">name</span><span class="sxs-lookup"><span data-stu-id="bdd4b-321">name</span></span> | <span data-ttu-id="bdd4b-322">The name of this session</span><span class="sxs-lookup"><span data-stu-id="bdd4b-322">The name of this session</span></span> | <span data-ttu-id="bdd4b-323">string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-323">string</span></span> |
    | <span data-ttu-id="bdd4b-324">conf</span><span class="sxs-lookup"><span data-stu-id="bdd4b-324">conf</span></span> | <span data-ttu-id="bdd4b-325">Spark configuration properties</span><span class="sxs-lookup"><span data-stu-id="bdd4b-325">Spark configuration properties</span></span> | <span data-ttu-id="bdd4b-326">Map of key=val</span><span class="sxs-lookup"><span data-stu-id="bdd4b-326">Map of key=val</span></span> |

    <span data-ttu-id="bdd4b-327">Response Body</span><span class="sxs-lookup"><span data-stu-id="bdd4b-327">Response Body</span></span>   
    <span data-ttu-id="bdd4b-328">The created Batch object.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-328">The created Batch object.</span></span>

    | <span data-ttu-id="bdd4b-329">name</span><span class="sxs-lookup"><span data-stu-id="bdd4b-329">name</span></span> | <span data-ttu-id="bdd4b-330">description</span><span class="sxs-lookup"><span data-stu-id="bdd4b-330">description</span></span> | <span data-ttu-id="bdd4b-331">type</span><span class="sxs-lookup"><span data-stu-id="bdd4b-331">type</span></span> | 
    | :- | :- | :- | 
    | <span data-ttu-id="bdd4b-332">id</span><span class="sxs-lookup"><span data-stu-id="bdd4b-332">id</span></span> | <span data-ttu-id="bdd4b-333">The session id</span><span class="sxs-lookup"><span data-stu-id="bdd4b-333">The session id</span></span> | <span data-ttu-id="bdd4b-334">int</span><span class="sxs-lookup"><span data-stu-id="bdd4b-334">int</span></span> | 
    | <span data-ttu-id="bdd4b-335">appId</span><span class="sxs-lookup"><span data-stu-id="bdd4b-335">appId</span></span> | <span data-ttu-id="bdd4b-336">The application id of this session</span><span class="sxs-lookup"><span data-stu-id="bdd4b-336">The application id of this session</span></span> |  <span data-ttu-id="bdd4b-337">String</span><span class="sxs-lookup"><span data-stu-id="bdd4b-337">String</span></span> |
    | <span data-ttu-id="bdd4b-338">appInfo</span><span class="sxs-lookup"><span data-stu-id="bdd4b-338">appInfo</span></span> | <span data-ttu-id="bdd4b-339">The detailed application info</span><span class="sxs-lookup"><span data-stu-id="bdd4b-339">The detailed application info</span></span> | <span data-ttu-id="bdd4b-340">Map of key=val</span><span class="sxs-lookup"><span data-stu-id="bdd4b-340">Map of key=val</span></span> |
    | <span data-ttu-id="bdd4b-341">log</span><span class="sxs-lookup"><span data-stu-id="bdd4b-341">log</span></span> | <span data-ttu-id="bdd4b-342">The log lines</span><span class="sxs-lookup"><span data-stu-id="bdd4b-342">The log lines</span></span> | <span data-ttu-id="bdd4b-343">list of strings</span><span class="sxs-lookup"><span data-stu-id="bdd4b-343">list of strings</span></span> |
    | <span data-ttu-id="bdd4b-344">state</span><span class="sxs-lookup"><span data-stu-id="bdd4b-344">state</span></span> |   <span data-ttu-id="bdd4b-345">The batch state</span><span class="sxs-lookup"><span data-stu-id="bdd4b-345">The batch state</span></span> | <span data-ttu-id="bdd4b-346">string</span><span class="sxs-lookup"><span data-stu-id="bdd4b-346">string</span></span> |

>[!NOTE]
><span data-ttu-id="bdd4b-347">The assigned livy config will display in output pane when submit script.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-347">The assigned livy config will display in output pane when submit script.</span></span>

## <a name="integrate-with-azure-hdinsight-from-explorer"></a><span data-ttu-id="bdd4b-348">Integrate with Azure HDInsight from Explorer</span><span class="sxs-lookup"><span data-stu-id="bdd4b-348">Integrate with Azure HDInsight from Explorer</span></span>

<span data-ttu-id="bdd4b-349">Azure HDInsight has been added to the left panel.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-349">Azure HDInsight has been added to the left panel.</span></span> <span data-ttu-id="bdd4b-350">You can browse and manage the cluster directly.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-350">You can browse and manage the cluster directly.</span></span>

1. <span data-ttu-id="bdd4b-351">Expand the **AZURE HDINSIGHT**, if not sign in, it will show **Sign in to Azure...** link.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-351">Expand the **AZURE HDINSIGHT**, if not sign in, it will show **Sign in to Azure...** link.</span></span>

    ![Sign in link image](./media/hdinsight-for-vscode/hid-azure-hdinsight-sign-in.png)

2. <span data-ttu-id="bdd4b-353">Click **Sign in to Azure**, it pops sign in link and code at the right bottom.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-353">Click **Sign in to Azure**, it pops sign in link and code at the right bottom.</span></span>

    ![Sign in instructions for other environment](./media/hdinsight-for-vscode/hdi-azure-hdinsight-azure-signin-code.png)

3. <span data-ttu-id="bdd4b-355">Click **Copy & Open** button will open browser, paste the code, click **Continue** button, then you will see the hint about sign in successfully.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-355">Click **Copy & Open** button will open browser, paste the code, click **Continue** button, then you will see the hint about sign in successfully.</span></span>

4. <span data-ttu-id="bdd4b-356">After signed in, the available subscriptions and clusters (Spark, Hadoop, and HBase are supported) will be listed in **AZURE HDINSIGHT**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-356">After signed in, the available subscriptions and clusters (Spark, Hadoop, and HBase are supported) will be listed in **AZURE HDINSIGHT**.</span></span> 

   ![Azure HDInsight Subscription](./media/hdinsight-for-vscode/hdi-azure-hdinsight-subscription.png)

5. <span data-ttu-id="bdd4b-358">Expand the cluster to view hive metadata database and table schema.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-358">Expand the cluster to view hive metadata database and table schema.</span></span>

   ![Azure HDInsight cluster](./media/hdinsight-for-vscode/hdi-azure-hdinsight-cluster.png)

## <a name="additional-features"></a><span data-ttu-id="bdd4b-360">Additional features</span><span class="sxs-lookup"><span data-stu-id="bdd4b-360">Additional features</span></span>

<span data-ttu-id="bdd4b-361">HDInsight for VS Code supports the following features:</span><span class="sxs-lookup"><span data-stu-id="bdd4b-361">HDInsight for VS Code supports the following features:</span></span>

- <span data-ttu-id="bdd4b-362">**IntelliSense auto-complete**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-362">**IntelliSense auto-complete**.</span></span> <span data-ttu-id="bdd4b-363">Suggestions pop up for keyword, methods, variables, and so on.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-363">Suggestions pop up for keyword, methods, variables, and so on.</span></span> <span data-ttu-id="bdd4b-364">Different icons represent different types of objects.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-364">Different icons represent different types of objects.</span></span>

    ![HDInsight Tools for Visual Studio Code IntelliSense object types](./media/hdinsight-for-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- <span data-ttu-id="bdd4b-366">**IntelliSense error marker**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-366">**IntelliSense error marker**.</span></span> <span data-ttu-id="bdd4b-367">The language service underlines the editing errors for the Hive script.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-367">The language service underlines the editing errors for the Hive script.</span></span>     
- <span data-ttu-id="bdd4b-368">**Syntax highlights**.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-368">**Syntax highlights**.</span></span> <span data-ttu-id="bdd4b-369">The language service uses different colors to differentiate variables, keywords, data type, functions, and so on.</span><span class="sxs-lookup"><span data-stu-id="bdd4b-369">The language service uses different colors to differentiate variables, keywords, data type, functions, and so on.</span></span> 

    ![HDInsight Tools for Visual Studio Code syntax highlights](./media/hdinsight-for-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="bdd4b-371">Next steps</span><span class="sxs-lookup"><span data-stu-id="bdd4b-371">Next steps</span></span>

### <a name="demo"></a><span data-ttu-id="bdd4b-372">Demo</span><span class="sxs-lookup"><span data-stu-id="bdd4b-372">Demo</span></span>
* <span data-ttu-id="bdd4b-373">HDInsight for VS Code: [Video](https://go.microsoft.com/fwlink/?linkid=858706)</span><span class="sxs-lookup"><span data-stu-id="bdd4b-373">HDInsight for VS Code: [Video](https://go.microsoft.com/fwlink/?linkid=858706)</span></span>

### <a name="tools-and-extensions"></a><span data-ttu-id="bdd4b-374">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="bdd4b-374">Tools and extensions</span></span>

* [<span data-ttu-id="bdd4b-375">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span><span class="sxs-lookup"><span data-stu-id="bdd4b-375">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](spark/apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="bdd4b-376">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span><span class="sxs-lookup"><span data-stu-id="bdd4b-376">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](spark/apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="bdd4b-377">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="bdd4b-377">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hadoop/hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="bdd4b-378">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span><span class="sxs-lookup"><span data-stu-id="bdd4b-378">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](spark/apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="bdd4b-379">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="bdd4b-379">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](spark/apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="bdd4b-380">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="bdd4b-380">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](spark/apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="bdd4b-381">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="bdd4b-381">Use external packages with Jupyter notebooks</span></span>](spark/apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="bdd4b-382">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="bdd4b-382">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](spark/apache-spark-jupyter-notebook-install-locally.md)
* [<span data-ttu-id="bdd4b-383">Visualize Hive data with Microsoft Power BI in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="bdd4b-383">Visualize Hive data with Microsoft Power BI in Azure HDInsight</span></span>](hadoop/apache-hadoop-connect-hive-power-bi.md)
* <span data-ttu-id="bdd4b-384">[Visualize Interactive Query Hive data with Power BI in Azure HDInsight](./interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).</span><span class="sxs-lookup"><span data-stu-id="bdd4b-384">[Visualize Interactive Query Hive data with Power BI in Azure HDInsight](./interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).</span></span>
* [<span data-ttu-id="bdd4b-385">Set Up PySpark Interactive Environment for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bdd4b-385">Set Up PySpark Interactive Environment for Visual Studio Code</span></span>](set-up-pyspark-interactive-environment.md)
* [<span data-ttu-id="bdd4b-386">Use Zeppelin to run Hive queries in Azure HDInsight </span><span class="sxs-lookup"><span data-stu-id="bdd4b-386">Use Zeppelin to run Hive queries in Azure HDInsight </span></span>](./hdinsight-connect-hive-zeppelin.md)

### <a name="scenarios"></a><span data-ttu-id="bdd4b-387">Scenarios</span><span class="sxs-lookup"><span data-stu-id="bdd4b-387">Scenarios</span></span>
* [<span data-ttu-id="bdd4b-388">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="bdd4b-388">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](spark/apache-spark-use-bi-tools.md)
* [<span data-ttu-id="bdd4b-389">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="bdd4b-389">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](spark/apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="bdd4b-390">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="bdd4b-390">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](spark/apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="bdd4b-391">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="bdd4b-391">Website log analysis using Spark in HDInsight</span></span>](spark/apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-running-applications"></a><span data-ttu-id="bdd4b-392">Create and running applications</span><span class="sxs-lookup"><span data-stu-id="bdd4b-392">Create and running applications</span></span>
* [<span data-ttu-id="bdd4b-393">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="bdd4b-393">Create a standalone application using Scala</span></span>](spark/apache-spark-create-standalone-application.md)
* [<span data-ttu-id="bdd4b-394">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="bdd4b-394">Run jobs remotely on a Spark cluster using Livy</span></span>](spark/apache-spark-livy-rest-interface.md)

### <a name="manage-resources"></a><span data-ttu-id="bdd4b-395">Manage resources</span><span class="sxs-lookup"><span data-stu-id="bdd4b-395">Manage resources</span></span>
* [<span data-ttu-id="bdd4b-396">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="bdd4b-396">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](spark/apache-spark-resource-manager.md)
* [<span data-ttu-id="bdd4b-397">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="bdd4b-397">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](spark/apache-spark-job-debugging.md)



