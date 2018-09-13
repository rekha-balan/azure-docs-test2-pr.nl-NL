---
title: Submit jobs from R Tools for Visual Studio - Azure HDInsight
description: Submit R jobs from your local Visual Studio machine to an HDInsight cluster.
services: hdinsight
ms.service: hdinsight
author: maxluk
ms.author: maxluk
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 06/27/2018
ms.openlocfilehash: 65a0d8074b8dcf89d8fc713cb4b2272c6576e8fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871425"
---
# <a name="submit-jobs-from-r-tools-for-visual-studio"></a><span data-ttu-id="7687e-103">Submit jobs from R Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7687e-103">Submit jobs from R Tools for Visual Studio</span></span>

<span data-ttu-id="7687e-104">[R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) (RTVS) is a free, open-source extension for the Community (free), Professional, and Enterprise editions of both [Visual Studio 2017](https://www.visualstudio.com/downloads/), and [Visual Studio 2015 Update 3](http://go.microsoft.com/fwlink/?LinkId=691129) or higher.</span><span class="sxs-lookup"><span data-stu-id="7687e-104">[R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) (RTVS) is a free, open-source extension for the Community (free), Professional, and Enterprise editions of both [Visual Studio 2017](https://www.visualstudio.com/downloads/), and [Visual Studio 2015 Update 3](http://go.microsoft.com/fwlink/?LinkId=691129) or higher.</span></span>

<span data-ttu-id="7687e-105">RTVS enhances your R workflow by offering tools such as the [R Interactive window](https://docs.microsoft.com/visualstudio/rtvs/interactive-repl) (REPL), intellisense (code completion), [plot visualization](https://docs.microsoft.com/visualstudio/rtvs/visualizing-data) through R libraries such as ggplot2 and ggviz, [R code debugging](https://docs.microsoft.com/visualstudio/rtvs/debugging), and more.</span><span class="sxs-lookup"><span data-stu-id="7687e-105">RTVS enhances your R workflow by offering tools such as the [R Interactive window](https://docs.microsoft.com/visualstudio/rtvs/interactive-repl) (REPL), intellisense (code completion), [plot visualization](https://docs.microsoft.com/visualstudio/rtvs/visualizing-data) through R libraries such as ggplot2 and ggviz, [R code debugging](https://docs.microsoft.com/visualstudio/rtvs/debugging), and more.</span></span>

## <a name="set-up-your-environment"></a><span data-ttu-id="7687e-106">Set up your environment</span><span class="sxs-lookup"><span data-stu-id="7687e-106">Set up your environment</span></span>

1. <span data-ttu-id="7687e-107">Install [R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).</span><span class="sxs-lookup"><span data-stu-id="7687e-107">Install [R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).</span></span>

    ![Installing RTVS in Visual Studio 2017](./media/r-server-submit-jobs-r-tools-vs/install-r-tools-for-vs.png)

2. <span data-ttu-id="7687e-109">Select the *Data science and analytical applications* workload, then select the **R language support**, **Runtime support for R development**, and **Microsoft R Client** options.</span><span class="sxs-lookup"><span data-stu-id="7687e-109">Select the *Data science and analytical applications* workload, then select the **R language support**, **Runtime support for R development**, and **Microsoft R Client** options.</span></span>

3. <span data-ttu-id="7687e-110">You need to have public and private keys for SSH authentication.</span><span class="sxs-lookup"><span data-stu-id="7687e-110">You need to have public and private keys for SSH authentication.</span></span>
<!-- {TODO tbd, no such file yet}[use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-windows.md) -->

4. <span data-ttu-id="7687e-111">Install [ML Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) on your machine.</span><span class="sxs-lookup"><span data-stu-id="7687e-111">Install [ML Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) on your machine.</span></span> <span data-ttu-id="7687e-112">ML Server provides the [`RevoScaleR`](https://msdn.microsoft.com/microsoft-r/scaler/scaler) and `RxSpark` functions.</span><span class="sxs-lookup"><span data-stu-id="7687e-112">ML Server provides the [`RevoScaleR`](https://msdn.microsoft.com/microsoft-r/scaler/scaler) and `RxSpark` functions.</span></span>

5. <span data-ttu-id="7687e-113">Install [PuTTY](http://www.putty.org/) to provide a compute context to run `RevoScaleR` functions from your local client to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7687e-113">Install [PuTTY](http://www.putty.org/) to provide a compute context to run `RevoScaleR` functions from your local client to your HDInsight cluster.</span></span>

6. <span data-ttu-id="7687e-114">You have the option to apply the Data Science Settings to your Visual Studio environment, which provides a new layout for your workspace for the R tools.</span><span class="sxs-lookup"><span data-stu-id="7687e-114">You have the option to apply the Data Science Settings to your Visual Studio environment, which provides a new layout for your workspace for the R tools.</span></span>
    1. <span data-ttu-id="7687e-115">To save your current Visual Studio settings, use the **Tools > Import and Export Settings** command, then select **Export selected environment settings** and specify a file name.</span><span class="sxs-lookup"><span data-stu-id="7687e-115">To save your current Visual Studio settings, use the **Tools > Import and Export Settings** command, then select **Export selected environment settings** and specify a file name.</span></span> <span data-ttu-id="7687e-116">To restore those settings, use the same command and select **Import selected environment settings**.</span><span class="sxs-lookup"><span data-stu-id="7687e-116">To restore those settings, use the same command and select **Import selected environment settings**.</span></span>

    2. <span data-ttu-id="7687e-117">Go to the **R Tools** menu item, then select **Data Science Settings...**.</span><span class="sxs-lookup"><span data-stu-id="7687e-117">Go to the **R Tools** menu item, then select **Data Science Settings...**.</span></span>

        ![Data Science Settings...](./media/r-server-submit-jobs-r-tools-vs/data-science-settings.png)

    > [!NOTE]
    > <span data-ttu-id="7687e-119">Using the approach in step 1, you can also save and restore your personalized data scientist layout, rather than repeating the **Data Science Settings** command.</span><span class="sxs-lookup"><span data-stu-id="7687e-119">Using the approach in step 1, you can also save and restore your personalized data scientist layout, rather than repeating the **Data Science Settings** command.</span></span>

## <a name="execute-local-r-methods"></a><span data-ttu-id="7687e-120">Execute local R methods</span><span class="sxs-lookup"><span data-stu-id="7687e-120">Execute local R methods</span></span>

1. <span data-ttu-id="7687e-121">Create your [HDInsight ML Services cluster](r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7687e-121">Create your [HDInsight ML Services cluster](r-server-get-started.md).</span></span>
2. <span data-ttu-id="7687e-122">Install the [RTVS extension](https://docs.microsoft.com/visualstudio/rtvs/installation).</span><span class="sxs-lookup"><span data-stu-id="7687e-122">Install the [RTVS extension](https://docs.microsoft.com/visualstudio/rtvs/installation).</span></span>
3. <span data-ttu-id="7687e-123">Download the [samples zip file](https://github.com/Microsoft/RTVS-docs/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="7687e-123">Download the [samples zip file](https://github.com/Microsoft/RTVS-docs/archive/master.zip).</span></span>
4. <span data-ttu-id="7687e-124">Open `examples/Examples.sln` to launch the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7687e-124">Open `examples/Examples.sln` to launch the solution in Visual Studio.</span></span>
5. <span data-ttu-id="7687e-125">Open the `1-Getting Started with R.R` file in the `A first look at R` solution folder.</span><span class="sxs-lookup"><span data-stu-id="7687e-125">Open the `1-Getting Started with R.R` file in the `A first look at R` solution folder.</span></span>
6. <span data-ttu-id="7687e-126">Starting at the top of the file, press Ctrl+Enter to send each line, one at a time, to the R Interactive window.</span><span class="sxs-lookup"><span data-stu-id="7687e-126">Starting at the top of the file, press Ctrl+Enter to send each line, one at a time, to the R Interactive window.</span></span> <span data-ttu-id="7687e-127">Some lines might take a while as they install packages.</span><span class="sxs-lookup"><span data-stu-id="7687e-127">Some lines might take a while as they install packages.</span></span>
    * <span data-ttu-id="7687e-128">Alternatively, you can select all lines in the R file (Ctrl+A), then either execute all (Ctrl+Enter), or select the Execute Interactive icon on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="7687e-128">Alternatively, you can select all lines in the R file (Ctrl+A), then either execute all (Ctrl+Enter), or select the Execute Interactive icon on the toolbar.</span></span>
        <span data-ttu-id="7687e-129">![Execute interactive](./media/r-server-submit-jobs-r-tools-vs/execute-interactive.png)</span><span class="sxs-lookup"><span data-stu-id="7687e-129">![Execute interactive](./media/r-server-submit-jobs-r-tools-vs/execute-interactive.png)</span></span>

7. <span data-ttu-id="7687e-130">After running all the lines in the script, you should see an output similar to this:</span><span class="sxs-lookup"><span data-stu-id="7687e-130">After running all the lines in the script, you should see an output similar to this:</span></span>

    ![Data Science Settings...](./media/r-server-submit-jobs-r-tools-vs/workspace.png)

## <a name="submit-jobs-to-an-hdinsight-ml-services-cluster"></a><span data-ttu-id="7687e-132">Submit jobs to an HDInsight ML Services cluster</span><span class="sxs-lookup"><span data-stu-id="7687e-132">Submit jobs to an HDInsight ML Services cluster</span></span>

<span data-ttu-id="7687e-133">Using a Microsoft ML Server/Microsoft R Client from a Windows computer equipped with PuTTY, you can create a compute context that will run distributed `RevoScaleR` functions from your local client to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7687e-133">Using a Microsoft ML Server/Microsoft R Client from a Windows computer equipped with PuTTY, you can create a compute context that will run distributed `RevoScaleR` functions from your local client to your HDInsight cluster.</span></span> <span data-ttu-id="7687e-134">Use `RxSpark` to create the compute context, specifying your username, the Hadoop cluster's edge node, SSH switches, and so forth.</span><span class="sxs-lookup"><span data-stu-id="7687e-134">Use `RxSpark` to create the compute context, specifying your username, the Hadoop cluster's edge node, SSH switches, and so forth.</span></span>

1. <span data-ttu-id="7687e-135">To find your edge node's host name, open your HDInsight ML Services cluster pane on Azure, then select **Secure Shell (SSH)** on the top menu of the Overview pane.</span><span class="sxs-lookup"><span data-stu-id="7687e-135">To find your edge node's host name, open your HDInsight ML Services cluster pane on Azure, then select **Secure Shell (SSH)** on the top menu of the Overview pane.</span></span>

    ![Secure Shell (SSH)](./media/r-server-submit-jobs-r-tools-vs/ssh.png)

2. <span data-ttu-id="7687e-137">Copy the **Edge node host name** value.</span><span class="sxs-lookup"><span data-stu-id="7687e-137">Copy the **Edge node host name** value.</span></span>

    ![Edge node host name](./media/r-server-submit-jobs-r-tools-vs/edge-node.png)

3. <span data-ttu-id="7687e-139">Paste the following code into the R Interactive window in Visual Studio, altering the values of the setup variables to match your environment.</span><span class="sxs-lookup"><span data-stu-id="7687e-139">Paste the following code into the R Interactive window in Visual Studio, altering the values of the setup variables to match your environment.</span></span>

    ```R
    # Setup variables that connect the compute context to your HDInsight cluster
    mySshHostname <- 'r-cluster-ed-ssh.azurehdinsight.net ' # HDI secure shell hostname
    mySshUsername <- 'sshuser' # HDI SSH username
    mySshClientDir <- "C:\\Program Files (x86)\\PuTTY"
    mySshSwitches <- '-i C:\\Users\\azureuser\\r.ppk' # Path to your private ssh key
    myHdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep = "/")
    myShareDir <- paste("/var/RevoShare", mySshUsername, sep = "/")
    mySshProfileScript <- "/usr/lib64/microsoft-r/3.3/hadoop/RevoHadoopEnvVars.site"

    # Create the Spark Cluster compute context
    mySparkCluster <- RxSpark(
          sshUsername = mySshUsername,
      sshHostname = mySshHostname,
      sshSwitches = mySshSwitches,
      sshProfileScript = mySshProfileScript,
      consoleOutput = TRUE,
      hdfsShareDir = myHdfsShareDir,
      shareDir = myShareDir,
      sshClientDir = mySshClientDir
    )
    
    # Set the current compute context as the Spark compute context defined above
    rxSetComputeContext(mySparkCluster)
    ```
    
    ![Setting the Spark context](./media/r-server-submit-jobs-r-tools-vs/spark-context.png)

4. <span data-ttu-id="7687e-141">Execute the following commands in the R Interactive window:</span><span class="sxs-lookup"><span data-stu-id="7687e-141">Execute the following commands in the R Interactive window:</span></span>

    ```R
    rxHadoopCommand("version") # should return version information
    rxHadoopMakeDir("/user/RevoShare/newUser") # creates a new folder in your storage account
    rxHadoopCopy("/example/data/people.json", "/user/RevoShare/newUser") # copies file to new folder
    ```

    <span data-ttu-id="7687e-142">You should see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="7687e-142">You should see an output similar to the following:</span></span>

    ![Successful rx command execution](./media/r-server-submit-jobs-r-tools-vs/rx-commands.png)

5. <span data-ttu-id="7687e-144">Verify that the `rxHadoopCopy` successfully copied the `people.json` file from the example data folder to the newly created `/user/RevoShare/newUser` folder:</span><span class="sxs-lookup"><span data-stu-id="7687e-144">Verify that the `rxHadoopCopy` successfully copied the `people.json` file from the example data folder to the newly created `/user/RevoShare/newUser` folder:</span></span>

    1. <span data-ttu-id="7687e-145">From your HDInsight ML Services cluster pane in Azure, select **Storage accounts** from the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="7687e-145">From your HDInsight ML Services cluster pane in Azure, select **Storage accounts** from the left-hand menu.</span></span>

        ![Storage accounts](./media/r-server-submit-jobs-r-tools-vs/storage-accounts.png)

    2. <span data-ttu-id="7687e-147">Select the default storage account for your cluster, making note of the container/directory name.</span><span class="sxs-lookup"><span data-stu-id="7687e-147">Select the default storage account for your cluster, making note of the container/directory name.</span></span>

    3. <span data-ttu-id="7687e-148">Select **Containers** from the left-hand menu on your storage account pane.</span><span class="sxs-lookup"><span data-stu-id="7687e-148">Select **Containers** from the left-hand menu on your storage account pane.</span></span>

        ![Containers](./media/r-server-submit-jobs-r-tools-vs/containers.png)

    4. <span data-ttu-id="7687e-150">Select your cluster's container name, browse to the **user** folder (you might have to click *Load more* at the bottom of the list), then select *RevoShare*, then **newUser**.</span><span class="sxs-lookup"><span data-stu-id="7687e-150">Select your cluster's container name, browse to the **user** folder (you might have to click *Load more* at the bottom of the list), then select *RevoShare*, then **newUser**.</span></span> <span data-ttu-id="7687e-151">The `people.json` file should be displayed in the `newUser` folder.</span><span class="sxs-lookup"><span data-stu-id="7687e-151">The `people.json` file should be displayed in the `newUser` folder.</span></span>

        ![Copied file](./media/r-server-submit-jobs-r-tools-vs/copied-file.png)

6. <span data-ttu-id="7687e-153">After you are finished using the current Spark context, you must stop it.</span><span class="sxs-lookup"><span data-stu-id="7687e-153">After you are finished using the current Spark context, you must stop it.</span></span> <span data-ttu-id="7687e-154">You cannot run multiple contexts at once.</span><span class="sxs-lookup"><span data-stu-id="7687e-154">You cannot run multiple contexts at once.</span></span>

    ```R
    rxStopEngine(mySparkCluster)
    ```

## <a name="next-steps"></a><span data-ttu-id="7687e-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="7687e-155">Next steps</span></span>

* [<span data-ttu-id="7687e-156">Compute context options for ML Services on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7687e-156">Compute context options for ML Services on HDInsight</span></span>](r-server-compute-contexts.md)
* <span data-ttu-id="7687e-157">[Combining ScaleR and SparkR](../hdinsight-hadoop-r-scaler-sparkr.md) provides an example of airline flight delay predictions.</span><span class="sxs-lookup"><span data-stu-id="7687e-157">[Combining ScaleR and SparkR](../hdinsight-hadoop-r-scaler-sparkr.md) provides an example of airline flight delay predictions.</span></span>
<!-- * You can also submit R jobs with the [R Studio Server](hdinsight-submit-jobs-from-r-studio-server.md) -->
