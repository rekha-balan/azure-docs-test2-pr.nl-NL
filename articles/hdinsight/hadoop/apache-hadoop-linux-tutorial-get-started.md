---
title: 'Quickstart: Get started with Hadoop and Hive in Azure HDInsight using Resource Manager template '
description: Learn how to create HDInsight clusters, and query data with Hive.
keywords: hadoop getting started,hadoop linux,hadoop quickstart,hive getting started,hive quickstart
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive,hdiseo17may2017,mvc
ms.topic: quickstart
ms.date: 05/07/2018
ms.openlocfilehash: 9e58f0a9de20acd2a8d65f6a2252e2d439beb250
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856801"
---
# <a name="quickstart-get-started-with-hadoop-and-hive-in-azure-hdinsight-using-resource-manager-template"></a><span data-ttu-id="67061-104">Quickstart: Get started with Hadoop and Hive in Azure HDInsight using Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="67061-104">Quickstart: Get started with Hadoop and Hive in Azure HDInsight using Resource Manager template</span></span>

<span data-ttu-id="67061-105">In this article, you learn how to create [Hadoop](http://hadoop.apache.org/) clusters in HDInsight using a Resource Manager template, and then run Hive jobs in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67061-105">In this article, you learn how to create [Hadoop](http://hadoop.apache.org/) clusters in HDInsight using a Resource Manager template, and then run Hive jobs in HDInsight.</span></span> <span data-ttu-id="67061-106">Most of Hadoop jobs are batch jobs.</span><span class="sxs-lookup"><span data-stu-id="67061-106">Most of Hadoop jobs are batch jobs.</span></span> <span data-ttu-id="67061-107">You create a cluster, run some jobs, and then delete the cluster.</span><span class="sxs-lookup"><span data-stu-id="67061-107">You create a cluster, run some jobs, and then delete the cluster.</span></span> <span data-ttu-id="67061-108">In this article, you perform all the three tasks.</span><span class="sxs-lookup"><span data-stu-id="67061-108">In this article, you perform all the three tasks.</span></span>

<span data-ttu-id="67061-109">In this quickstart, you use a Resource Manager template to create an HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="67061-109">In this quickstart, you use a Resource Manager template to create an HDInsight Hadoop cluster.</span></span> <span data-ttu-id="67061-110">You can also create a cluster using the [Azure Portal](apache-hadoop-linux-create-cluster-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="67061-110">You can also create a cluster using the [Azure Portal](apache-hadoop-linux-create-cluster-get-started-portal.md).</span></span>

<span data-ttu-id="67061-111">Currently HDInsight comes with [seven different cluster types](./apache-hadoop-introduction.md#cluster-types-in-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="67061-111">Currently HDInsight comes with [seven different cluster types](./apache-hadoop-introduction.md#cluster-types-in-hdinsight).</span></span> <span data-ttu-id="67061-112">Each cluster type supports a different set of components.</span><span class="sxs-lookup"><span data-stu-id="67061-112">Each cluster type supports a different set of components.</span></span> <span data-ttu-id="67061-113">All cluster types support Hive.</span><span class="sxs-lookup"><span data-stu-id="67061-113">All cluster types support Hive.</span></span> <span data-ttu-id="67061-114">For a list of supported components in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](../hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="67061-114">For a list of supported components in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](../hdinsight-component-versioning.md)</span></span>  

<span data-ttu-id="67061-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="67061-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

<a name="create-cluster"></a>
## <a name="create-a-hadoop-cluster"></a><span data-ttu-id="67061-116">Create a Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="67061-116">Create a Hadoop cluster</span></span>

<span data-ttu-id="67061-117">In this section, you create a Hadoop cluster in HDInsight using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="67061-117">In this section, you create a Hadoop cluster in HDInsight using an Azure Resource Manager template.</span></span> <span data-ttu-id="67061-118">Resource Manager template experience is not required for following this article.</span><span class="sxs-lookup"><span data-stu-id="67061-118">Resource Manager template experience is not required for following this article.</span></span> 

1. <span data-ttu-id="67061-119">Click the **Deploy to Azure** button below to sign in to Azure and open the Resource Manager template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="67061-119">Click the **Deploy to Azure** button below to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/apache-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="67061-120">Enter or select the values as suggested in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="67061-120">Enter or select the values as suggested in the following screenshot:</span></span>

    > [!NOTE]
    > <span data-ttu-id="67061-121">The values you provide must be unique and should follow the naming guidelines.</span><span class="sxs-lookup"><span data-stu-id="67061-121">The values you provide must be unique and should follow the naming guidelines.</span></span> <span data-ttu-id="67061-122">The template does not perform validation checks.</span><span class="sxs-lookup"><span data-stu-id="67061-122">The template does not perform validation checks.</span></span> <span data-ttu-id="67061-123">If the values you provide are already in use, or do not follow the guidelines, you get an error after you have submitted the template.</span><span class="sxs-lookup"><span data-stu-id="67061-123">If the values you provide are already in use, or do not follow the guidelines, you get an error after you have submitted the template.</span></span>       
    > 
    >
    
    <span data-ttu-id="67061-124">![HDInsight Linux get started Resource Manager template on portal](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "Deploy Hadoop cluster in HDInsigut using the Azure portal and a resource group manager template")</span><span class="sxs-lookup"><span data-stu-id="67061-124">![HDInsight Linux get started Resource Manager template on portal](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "Deploy Hadoop cluster in HDInsigut using the Azure portal and a resource group manager template")</span></span>

    <span data-ttu-id="67061-125">Enter or select the following values:</span><span class="sxs-lookup"><span data-stu-id="67061-125">Enter or select the following values:</span></span>
    
    |<span data-ttu-id="67061-126">Property</span><span class="sxs-lookup"><span data-stu-id="67061-126">Property</span></span>  |<span data-ttu-id="67061-127">Description</span><span class="sxs-lookup"><span data-stu-id="67061-127">Description</span></span>  |
    |---------|---------|
    |<span data-ttu-id="67061-128">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="67061-128">**Subscription**</span></span>     |  <span data-ttu-id="67061-129">Select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="67061-129">Select your Azure subscription.</span></span> |
    |<span data-ttu-id="67061-130">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="67061-130">**Resource group**</span></span>     | <span data-ttu-id="67061-131">Create a resource group or select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="67061-131">Create a resource group or select an existing resource group.</span></span>  <span data-ttu-id="67061-132">A resource group is a container of Azure components.</span><span class="sxs-lookup"><span data-stu-id="67061-132">A resource group is a container of Azure components.</span></span>  <span data-ttu-id="67061-133">In this case, the resource group contains the HDInsight cluster and the dependent Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="67061-133">In this case, the resource group contains the HDInsight cluster and the dependent Azure Storage account.</span></span> |
    |<span data-ttu-id="67061-134">**Location**</span><span class="sxs-lookup"><span data-stu-id="67061-134">**Location**</span></span>     | <span data-ttu-id="67061-135">Select an Azure location where you want to create your cluster.</span><span class="sxs-lookup"><span data-stu-id="67061-135">Select an Azure location where you want to create your cluster.</span></span>  <span data-ttu-id="67061-136">Choose a location closer to you for better performance.</span><span class="sxs-lookup"><span data-stu-id="67061-136">Choose a location closer to you for better performance.</span></span> |
    |<span data-ttu-id="67061-137">**Cluster Type**</span><span class="sxs-lookup"><span data-stu-id="67061-137">**Cluster Type**</span></span>     | <span data-ttu-id="67061-138">Select **hadoop**.</span><span class="sxs-lookup"><span data-stu-id="67061-138">Select **hadoop**.</span></span> |
    |<span data-ttu-id="67061-139">**Cluster Name**</span><span class="sxs-lookup"><span data-stu-id="67061-139">**Cluster Name**</span></span>     | <span data-ttu-id="67061-140">Enter a name for the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="67061-140">Enter a name for the Hadoop cluster.</span></span> <span data-ttu-id="67061-141">Because all clusters in HDInsight share the same DNS namespace this name needs to be unique.</span><span class="sxs-lookup"><span data-stu-id="67061-141">Because all clusters in HDInsight share the same DNS namespace this name needs to be unique.</span></span> <span data-ttu-id="67061-142">The name can consist of up to 59 characters includings letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="67061-142">The name can consist of up to 59 characters includings letters, numbers, and hyphens.</span></span> <span data-ttu-id="67061-143">The first and last characters of the name cannot be hyphens.</span><span class="sxs-lookup"><span data-stu-id="67061-143">The first and last characters of the name cannot be hyphens.</span></span> |
    |<span data-ttu-id="67061-144">**Cluster login name and password**</span><span class="sxs-lookup"><span data-stu-id="67061-144">**Cluster login name and password**</span></span>     | <span data-ttu-id="67061-145">The default login name is **admin**. The password must be at least 10 characters in length and must contain at least one digit, one uppercase, and one lower case letter, one non-alphanumeric character (except characters ' " \` \).</span><span class="sxs-lookup"><span data-stu-id="67061-145">The default login name is **admin**. The password must be at least 10 characters in length and must contain at least one digit, one uppercase, and one lower case letter, one non-alphanumeric character (except characters ' " \` \).</span></span> <span data-ttu-id="67061-146">Make sure you **do not provide** common passwords such as "Pass@word1".</span><span class="sxs-lookup"><span data-stu-id="67061-146">Make sure you **do not provide** common passwords such as "Pass@word1".</span></span>|
    |<span data-ttu-id="67061-147">**SSH username and password**</span><span class="sxs-lookup"><span data-stu-id="67061-147">**SSH username and password**</span></span>     | <span data-ttu-id="67061-148">The default username is **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="67061-148">The default username is **sshuser**.</span></span>  <span data-ttu-id="67061-149">You can rename the SSH username.</span><span class="sxs-lookup"><span data-stu-id="67061-149">You can rename the SSH username.</span></span>  <span data-ttu-id="67061-150">The SSH user password has the same requirements as the cluster login password.</span><span class="sxs-lookup"><span data-stu-id="67061-150">The SSH user password has the same requirements as the cluster login password.</span></span>|
       
    <span data-ttu-id="67061-151">Some properties have been hardcoded in the template.</span><span class="sxs-lookup"><span data-stu-id="67061-151">Some properties have been hardcoded in the template.</span></span>  <span data-ttu-id="67061-152">You can configure these values from the template.</span><span class="sxs-lookup"><span data-stu-id="67061-152">You can configure these values from the template.</span></span> <span data-ttu-id="67061-153">For more explanation of these properties, see [Create Hadoop clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="67061-153">For more explanation of these properties, see [Create Hadoop clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span></span>

3. <span data-ttu-id="67061-154">Select **I agree to the terms and conditions stated above** and **Pin to dashboard**, and then select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="67061-154">Select **I agree to the terms and conditions stated above** and **Pin to dashboard**, and then select **Purchase**.</span></span> <span data-ttu-id="67061-155">You shall see a new tile titled **Submitting deployment** on the portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="67061-155">You shall see a new tile titled **Submitting deployment** on the portal dashboard.</span></span> <span data-ttu-id="67061-156">It takes about 20 minutes to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="67061-156">It takes about 20 minutes to create a cluster.</span></span>

    <span data-ttu-id="67061-157">![Template deployment progress](./media/apache-hadoop-linux-tutorial-get-started/deployment-progress-tile.png "Azure Template deployment progress")</span><span class="sxs-lookup"><span data-stu-id="67061-157">![Template deployment progress](./media/apache-hadoop-linux-tutorial-get-started/deployment-progress-tile.png "Azure Template deployment progress")</span></span>

4. <span data-ttu-id="67061-158">Once the cluster is created, the caption of the tile is changed to the resource group name you specified.</span><span class="sxs-lookup"><span data-stu-id="67061-158">Once the cluster is created, the caption of the tile is changed to the resource group name you specified.</span></span> <span data-ttu-id="67061-159">The tile also lists the HDInsight cluster that is created within the resource group.</span><span class="sxs-lookup"><span data-stu-id="67061-159">The tile also lists the HDInsight cluster that is created within the resource group.</span></span> 
   
    <span data-ttu-id="67061-160">![HDInsight Linux get started resource group](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Azure HDInsight cluster resource group")</span><span class="sxs-lookup"><span data-stu-id="67061-160">![HDInsight Linux get started resource group](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Azure HDInsight cluster resource group")</span></span>
    
5. <span data-ttu-id="67061-161">The tile also lists the default storage associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="67061-161">The tile also lists the default storage associated with the cluster.</span></span> <span data-ttu-id="67061-162">Each cluster has an [Azure Storage account](../hdinsight-hadoop-use-blob-storage.md) or an [Azure Data Lake account](../hdinsight-hadoop-use-data-lake-store.md) dependency.</span><span class="sxs-lookup"><span data-stu-id="67061-162">Each cluster has an [Azure Storage account](../hdinsight-hadoop-use-blob-storage.md) or an [Azure Data Lake account](../hdinsight-hadoop-use-data-lake-store.md) dependency.</span></span> <span data-ttu-id="67061-163">It is referred as the default storage account.</span><span class="sxs-lookup"><span data-stu-id="67061-163">It is referred as the default storage account.</span></span> <span data-ttu-id="67061-164">HDInsight cluster and its default storage account must be co-located in the same Azure region.</span><span class="sxs-lookup"><span data-stu-id="67061-164">HDInsight cluster and its default storage account must be co-located in the same Azure region.</span></span> <span data-ttu-id="67061-165">Deleting clusters does not delete the storage account.</span><span class="sxs-lookup"><span data-stu-id="67061-165">Deleting clusters does not delete the storage account.</span></span>
    

> [!NOTE]
> <span data-ttu-id="67061-166">For other cluster creation methods and understanding the properties used in this tutorial, see [Create HDInsight clusters](../hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="67061-166">For other cluster creation methods and understanding the properties used in this tutorial, see [Create HDInsight clusters](../hdinsight-hadoop-provision-linux-clusters.md).</span></span>       
> 
>

## <a name="use-vscode-to-run-hive-queries"></a><span data-ttu-id="67061-167">Use VSCode to run Hive queries</span><span class="sxs-lookup"><span data-stu-id="67061-167">Use VSCode to run Hive queries</span></span>

<span data-ttu-id="67061-168">How to get HDInsight Tools in VSCode, see [Use Azure HDInsight Tools for Visual Studio Code](../hdinsight-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="67061-168">How to get HDInsight Tools in VSCode, see [Use Azure HDInsight Tools for Visual Studio Code](../hdinsight-for-vscode.md).</span></span>

### <a name="submit-interactive-hive-queries"></a><span data-ttu-id="67061-169">Submit interactive Hive queries</span><span class="sxs-lookup"><span data-stu-id="67061-169">Submit interactive Hive queries</span></span>

<span data-ttu-id="67061-170">With HDInsight Tools for VSCode, you can submit interactive Hive queries to HDInsight interactive query clusters.</span><span class="sxs-lookup"><span data-stu-id="67061-170">With HDInsight Tools for VSCode, you can submit interactive Hive queries to HDInsight interactive query clusters.</span></span>

1. <span data-ttu-id="67061-171">Create a new work folder and a new Hive script file if you don't already have them.</span><span class="sxs-lookup"><span data-stu-id="67061-171">Create a new work folder and a new Hive script file if you don't already have them.</span></span>

2. <span data-ttu-id="67061-172">Connect to your Azure account, and then configure the default cluster if you haven't already done so.</span><span class="sxs-lookup"><span data-stu-id="67061-172">Connect to your Azure account, and then configure the default cluster if you haven't already done so.</span></span>

3. <span data-ttu-id="67061-173">Copy and paste the following code into your Hive file, and then save it.</span><span class="sxs-lookup"><span data-stu-id="67061-173">Copy and paste the following code into your Hive file, and then save it.</span></span>

    ```hiveql
    SELECT * FROM hivesampletable;
    ```
4. <span data-ttu-id="67061-174">Right-click the script editor, and then select **HDInsight: Hive Interactive** to submit the query.</span><span class="sxs-lookup"><span data-stu-id="67061-174">Right-click the script editor, and then select **HDInsight: Hive Interactive** to submit the query.</span></span> <span data-ttu-id="67061-175">The tools also allow you to submit a block of code instead of the whole script file using the context menu.</span><span class="sxs-lookup"><span data-stu-id="67061-175">The tools also allow you to submit a block of code instead of the whole script file using the context menu.</span></span> <span data-ttu-id="67061-176">Soon after, the query results appear in a new tab.</span><span class="sxs-lookup"><span data-stu-id="67061-176">Soon after, the query results appear in a new tab.</span></span>

   ![Interactive Hive result](./media/apache-hadoop-linux-tutorial-get-started/interactive-hive-result.png)

    - <span data-ttu-id="67061-178">**RESULTS** panel: You can save the whole result as CSV, JSON, or Excel file to local path, or just select multiple lines.</span><span class="sxs-lookup"><span data-stu-id="67061-178">**RESULTS** panel: You can save the whole result as CSV, JSON, or Excel file to local path, or just select multiple lines.</span></span>

    - <span data-ttu-id="67061-179">**MESSAGES** panel: When you select **Line** number, it jumps to the first line of the running script.</span><span class="sxs-lookup"><span data-stu-id="67061-179">**MESSAGES** panel: When you select **Line** number, it jumps to the first line of the running script.</span></span>

<span data-ttu-id="67061-180">Running the interactive query takes much less time than [running a Hive batch job](#submit-hive-batch-scripts).</span><span class="sxs-lookup"><span data-stu-id="67061-180">Running the interactive query takes much less time than [running a Hive batch job](#submit-hive-batch-scripts).</span></span>

### <a name="submit-hive-batch-scripts"></a><span data-ttu-id="67061-181">Submit Hive batch scripts</span><span class="sxs-lookup"><span data-stu-id="67061-181">Submit Hive batch scripts</span></span>

1. <span data-ttu-id="67061-182">Create a new work folder and a new Hive script file if you don't already have them.</span><span class="sxs-lookup"><span data-stu-id="67061-182">Create a new work folder and a new Hive script file if you don't already have them.</span></span>

2. <span data-ttu-id="67061-183">Connect to your Azure account, and then configure the default cluster if you haven't already done so.</span><span class="sxs-lookup"><span data-stu-id="67061-183">Connect to your Azure account, and then configure the default cluster if you haven't already done so.</span></span>

3. <span data-ttu-id="67061-184">Copy and paste the following code into your Hive file, and then save it.</span><span class="sxs-lookup"><span data-stu-id="67061-184">Copy and paste the following code into your Hive file, and then save it.</span></span>

    ```hiveql
    SELECT * FROM hivesampletable;
    ```
4. <span data-ttu-id="67061-185">Right-click the script editor, and then select **HDInsight: Hive Batch** to submit a Hive job.</span><span class="sxs-lookup"><span data-stu-id="67061-185">Right-click the script editor, and then select **HDInsight: Hive Batch** to submit a Hive job.</span></span> 

5. <span data-ttu-id="67061-186">Select the cluster to which you want to submit.</span><span class="sxs-lookup"><span data-stu-id="67061-186">Select the cluster to which you want to submit.</span></span>  

    <span data-ttu-id="67061-187">After you submit a Hive job, the submission success info and jobid appears in the **OUTPUT** panel.</span><span class="sxs-lookup"><span data-stu-id="67061-187">After you submit a Hive job, the submission success info and jobid appears in the **OUTPUT** panel.</span></span> <span data-ttu-id="67061-188">The Hive job also opens **WEB BROWSER**, which shows the real-time job  logs and status.</span><span class="sxs-lookup"><span data-stu-id="67061-188">The Hive job also opens **WEB BROWSER**, which shows the real-time job  logs and status.</span></span>

   ![submit Hive job result](./media/apache-hadoop-linux-tutorial-get-started/submit-Hivejob-result.png)

<span data-ttu-id="67061-190">[Submitting interactive Hive queries](#submit-interactive-hive-queries) takes much less time than submitting a batch job.</span><span class="sxs-lookup"><span data-stu-id="67061-190">[Submitting interactive Hive queries](#submit-interactive-hive-queries) takes much less time than submitting a batch job.</span></span>

## <a name="use-visualstudio-to-run-hive-queries"></a><span data-ttu-id="67061-191">Use VisualStudio to run Hive queries</span><span class="sxs-lookup"><span data-stu-id="67061-191">Use VisualStudio to run Hive queries</span></span>

<span data-ttu-id="67061-192">How to get HDInsight Tools in Visual Studio, see [Use Data Lake Tools for Visual Studio](./apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="67061-192">How to get HDInsight Tools in Visual Studio, see [Use Data Lake Tools for Visual Studio](./apache-hadoop-visual-studio-tools-get-started.md).</span></span>

### <a name="run-hive-queries"></a><span data-ttu-id="67061-193">Run Hive queries</span><span class="sxs-lookup"><span data-stu-id="67061-193">Run Hive queries</span></span>

<span data-ttu-id="67061-194">You have two options for creating and running Hive queries:</span><span class="sxs-lookup"><span data-stu-id="67061-194">You have two options for creating and running Hive queries:</span></span>

* <span data-ttu-id="67061-195">Create ad-hoc queries</span><span class="sxs-lookup"><span data-stu-id="67061-195">Create ad-hoc queries</span></span>
* <span data-ttu-id="67061-196">Create a Hive application</span><span class="sxs-lookup"><span data-stu-id="67061-196">Create a Hive application</span></span>

<span data-ttu-id="67061-197">To create and run ad-hoc queries:</span><span class="sxs-lookup"><span data-stu-id="67061-197">To create and run ad-hoc queries:</span></span>

1. <span data-ttu-id="67061-198">In **Server Explorer**, select **Azure** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="67061-198">In **Server Explorer**, select **Azure** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="67061-199">Right-click the cluster where you want to run the query, and then select **Write a Hive Query**.</span><span class="sxs-lookup"><span data-stu-id="67061-199">Right-click the cluster where you want to run the query, and then select **Write a Hive Query**.</span></span>  

3. <span data-ttu-id="67061-200">Enter the Hive queries.</span><span class="sxs-lookup"><span data-stu-id="67061-200">Enter the Hive queries.</span></span> 

    <span data-ttu-id="67061-201">The Hive editor supports IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="67061-201">The Hive editor supports IntelliSense.</span></span> <span data-ttu-id="67061-202">Data Lake Tools for Visual Studio supports loading remote metadata when you edit your Hive script.</span><span class="sxs-lookup"><span data-stu-id="67061-202">Data Lake Tools for Visual Studio supports loading remote metadata when you edit your Hive script.</span></span> <span data-ttu-id="67061-203">For example, if you type **SELECT \* FROM**, IntelliSense lists all the suggested table names.</span><span class="sxs-lookup"><span data-stu-id="67061-203">For example, if you type **SELECT \* FROM**, IntelliSense lists all the suggested table names.</span></span> <span data-ttu-id="67061-204">When a table name is specified, IntelliSense lists the column names.</span><span class="sxs-lookup"><span data-stu-id="67061-204">When a table name is specified, IntelliSense lists the column names.</span></span> <span data-ttu-id="67061-205">The tools support most Hive DML statements, subqueries, and built-in UDFs.</span><span class="sxs-lookup"><span data-stu-id="67061-205">The tools support most Hive DML statements, subqueries, and built-in UDFs.</span></span>
   
    <span data-ttu-id="67061-206">![Screenshot of an HDInsight Visual Studio Tools IntelliSense example 1](./media/apache-hadoop-linux-tutorial-get-started/vs-intellisense-table-name.png "U-SQL IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="67061-206">![Screenshot of an HDInsight Visual Studio Tools IntelliSense example 1](./media/apache-hadoop-linux-tutorial-get-started/vs-intellisense-table-name.png "U-SQL IntelliSense")</span></span>
   
    <span data-ttu-id="67061-207">![Screenshot of an HDInsight Visual Studio Tools IntelliSense example 2](./media/apache-hadoop-linux-tutorial-get-started/vs-intellisense-column-name.png "U-SQL IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="67061-207">![Screenshot of an HDInsight Visual Studio Tools IntelliSense example 2](./media/apache-hadoop-linux-tutorial-get-started/vs-intellisense-column-name.png "U-SQL IntelliSense")</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="67061-208">IntelliSense suggests only the metadata of the cluster that is selected in the HDInsight toolbar.</span><span class="sxs-lookup"><span data-stu-id="67061-208">IntelliSense suggests only the metadata of the cluster that is selected in the HDInsight toolbar.</span></span>
   > 
   
4. <span data-ttu-id="67061-209">Select **Submit** or **Submit (Advanced)**.</span><span class="sxs-lookup"><span data-stu-id="67061-209">Select **Submit** or **Submit (Advanced)**.</span></span> 
   
    ![Screenshot of submit a hive query](./media/apache-hadoop-linux-tutorial-get-started/vs-batch-query.png)

   <span data-ttu-id="67061-211">If you select the advanced submit option, configure **Job Name**, **Arguments**, **Additional Configurations**, and **Status Directory** for the script:</span><span class="sxs-lookup"><span data-stu-id="67061-211">If you select the advanced submit option, configure **Job Name**, **Arguments**, **Additional Configurations**, and **Status Directory** for the script:</span></span>

    <span data-ttu-id="67061-212">![Screenshot of an HDInsight Hadoop Hive query](./media/apache-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Submit queries")</span><span class="sxs-lookup"><span data-stu-id="67061-212">![Screenshot of an HDInsight Hadoop Hive query](./media/apache-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Submit queries")</span></span>

   <span data-ttu-id="67061-213">Run Interactive Hive queries</span><span class="sxs-lookup"><span data-stu-id="67061-213">Run Interactive Hive queries</span></span>

   * <span data-ttu-id="67061-214">click on down-arrow to choose **interactive**.</span><span class="sxs-lookup"><span data-stu-id="67061-214">click on down-arrow to choose **interactive**.</span></span> 
   
   * <span data-ttu-id="67061-215">Click **Execute**.</span><span class="sxs-lookup"><span data-stu-id="67061-215">Click **Execute**.</span></span>

   ![Screenshot of Execute Interactive Hive queries](./media/apache-hadoop-linux-tutorial-get-started/vs-execute-hive-query.png)

<span data-ttu-id="67061-217">To create and run a Hive solution:</span><span class="sxs-lookup"><span data-stu-id="67061-217">To create and run a Hive solution:</span></span>

1. <span data-ttu-id="67061-218">On the **File** menu, select **New**, and then select **Project**.</span><span class="sxs-lookup"><span data-stu-id="67061-218">On the **File** menu, select **New**, and then select **Project**.</span></span>
2. <span data-ttu-id="67061-219">In the left pane, select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="67061-219">In the left pane, select **HDInsight**.</span></span> <span data-ttu-id="67061-220">In the middle pane, select **Hive Application**.</span><span class="sxs-lookup"><span data-stu-id="67061-220">In the middle pane, select **Hive Application**.</span></span> <span data-ttu-id="67061-221">Enter the properties, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="67061-221">Enter the properties, and then select **OK**.</span></span>
   
    <span data-ttu-id="67061-222">![Screenshot of an HDInsight Visual Studio Tools new Hive project](./media/apache-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Create Hive applications from Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="67061-222">![Screenshot of an HDInsight Visual Studio Tools new Hive project](./media/apache-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Create Hive applications from Visual Studio")</span></span>
3. <span data-ttu-id="67061-223">In **Solution Explorer**, double-click **Script.hql** to open the script.</span><span class="sxs-lookup"><span data-stu-id="67061-223">In **Solution Explorer**, double-click **Script.hql** to open the script.</span></span>
4. <span data-ttu-id="67061-224">Enter the Hive queries and submit.</span><span class="sxs-lookup"><span data-stu-id="67061-224">Enter the Hive queries and submit.</span></span> <span data-ttu-id="67061-225">(Refer to the step3&4 above)</span><span class="sxs-lookup"><span data-stu-id="67061-225">(Refer to the step3&4 above)</span></span>  



## <a name="run-hive-queries"></a><span data-ttu-id="67061-226">Run Hive queries</span><span class="sxs-lookup"><span data-stu-id="67061-226">Run Hive queries</span></span>

<span data-ttu-id="67061-227">[Apache Hive](hdinsight-use-hive.md) is the most popular component used in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67061-227">[Apache Hive](hdinsight-use-hive.md) is the most popular component used in HDInsight.</span></span> <span data-ttu-id="67061-228">There are many ways to run Hive jobs in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67061-228">There are many ways to run Hive jobs in HDInsight.</span></span> <span data-ttu-id="67061-229">In this tutorial, you use the Ambari Hive view from the portal.</span><span class="sxs-lookup"><span data-stu-id="67061-229">In this tutorial, you use the Ambari Hive view from the portal.</span></span> <span data-ttu-id="67061-230">For other methods for submitting Hive jobs, see [Use Hive in HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="67061-230">For other methods for submitting Hive jobs, see [Use Hive in HDInsight](hdinsight-use-hive.md).</span></span>

1. <span data-ttu-id="67061-231">To open Ambari, from the previous screenshot, select **Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="67061-231">To open Ambari, from the previous screenshot, select **Cluster Dashboard**.</span></span>  <span data-ttu-id="67061-232">You can also browse to  **https://&lt;ClusterName>.azurehdinsight.net**, where &lt;ClusterName> is the cluster you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="67061-232">You can also browse to  **https://&lt;ClusterName>.azurehdinsight.net**, where &lt;ClusterName> is the cluster you created in the previous section.</span></span>

    <span data-ttu-id="67061-233">![HDInsight Linux get started cluster dashboard](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-open-cluster-dashboard.png "HDInsight Linux get started cluster dashboard")</span><span class="sxs-lookup"><span data-stu-id="67061-233">![HDInsight Linux get started cluster dashboard](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-open-cluster-dashboard.png "HDInsight Linux get started cluster dashboard")</span></span>

2. <span data-ttu-id="67061-234">Enter the Hadoop username and password that you specified while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="67061-234">Enter the Hadoop username and password that you specified while creating the cluster.</span></span> <span data-ttu-id="67061-235">The default username is **admin**.</span><span class="sxs-lookup"><span data-stu-id="67061-235">The default username is **admin**.</span></span>

3. <span data-ttu-id="67061-236">Open **Hive View** as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="67061-236">Open **Hive View** as shown in the following screenshot:</span></span>
   
    <span data-ttu-id="67061-237">![Selecting Ambari views](./media/apache-hadoop-linux-tutorial-get-started/selecthiveview.png "HDInsight Hive Viewer menu")</span><span class="sxs-lookup"><span data-stu-id="67061-237">![Selecting Ambari views](./media/apache-hadoop-linux-tutorial-get-started/selecthiveview.png "HDInsight Hive Viewer menu")</span></span>

4. <span data-ttu-id="67061-238">In the **QUERY** tab, paste the following HiveQL statements into the worksheet:</span><span class="sxs-lookup"><span data-stu-id="67061-238">In the **QUERY** tab, paste the following HiveQL statements into the worksheet:</span></span>
   
        SHOW TABLES;

    <span data-ttu-id="67061-239">![HDInsight Hive views](./media/apache-hadoop-linux-tutorial-get-started/hiveview-1.png "HDInsight Hive View Query Editor")</span><span class="sxs-lookup"><span data-stu-id="67061-239">![HDInsight Hive views](./media/apache-hadoop-linux-tutorial-get-started/hiveview-1.png "HDInsight Hive View Query Editor")</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="67061-240">Semi-colon is required by Hive.</span><span class="sxs-lookup"><span data-stu-id="67061-240">Semi-colon is required by Hive.</span></span>       
   > 
   > 

5. <span data-ttu-id="67061-241">Select **Execute**.</span><span class="sxs-lookup"><span data-stu-id="67061-241">Select **Execute**.</span></span> <span data-ttu-id="67061-242">A **RESULTS** tab appears beneath the **QUERY** tab and displays information about the job.</span><span class="sxs-lookup"><span data-stu-id="67061-242">A **RESULTS** tab appears beneath the **QUERY** tab and displays information about the job.</span></span> 
   
    <span data-ttu-id="67061-243">Once the query has finished, The **QUERY** tab displays the results of the operation.</span><span class="sxs-lookup"><span data-stu-id="67061-243">Once the query has finished, The **QUERY** tab displays the results of the operation.</span></span> <span data-ttu-id="67061-244">You shall see one table called **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="67061-244">You shall see one table called **hivesampletable**.</span></span> <span data-ttu-id="67061-245">This sample Hive table comes with all the HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="67061-245">This sample Hive table comes with all the HDInsight clusters.</span></span>
   
    <span data-ttu-id="67061-246">![HDInsight Hive views](./media/apache-hadoop-linux-tutorial-get-started/hiveview.png "HDInsight Hive View Query Editor")</span><span class="sxs-lookup"><span data-stu-id="67061-246">![HDInsight Hive views](./media/apache-hadoop-linux-tutorial-get-started/hiveview.png "HDInsight Hive View Query Editor")</span></span>

6. <span data-ttu-id="67061-247">Repeat step 4 and step 5 to run the following query:</span><span class="sxs-lookup"><span data-stu-id="67061-247">Repeat step 4 and step 5 to run the following query:</span></span>
   
        SELECT * FROM hivesampletable;
   
7. <span data-ttu-id="67061-248">You can also save the results of the query.</span><span class="sxs-lookup"><span data-stu-id="67061-248">You can also save the results of the query.</span></span> <span data-ttu-id="67061-249">Select the menu button on the right, and specify whether you want to download the results as a CSV file or store it to the storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="67061-249">Select the menu button on the right, and specify whether you want to download the results as a CSV file or store it to the storage account associated with the cluster.</span></span>

    <span data-ttu-id="67061-250">![Save result of Hive query](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-linux-hive-view-save-results.png "Save result of Hive query")</span><span class="sxs-lookup"><span data-stu-id="67061-250">![Save result of Hive query](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-linux-hive-view-save-results.png "Save result of Hive query")</span></span>

<span data-ttu-id="67061-251">After you have completed a Hive job, you can [export the results to Azure SQL database or SQL Server database](apache-hadoop-use-sqoop-mac-linux.md), you can also [visualize the results using Excel](apache-hadoop-connect-excel-power-query.md).</span><span class="sxs-lookup"><span data-stu-id="67061-251">After you have completed a Hive job, you can [export the results to Azure SQL database or SQL Server database](apache-hadoop-use-sqoop-mac-linux.md), you can also [visualize the results using Excel](apache-hadoop-connect-excel-power-query.md).</span></span> <span data-ttu-id="67061-252">For more information about using Hive in HDInsight, see [Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="67061-252">For more information about using Hive in HDInsight, see [Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file](hdinsight-use-hive.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="67061-253">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="67061-253">Troubleshoot</span></span>

<span data-ttu-id="67061-254">If you run into issues with creating HDInsight clusters, see [access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="67061-254">If you run into issues with creating HDInsight clusters, see [access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="67061-255">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="67061-255">Clean up resources</span></span>
<span data-ttu-id="67061-256">After you complete the article, you may want to delete the cluster.</span><span class="sxs-lookup"><span data-stu-id="67061-256">After you complete the article, you may want to delete the cluster.</span></span> <span data-ttu-id="67061-257">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="67061-257">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="67061-258">You are also charged for an HDInsight cluster, even when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="67061-258">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="67061-259">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span><span class="sxs-lookup"><span data-stu-id="67061-259">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> 

> [!NOTE]
> <span data-ttu-id="67061-260">If you are *immediately* proceeding to the next tutorial to learn how to run ETL operations using Hadoop on HDInsight, you may want to keep the cluster running.</span><span class="sxs-lookup"><span data-stu-id="67061-260">If you are *immediately* proceeding to the next tutorial to learn how to run ETL operations using Hadoop on HDInsight, you may want to keep the cluster running.</span></span> <span data-ttu-id="67061-261">This is becuase in the tutorial you have to create a Hadoop cluster again.</span><span class="sxs-lookup"><span data-stu-id="67061-261">This is becuase in the tutorial you have to create a Hadoop cluster again.</span></span> <span data-ttu-id="67061-262">However, if you are not going through the next tutorial right away, you must delete the cluster now.</span><span class="sxs-lookup"><span data-stu-id="67061-262">However, if you are not going through the next tutorial right away, you must delete the cluster now.</span></span>
> 
> 

<span data-ttu-id="67061-263">**To delete the cluster and/or the default storage account**</span><span class="sxs-lookup"><span data-stu-id="67061-263">**To delete the cluster and/or the default storage account**</span></span>

1. <span data-ttu-id="67061-264">Go back to the browser tab where you have the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="67061-264">Go back to the browser tab where you have the Azure portal.</span></span> <span data-ttu-id="67061-265">You shall be on the cluster overview page.</span><span class="sxs-lookup"><span data-stu-id="67061-265">You shall be on the cluster overview page.</span></span> <span data-ttu-id="67061-266">If you only want to delete the cluster but retain the default storage account, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="67061-266">If you only want to delete the cluster but retain the default storage account, select **Delete**.</span></span>

    <span data-ttu-id="67061-267">![HDInsight delete cluster](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-delete-cluster.png "Delete HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="67061-267">![HDInsight delete cluster](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-delete-cluster.png "Delete HDInsight cluster")</span></span>

2. <span data-ttu-id="67061-268">If you want to delete the cluster as well as the default storage account, select the resource group name (highlighted in the previous screenshot) to open the resource group page.</span><span class="sxs-lookup"><span data-stu-id="67061-268">If you want to delete the cluster as well as the default storage account, select the resource group name (highlighted in the previous screenshot) to open the resource group page.</span></span>

3. <span data-ttu-id="67061-269">Select **Delete resource group** to delete the resource group, which contains the cluster and the default storage account.</span><span class="sxs-lookup"><span data-stu-id="67061-269">Select **Delete resource group** to delete the resource group, which contains the cluster and the default storage account.</span></span> <span data-ttu-id="67061-270">Note deleting the resource group deletes the storage account.</span><span class="sxs-lookup"><span data-stu-id="67061-270">Note deleting the resource group deletes the storage account.</span></span> <span data-ttu-id="67061-271">If you want to keep the storage account, choose to delete the cluster only.</span><span class="sxs-lookup"><span data-stu-id="67061-271">If you want to keep the storage account, choose to delete the cluster only.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67061-272">Next steps</span><span class="sxs-lookup"><span data-stu-id="67061-272">Next steps</span></span>
<span data-ttu-id="67061-273">In this article, you learned how to create a Linux-based HDInsight cluster using a Resource Manager template, and how to perform basic Hive queries.</span><span class="sxs-lookup"><span data-stu-id="67061-273">In this article, you learned how to create a Linux-based HDInsight cluster using a Resource Manager template, and how to perform basic Hive queries.</span></span> <span data-ttu-id="67061-274">In the next article, you learn how to perform an extract, transform, and load (ETL) operation using Hadoop on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67061-274">In the next article, you learn how to perform an extract, transform, and load (ETL) operation using Hadoop on HDInsight.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="67061-275">Extract, transform, and load data using Apache Hive on HDInsight </span><span class="sxs-lookup"><span data-stu-id="67061-275">Extract, transform, and load data using Apache Hive on HDInsight </span></span>](../hdinsight-analyze-flight-delay-data-linux.md)

<span data-ttu-id="67061-276">If you're ready to start working with your own data and need to know more about how HDInsight stores data or how to get data into HDInsight, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="67061-276">If you're ready to start working with your own data and need to know more about how HDInsight stores data or how to get data into HDInsight, see the following articles:</span></span>

* <span data-ttu-id="67061-277">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](../hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="67061-277">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](../hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="67061-278">For information on how to create an HDInsight cluster with Data Lake Storage, see [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="67061-278">For information on how to create an HDInsight cluster with Data Lake Storage, see [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md)</span></span>
* <span data-ttu-id="67061-279">For information on how to upload data to HDInsight, see [Upload data to HDInsight](../hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="67061-279">For information on how to upload data to HDInsight, see [Upload data to HDInsight](../hdinsight-upload-data.md).</span></span>

<span data-ttu-id="67061-280">To learn more about analyzing data with HDInsight, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="67061-280">To learn more about analyzing data with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="67061-281">To learn more about using Hive with HDInsight, including how to perform Hive queries from Visual Studio, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="67061-281">To learn more about using Hive with HDInsight, including how to perform Hive queries from Visual Studio, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>
* <span data-ttu-id="67061-282">To learn about Pig, a language used to transform data, see [Use Pig with HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="67061-282">To learn about Pig, a language used to transform data, see [Use Pig with HDInsight](hdinsight-use-pig.md).</span></span>
* <span data-ttu-id="67061-283">To learn about MapReduce, a way to write programs that process data on Hadoop, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="67061-283">To learn about MapReduce, a way to write programs that process data on Hadoop, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>
* <span data-ttu-id="67061-284">To learn about using the HDInsight Tools for Visual Studio to analyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="67061-284">To learn about using the HDInsight Tools for Visual Studio to analyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](apache-hadoop-visual-studio-tools-get-started.md).</span></span>
* <span data-ttu-id="67061-285">To learn about using the HDInsight Tools for VSCode to analyze data on HDInsight, see [Use Azure HDInsight Tools for Visual Studio Code](../hdinsight-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="67061-285">To learn about using the HDInsight Tools for VSCode to analyze data on HDInsight, see [Use Azure HDInsight Tools for Visual Studio Code](../hdinsight-for-vscode.md).</span></span>


<span data-ttu-id="67061-286">If you'd like to learn more about creating or managing an HDInsight cluster, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="67061-286">If you'd like to learn more about creating or managing an HDInsight cluster, see the following articles:</span></span>

* <span data-ttu-id="67061-287">To learn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](../hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="67061-287">To learn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](../hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="67061-288">To learn more about the options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](../hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="67061-288">To learn more about the options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](../hdinsight-hadoop-provision-linux-clusters.md).</span></span>


[1]: ../HDInsight/apache-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


