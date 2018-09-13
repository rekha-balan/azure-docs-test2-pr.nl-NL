---
title: Manage ML Services cluster on HDInsight - Azure
description: Learn how to manage an ML Services cluster in Azure HDInsight.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 06/27/2018
ms.openlocfilehash: 38a8366a586b032c3b11cbef8ee5f01ad2b822a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866348"
---
# <a name="manage-ml-services-cluster-on-azure-hdinsight"></a><span data-ttu-id="523f6-103">Manage ML Services cluster on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="523f6-103">Manage ML Services cluster on Azure HDInsight</span></span>

<span data-ttu-id="523f6-104">In this article, you learn how to manage an existing ML Services cluster on Azure HDInsight to perform tasks like adding mulitiple concurrent users, connecting remotely to an ML Services cluster, changing compute context, etc.</span><span class="sxs-lookup"><span data-stu-id="523f6-104">In this article, you learn how to manage an existing ML Services cluster on Azure HDInsight to perform tasks like adding mulitiple concurrent users, connecting remotely to an ML Services cluster, changing compute context, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="523f6-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="523f6-105">Prerequisites</span></span>

* <span data-ttu-id="523f6-106">**An ML Services cluster on HDInsight**: For instructions, see [Get started with ML Services on HDInsight](r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="523f6-106">**An ML Services cluster on HDInsight**: For instructions, see [Get started with ML Services on HDInsight](r-server-get-started.md).</span></span>

* <span data-ttu-id="523f6-107">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span><span class="sxs-lookup"><span data-stu-id="523f6-107">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span></span> <span data-ttu-id="523f6-108">For more information, see [Use SSH with HDInsight.](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="523f6-108">For more information, see [Use SSH with HDInsight.](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="523f6-109">Enable multiple concurrent users</span><span class="sxs-lookup"><span data-stu-id="523f6-109">Enable multiple concurrent users</span></span>

<span data-ttu-id="523f6-110">You can enable multiple concurrent users for ML Services cluster on HDInsight by adding more users for the edge node on which the RStudio community version runs.</span><span class="sxs-lookup"><span data-stu-id="523f6-110">You can enable multiple concurrent users for ML Services cluster on HDInsight by adding more users for the edge node on which the RStudio community version runs.</span></span> <span data-ttu-id="523f6-111">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span><span class="sxs-lookup"><span data-stu-id="523f6-111">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Concurrent user 1](./media/r-server-hdinsight-manage/concurrent-users-1.png)

- <span data-ttu-id="523f6-113">**Cluster login username**: an HTTP user for authentication through the HDInsight gateway that is used to protect the HDInsight clusters you created.</span><span class="sxs-lookup"><span data-stu-id="523f6-113">**Cluster login username**: an HTTP user for authentication through the HDInsight gateway that is used to protect the HDInsight clusters you created.</span></span> <span data-ttu-id="523f6-114">This HTTP user is used to access the Ambari UI, YARN UI, as well as other UI components.</span><span class="sxs-lookup"><span data-stu-id="523f6-114">This HTTP user is used to access the Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="523f6-115">**Secure Shell (SSH) username**: an SSH user to access the cluster through secure shell.</span><span class="sxs-lookup"><span data-stu-id="523f6-115">**Secure Shell (SSH) username**: an SSH user to access the cluster through secure shell.</span></span> <span data-ttu-id="523f6-116">This user is a user in the Linux system for all the head nodes, worker nodes, and edge nodes.</span><span class="sxs-lookup"><span data-stu-id="523f6-116">This user is a user in the Linux system for all the head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="523f6-117">So you can use secure shell to access any of the nodes in a remote cluster.</span><span class="sxs-lookup"><span data-stu-id="523f6-117">So you can use secure shell to access any of the nodes in a remote cluster.</span></span>

<span data-ttu-id="523f6-118">The R Studio Server Community version used in the ML Services cluster on HDInsight accepts only Linux username and password as a sign in mechanism.</span><span class="sxs-lookup"><span data-stu-id="523f6-118">The R Studio Server Community version used in the ML Services cluster on HDInsight accepts only Linux username and password as a sign in mechanism.</span></span> <span data-ttu-id="523f6-119">It does not support passing tokens.</span><span class="sxs-lookup"><span data-stu-id="523f6-119">It does not support passing tokens.</span></span> <span data-ttu-id="523f6-120">So, when you try to access R Studio for the first time on an ML Services cluster, you need to sign in twice.</span><span class="sxs-lookup"><span data-stu-id="523f6-120">So, when you try to access R Studio for the first time on an ML Services cluster, you need to sign in twice.</span></span>

- <span data-ttu-id="523f6-121">First sign in using the HTTP user credentials through the HDInsight Gateway.</span><span class="sxs-lookup"><span data-stu-id="523f6-121">First sign in using the HTTP user credentials through the HDInsight Gateway.</span></span> 

- <span data-ttu-id="523f6-122">Then use the SSH user credentials to sign in to RStudio.</span><span class="sxs-lookup"><span data-stu-id="523f6-122">Then use the SSH user credentials to sign in to RStudio.</span></span>
  
<span data-ttu-id="523f6-123">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="523f6-123">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="523f6-124">So to enable multiple users to access ML Services cluster on HDInsight, you must create additional users in the Linux system.</span><span class="sxs-lookup"><span data-stu-id="523f6-124">So to enable multiple users to access ML Services cluster on HDInsight, you must create additional users in the Linux system.</span></span>

<span data-ttu-id="523f6-125">Because RStudio runs on the cluster’s edge node, there are several steps here:</span><span class="sxs-lookup"><span data-stu-id="523f6-125">Because RStudio runs on the cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="523f6-126">Use the existing SSH user to sign in to the edge node</span><span class="sxs-lookup"><span data-stu-id="523f6-126">Use the existing SSH user to sign in to the edge node</span></span>
2. <span data-ttu-id="523f6-127">Add more Linux users in edge node</span><span class="sxs-lookup"><span data-stu-id="523f6-127">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="523f6-128">Use RStudio Community version with the user created</span><span class="sxs-lookup"><span data-stu-id="523f6-128">Use RStudio Community version with the user created</span></span>

### <a name="step-1-use-the-created-ssh-user-to-sign-in-to-the-edge-node"></a><span data-ttu-id="523f6-129">Step 1: Use the created SSH user to sign in to the edge node</span><span class="sxs-lookup"><span data-stu-id="523f6-129">Step 1: Use the created SSH user to sign in to the edge node</span></span>

<span data-ttu-id="523f6-130">Follow the instructions at [Connect to HDInsight (Hadoop) using SSH](../hdinsight-hadoop-linux-use-ssh-unix.md) to access the edge node.</span><span class="sxs-lookup"><span data-stu-id="523f6-130">Follow the instructions at [Connect to HDInsight (Hadoop) using SSH](../hdinsight-hadoop-linux-use-ssh-unix.md) to access the edge node.</span></span> <span data-ttu-id="523f6-131">The edge node address for ML Services cluster on HDInsight is `CLUSTERNAME-ed-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="523f6-131">The edge node address for ML Services cluster on HDInsight is `CLUSTERNAME-ed-ssh.azurehdinsight.net`.</span></span>

### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="523f6-132">Step 2: Add more Linux users in edge node</span><span class="sxs-lookup"><span data-stu-id="523f6-132">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="523f6-133">To add a user to the edge node, execute the commands:</span><span class="sxs-lookup"><span data-stu-id="523f6-133">To add a user to the edge node, execute the commands:</span></span>

    # Add a user 
    sudo useradd <yournewusername> -m

    # Set password for the new user
    sudo passwd <yournewusername>

<span data-ttu-id="523f6-134">The following screenshot shows the outputs.</span><span class="sxs-lookup"><span data-stu-id="523f6-134">The following screenshot shows the outputs.</span></span>

![Concurrent user 3](./media/r-server-hdinsight-manage/concurrent-users-2.png)

<span data-ttu-id="523f6-136">When prompted for "Current Kerberos password:", just press **Enter** to ignore it.</span><span class="sxs-lookup"><span data-stu-id="523f6-136">When prompted for "Current Kerberos password:", just press **Enter** to ignore it.</span></span> <span data-ttu-id="523f6-137">The `-m` option in `useradd` command indicates that the system will create a home folder for the user, which is required for RStudio Community version.</span><span class="sxs-lookup"><span data-stu-id="523f6-137">The `-m` option in `useradd` command indicates that the system will create a home folder for the user, which is required for RStudio Community version.</span></span>

### <a name="step-3-use-rstudio-community-version-with-the-user-created"></a><span data-ttu-id="523f6-138">Step 3: Use RStudio Community version with the user created</span><span class="sxs-lookup"><span data-stu-id="523f6-138">Step 3: Use RStudio Community version with the user created</span></span>

<span data-ttu-id="523f6-139">Access RStudio from https://CLUSTERNAME.azurehdinsight.net/rstudio/.</span><span class="sxs-lookup"><span data-stu-id="523f6-139">Access RStudio from https://CLUSTERNAME.azurehdinsight.net/rstudio/.</span></span> <span data-ttu-id="523f6-140">If you are logging in for the first time after creating the cluster, enter the cluster admin credentials followed by the SSH user credentials you created.</span><span class="sxs-lookup"><span data-stu-id="523f6-140">If you are logging in for the first time after creating the cluster, enter the cluster admin credentials followed by the SSH user credentials you created.</span></span> <span data-ttu-id="523f6-141">If this is not your first login, only enter the credentials for the SSH user you created.</span><span class="sxs-lookup"><span data-stu-id="523f6-141">If this is not your first login, only enter the credentials for the SSH user you created.</span></span>

<span data-ttu-id="523f6-142">You can also sign in using the original credentials (by default, it is *sshuser*) concurrently from another browser window.</span><span class="sxs-lookup"><span data-stu-id="523f6-142">You can also sign in using the original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="523f6-143">Note also that the newly added users do not have root privileges in Linux system, but they do have the same access to all the files in the remote HDFS and WASB storage.</span><span class="sxs-lookup"><span data-stu-id="523f6-143">Note also that the newly added users do not have root privileges in Linux system, but they do have the same access to all the files in the remote HDFS and WASB storage.</span></span>

## <a name="connect-remotely-to-microsoft-ml-services"></a><span data-ttu-id="523f6-144">Connect remotely to Microsoft ML Services</span><span class="sxs-lookup"><span data-stu-id="523f6-144">Connect remotely to Microsoft ML Services</span></span>

<span data-ttu-id="523f6-145">You can set up access to the HDInsight Hadoop Spark compute context from a remote instance of ML Client running on your desktop.</span><span class="sxs-lookup"><span data-stu-id="523f6-145">You can set up access to the HDInsight Hadoop Spark compute context from a remote instance of ML Client running on your desktop.</span></span> <span data-ttu-id="523f6-146">To do so, you must specify the options (hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript) when defining the RxSpark compute context on your desktop: For example:</span><span class="sxs-lookup"><span data-stu-id="523f6-146">To do so, you must specify the options (hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript) when defining the RxSpark compute context on your desktop: For example:</span></span>

    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- '<clustername>-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- '<sshuser>'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )

<span data-ttu-id="523f6-147">For more information, see the "Using Microsoft Machine Learning Server as a Hadoop Client" section in [How to use RevoScaleR in a Spark compute context](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-spark#more-spark-scenarios)</span><span class="sxs-lookup"><span data-stu-id="523f6-147">For more information, see the "Using Microsoft Machine Learning Server as a Hadoop Client" section in [How to use RevoScaleR in a Spark compute context](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-spark#more-spark-scenarios)</span></span>

## <a name="use-a-compute-context"></a><span data-ttu-id="523f6-148">Use a compute context</span><span class="sxs-lookup"><span data-stu-id="523f6-148">Use a compute context</span></span>

<span data-ttu-id="523f6-149">A compute context allows you to control whether computation is performed locally on the edge node or distributed across the nodes in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="523f6-149">A compute context allows you to control whether computation is performed locally on the edge node or distributed across the nodes in the HDInsight cluster.</span></span>

1. <span data-ttu-id="523f6-150">From RStudio Server or the R console (in an SSH session), use the following code to load example data into the default storage for HDInsight:</span><span class="sxs-lookup"><span data-stu-id="523f6-150">From RStudio Server or the R console (in an SSH session), use the following code to load example data into the default storage for HDInsight:</span></span>

        # Set the HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data to the tmp folder
        remoteDir <- "https://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot to load the data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make the directory
        rxHadoopMakeDir(inputDir)

        # Copy the data from source to input
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="523f6-151">Next, create some data info and define two data sources.</span><span class="sxs-lookup"><span data-stu-id="523f6-151">Next, create some data info and define two data sources.</span></span>

        # Define the HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for the airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all the column names
        varNames <- names(airlineColInfo)

        # Define the text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define the text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula to use
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="523f6-152">Run a logistic regression over the data using the local compute context.</span><span class="sxs-lookup"><span data-stu-id="523f6-152">Run a logistic regression over the data using the local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="523f6-153">You should see output that ends with lines similar to the following snippet:</span><span class="sxs-lookup"><span data-stu-id="523f6-153">You should see output that ends with lines similar to the following snippet:</span></span>

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. <span data-ttu-id="523f6-154">Run the same logistic regression using the Spark context.</span><span class="sxs-lookup"><span data-stu-id="523f6-154">Run the same logistic regression using the Spark context.</span></span> <span data-ttu-id="523f6-155">The Spark context distributes the processing over all the worker nodes in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="523f6-155">The Spark context distributes the processing over all the worker nodes in the HDInsight cluster.</span></span>

        # Define the Spark compute context
        mySparkCluster <- RxSpark()

        # Set the compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )

        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="523f6-156">You can also use MapReduce to distribute computation across cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="523f6-156">You can also use MapReduce to distribute computation across cluster nodes.</span></span> <span data-ttu-id="523f6-157">For more information on compute context, see [Compute context options for ML Services cluster on HDInsight](r-server-compute-contexts.md).</span><span class="sxs-lookup"><span data-stu-id="523f6-157">For more information on compute context, see [Compute context options for ML Services cluster on HDInsight](r-server-compute-contexts.md).</span></span>

## <a name="distribute-r-code-to-multiple-nodes"></a><span data-ttu-id="523f6-158">Distribute R code to multiple nodes</span><span class="sxs-lookup"><span data-stu-id="523f6-158">Distribute R code to multiple nodes</span></span>

<span data-ttu-id="523f6-159">With ML Services on HDInsight, you can take existing R code and run it across multiple nodes in the cluster by using `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="523f6-159">With ML Services on HDInsight, you can take existing R code and run it across multiple nodes in the cluster by using `rxExec`.</span></span> <span data-ttu-id="523f6-160">This function is useful when doing a parameter sweep or simulations.</span><span class="sxs-lookup"><span data-stu-id="523f6-160">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="523f6-161">The following code is an example of how to use `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="523f6-161">The following code is an example of how to use `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="523f6-162">If you are still using the Spark or MapReduce context, this  command returns the nodename value for the worker nodes that the code `(Sys.info()["nodename"])` is run on.</span><span class="sxs-lookup"><span data-stu-id="523f6-162">If you are still using the Spark or MapReduce context, this  command returns the nodename value for the worker nodes that the code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="523f6-163">For example, on a four node cluster, you expect to receive output similar to the following snippet:</span><span class="sxs-lookup"><span data-stu-id="523f6-163">For example, on a four node cluster, you expect to receive output similar to the following snippet:</span></span>

    $rxElem1
        nodename
    "wn3-mymlser"

    $rxElem2
        nodename
    "wn0-mymlser"

    $rxElem3
        nodename
    "wn3-mymlser"

    $rxElem4
        nodename
    "wn3-mymlser"

## <a name="access-data-in-hive-and-parquet"></a><span data-ttu-id="523f6-164">Access data in Hive and Parquet</span><span class="sxs-lookup"><span data-stu-id="523f6-164">Access data in Hive and Parquet</span></span>

<span data-ttu-id="523f6-165">HDInsight ML Services allows direct access to data in Hive and Parquet for use by ScaleR functions in the Spark compute context.</span><span class="sxs-lookup"><span data-stu-id="523f6-165">HDInsight ML Services allows direct access to data in Hive and Parquet for use by ScaleR functions in the Spark compute context.</span></span> <span data-ttu-id="523f6-166">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL to load data directly into a Spark DataFrame for analysis by ScaleR.</span><span class="sxs-lookup"><span data-stu-id="523f6-166">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL to load data directly into a Spark DataFrame for analysis by ScaleR.</span></span>

<span data-ttu-id="523f6-167">The following code provides some sample code on use of the new functions:</span><span class="sxs-lookup"><span data-stu-id="523f6-167">The following code provides some sample code on use of the new functions:</span></span>

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close the Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="523f6-168">For additional info on use of these new functions see the online help in ML Services through use of the `?RxHivedata` and `?RxParquetData` commands.</span><span class="sxs-lookup"><span data-stu-id="523f6-168">For additional info on use of these new functions see the online help in ML Services through use of the `?RxHivedata` and `?RxParquetData` commands.</span></span>  

## <a name="install-additional-r-packages-on-the-cluster"></a><span data-ttu-id="523f6-169">Install additional R packages on the cluster</span><span class="sxs-lookup"><span data-stu-id="523f6-169">Install additional R packages on the cluster</span></span>

### <a name="to-install-r-packages-on-the-edge-node"></a><span data-ttu-id="523f6-170">To install R packages on the edge node</span><span class="sxs-lookup"><span data-stu-id="523f6-170">To install R packages on the edge node</span></span>

<span data-ttu-id="523f6-171">If you want to install additional R packages on the edge node, you can use `install.packages()` directly from within the R console, once connected to the edge node through SSH.</span><span class="sxs-lookup"><span data-stu-id="523f6-171">If you want to install additional R packages on the edge node, you can use `install.packages()` directly from within the R console, once connected to the edge node through SSH.</span></span> 

### <a name="to-install-r-packages-on-the-worker-node"></a><span data-ttu-id="523f6-172">To install R packages on the worker node</span><span class="sxs-lookup"><span data-stu-id="523f6-172">To install R packages on the worker node</span></span>

<span data-ttu-id="523f6-173">To install R packages on the worker nodes of the cluster, you must use a Script Action.</span><span class="sxs-lookup"><span data-stu-id="523f6-173">To install R packages on the worker nodes of the cluster, you must use a Script Action.</span></span> <span data-ttu-id="523f6-174">Script Actions are Bash scripts that are used to make configuration changes to the HDInsight cluster or to install additional software, such as additional R packages.</span><span class="sxs-lookup"><span data-stu-id="523f6-174">Script Actions are Bash scripts that are used to make configuration changes to the HDInsight cluster or to install additional software, such as additional R packages.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="523f6-175">Using Script Actions to install additional R packages can only be used after the cluster has been created.</span><span class="sxs-lookup"><span data-stu-id="523f6-175">Using Script Actions to install additional R packages can only be used after the cluster has been created.</span></span> <span data-ttu-id="523f6-176">Do not use this procedure during cluster creation, as the script relies on ML Services being completely configured.</span><span class="sxs-lookup"><span data-stu-id="523f6-176">Do not use this procedure during cluster creation, as the script relies on ML Services being completely configured.</span></span>
>
>

1. <span data-ttu-id="523f6-177">Follow the steps at [Customize clusters using Script Action](../hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="523f6-177">Follow the steps at [Customize clusters using Script Action](../hdinsight-hadoop-customize-cluster-linux.md).</span></span>

3. <span data-ttu-id="523f6-178">For **Submit script action**, provide the following information:</span><span class="sxs-lookup"><span data-stu-id="523f6-178">For **Submit script action**, provide the following information:</span></span>

   * <span data-ttu-id="523f6-179">For **Script type**, select **Custom**.</span><span class="sxs-lookup"><span data-stu-id="523f6-179">For **Script type**, select **Custom**.</span></span>

   * <span data-ttu-id="523f6-180">For **Name**, provide a name for the script action.</span><span class="sxs-lookup"><span data-stu-id="523f6-180">For **Name**, provide a name for the script action.</span></span>

    * <span data-ttu-id="523f6-181">For **Bash script URI**, enter  `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`.</span><span class="sxs-lookup"><span data-stu-id="523f6-181">For **Bash script URI**, enter  `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`.</span></span> <span data-ttu-id="523f6-182">This is the script that installs additional R packages on the worker node</span><span class="sxs-lookup"><span data-stu-id="523f6-182">This is the script that installs additional R packages on the worker node</span></span>

   * <span data-ttu-id="523f6-183">Select the check box only for **Worker**.</span><span class="sxs-lookup"><span data-stu-id="523f6-183">Select the check box only for **Worker**.</span></span>

   * <span data-ttu-id="523f6-184">**Parameters**: The R packages to be installed.</span><span class="sxs-lookup"><span data-stu-id="523f6-184">**Parameters**: The R packages to be installed.</span></span> <span data-ttu-id="523f6-185">For example, `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="523f6-185">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="523f6-186">Select the check box to **Persist this script action**.</span><span class="sxs-lookup"><span data-stu-id="523f6-186">Select the check box to **Persist this script action**.</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="523f6-187">By default, all R packages are installed from a snapshot of the Microsoft MRAN repository consistent with the version of ML Server that has been installed.</span><span class="sxs-lookup"><span data-stu-id="523f6-187">By default, all R packages are installed from a snapshot of the Microsoft MRAN repository consistent with the version of ML Server that has been installed.</span></span> <span data-ttu-id="523f6-188">If you want to install newer versions of packages, then there is some risk of incompatibility.</span><span class="sxs-lookup"><span data-stu-id="523f6-188">If you want to install newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="523f6-189">However this kind of install is possible by specifying `useCRAN` as the first element of the package list, for example `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="523f6-189">However this kind of install is possible by specifying `useCRAN` as the first element of the package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="523f6-190">Some R packages require additional Linux system libraries.</span><span class="sxs-lookup"><span data-stu-id="523f6-190">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="523f6-191">For convenience, the HDInsight ML Services comes pre-installed with the dependencies needed by the top 100 most popular R packages.</span><span class="sxs-lookup"><span data-stu-id="523f6-191">For convenience, the HDInsight ML Services comes pre-installed with the dependencies needed by the top 100 most popular R packages.</span></span> <span data-ttu-id="523f6-192">However, if the R package(s) you install require libraries beyond these then you must download the base script used here and add steps to install the system libraries.</span><span class="sxs-lookup"><span data-stu-id="523f6-192">However, if the R package(s) you install require libraries beyond these then you must download the base script used here and add steps to install the system libraries.</span></span> <span data-ttu-id="523f6-193">You must then upload the modified script to a public blob container in Azure storage and use the modified script to install the packages.</span><span class="sxs-lookup"><span data-stu-id="523f6-193">You must then upload the modified script to a public blob container in Azure storage and use the modified script to install the packages.</span></span>
   >    <span data-ttu-id="523f6-194">For more information on developing Script Actions, see [Script Action development](../hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="523f6-194">For more information on developing Script Actions, see [Script Action development](../hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Adding a script action](./media/r-server-hdinsight-manage/submitscriptaction.png)

4. <span data-ttu-id="523f6-196">Select **Create** to run the script.</span><span class="sxs-lookup"><span data-stu-id="523f6-196">Select **Create** to run the script.</span></span> <span data-ttu-id="523f6-197">Once the script completes, the R packages are available on all worker nodes.</span><span class="sxs-lookup"><span data-stu-id="523f6-197">Once the script completes, the R packages are available on all worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="523f6-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="523f6-198">Next steps</span></span>

* [<span data-ttu-id="523f6-199">Operationalize ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="523f6-199">Operationalize ML Services cluster on HDInsight</span></span>](r-server-operationalize.md)
* [<span data-ttu-id="523f6-200">Compute context options for ML Service cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="523f6-200">Compute context options for ML Service cluster on HDInsight</span></span>](r-server-compute-contexts.md)
* [<span data-ttu-id="523f6-201">Azure Storage options for ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="523f6-201">Azure Storage options for ML Services cluster on HDInsight</span></span>](r-server-storage.md)
