---
title: Install RStudio with R Server on HDInsight | Microsoft Docs
description: How to install RStudio with R Server on HDInsight.
services: hdinsight
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/28/2017
ms.author: jeffstok
ms.openlocfilehash: 4f9f43326c2193f7603871559d8edc1d707c719f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661606"
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="e7c63-103">Installing RStudio with R Server on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7c63-103">Installing RStudio with R Server on HDInsight</span></span>
<span data-ttu-id="e7c63-104">There are multiple integrated development environments (IDE) available for R today, including Microsoft’s recently announced [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS), a family of desktop and server tools from [RStudio](https://www.rstudio.com/products/rstudio-server/), or Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span><span class="sxs-lookup"><span data-stu-id="e7c63-104">There are multiple integrated development environments (IDE) available for R today, including Microsoft’s recently announced [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS), a family of desktop and server tools from [RStudio](https://www.rstudio.com/products/rstudio-server/), or Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span> <span data-ttu-id="e7c63-105">Among the most popular on Linux is the use of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) that provides a browser-based IDE for use by remote clients.</span><span class="sxs-lookup"><span data-stu-id="e7c63-105">Among the most popular on Linux is the use of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) that provides a browser-based IDE for use by remote clients.</span></span>  <span data-ttu-id="e7c63-106">Installing RStudio Server on the edge node of an HDInsight cluster provides a full IDE experience for the development and execution of R scripts with R Server on the cluster, and can be considerably more productive than default use of the R Console.</span><span class="sxs-lookup"><span data-stu-id="e7c63-106">Installing RStudio Server on the edge node of an HDInsight cluster provides a full IDE experience for the development and execution of R scripts with R Server on the cluster, and can be considerably more productive than default use of the R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="e7c63-107">The procedure described in this article is only relevant if you did not select to install RStudio Server community edition when provisioning your cluster.</span><span class="sxs-lookup"><span data-stu-id="e7c63-107">The procedure described in this article is only relevant if you did not select to install RStudio Server community edition when provisioning your cluster.</span></span>  <span data-ttu-id="e7c63-108">If you added it during provisioning then you access it by clicking on the **R Server Dashboards** tile in the Azure Portal entry for your cluster and then on the **R Studio Server** tile.</span><span class="sxs-lookup"><span data-stu-id="e7c63-108">If you added it during provisioning then you access it by clicking on the **R Server Dashboards** tile in the Azure Portal entry for your cluster and then on the **R Studio Server** tile.</span></span> 

<span data-ttu-id="e7c63-109">In this article you will learn how to install the community (free) version of RStudio Server on the edge node of a cluster by using a custom script.</span><span class="sxs-lookup"><span data-stu-id="e7c63-109">In this article you will learn how to install the community (free) version of RStudio Server on the edge node of a cluster by using a custom script.</span></span> <span data-ttu-id="e7c63-110">If you prefer the commercially licensed Pro version of RStudio Server, you must follow the installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="e7c63-110">If you prefer the commercially licensed Pro version of RStudio Server, you must follow the installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="e7c63-111">The steps in this document require an R Server on HDInsight cluster and will not work correctly if you are using an HDInsight cluster where R was installed using the [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e7c63-111">The steps in this document require an R Server on HDInsight cluster and will not work correctly if you are using an HDInsight cluster where R was installed using the [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md).</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="e7c63-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e7c63-112">Prerequisites</span></span>
* <span data-ttu-id="e7c63-113">An Azure HDInsight cluster with R Server installed.</span><span class="sxs-lookup"><span data-stu-id="e7c63-113">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="e7c63-114">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e7c63-114">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="e7c63-115">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="e7c63-115">An SSH client.</span></span> <span data-ttu-id="e7c63-116">For Linux and Unix distributions or Macintosh OS X, the `ssh` command is provided with the operating system.</span><span class="sxs-lookup"><span data-stu-id="e7c63-116">For Linux and Unix distributions or Macintosh OS X, the `ssh` command is provided with the operating system.</span></span> <span data-ttu-id="e7c63-117">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with the [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="e7c63-117">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with the [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a><span data-ttu-id="e7c63-118">Install RStudio on the cluster using a custom script</span><span class="sxs-lookup"><span data-stu-id="e7c63-118">Install RStudio on the cluster using a custom script</span></span>
1. <span data-ttu-id="e7c63-119">Identify the edge node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="e7c63-119">Identify the edge node of the cluster.</span></span> <span data-ttu-id="e7c63-120">For an HDInsight cluster with R Server, following is the naming convention for head node and edge node.</span><span class="sxs-lookup"><span data-stu-id="e7c63-120">For an HDInsight cluster with R Server, following is the naming convention for head node and edge node.</span></span>

   * <span data-ttu-id="e7c63-121">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="e7c63-121">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="e7c63-122">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="e7c63-122">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 
2. <span data-ttu-id="e7c63-123">SSH into the edge node of the cluster using the above naming pattern.</span><span class="sxs-lookup"><span data-stu-id="e7c63-123">SSH into the edge node of the cluster using the above naming pattern.</span></span> <span data-ttu-id="e7c63-124">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e7c63-124">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="e7c63-125">Once you are connected, become a root user on the cluster.</span><span class="sxs-lookup"><span data-stu-id="e7c63-125">Once you are connected, become a root user on the cluster.</span></span> <span data-ttu-id="e7c63-126">In the SSH session, use the following command.</span><span class="sxs-lookup"><span data-stu-id="e7c63-126">In the SSH session, use the following command.</span></span>

        sudo su -
4. <span data-ttu-id="e7c63-127">Download the custom script to install RStudio.</span><span class="sxs-lookup"><span data-stu-id="e7c63-127">Download the custom script to install RStudio.</span></span> <span data-ttu-id="e7c63-128">Use the following command.</span><span class="sxs-lookup"><span data-stu-id="e7c63-128">Use the following command.</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh
5. <span data-ttu-id="e7c63-129">Change the permissions on the custom script file and run the script.</span><span class="sxs-lookup"><span data-stu-id="e7c63-129">Change the permissions on the custom script file and run the script.</span></span> <span data-ttu-id="e7c63-130">Use the following commands.</span><span class="sxs-lookup"><span data-stu-id="e7c63-130">Use the following commands.</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh
6. <span data-ttu-id="e7c63-131">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed to the next.</span><span class="sxs-lookup"><span data-stu-id="e7c63-131">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed to the next.</span></span> <span data-ttu-id="e7c63-132">If you used an SSH key instead to create the cluster, you must set a password for your SSH user.</span><span class="sxs-lookup"><span data-stu-id="e7c63-132">If you used an SSH key instead to create the cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="e7c63-133">You will need this password when connecting to RStudio.</span><span class="sxs-lookup"><span data-stu-id="e7c63-133">You will need this password when connecting to RStudio.</span></span> <span data-ttu-id="e7c63-134">Run the following commands.</span><span class="sxs-lookup"><span data-stu-id="e7c63-134">Run the following commands.</span></span> <span data-ttu-id="e7c63-135">When prompted for **Current Kerberos password**, just press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e7c63-135">When prompted for **Current Kerberos password**, just press **ENTER**.</span></span>  <span data-ttu-id="e7c63-136">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e7c63-136">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:

    <span data-ttu-id="e7c63-137">If your password is successfully set, you should see a message like this.</span><span class="sxs-lookup"><span data-stu-id="e7c63-137">If your password is successfully set, you should see a message like this.</span></span>

        passwd: password updated successfully

    <span data-ttu-id="e7c63-138">Exit the SSH session.</span><span class="sxs-lookup"><span data-stu-id="e7c63-138">Exit the SSH session.</span></span>

7. <span data-ttu-id="e7c63-139">Create an SSH tunnel to the cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on the HDInsight cluster to the client machine.</span><span class="sxs-lookup"><span data-stu-id="e7c63-139">Create an SSH tunnel to the cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on the HDInsight cluster to the client machine.</span></span> <span data-ttu-id="e7c63-140">You must create an SSH tunnel before opening a new browser session.</span><span class="sxs-lookup"><span data-stu-id="e7c63-140">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="e7c63-141">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/) then open a terminal session and use the following command.</span><span class="sxs-lookup"><span data-stu-id="e7c63-141">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/) then open a terminal session and use the following command.</span></span>

           ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="e7c63-142">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster   You can also use a SSH key rather than a password by adding `-i id_rsa_key`</span><span class="sxs-lookup"><span data-stu-id="e7c63-142">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster   You can also use a SSH key rather than a password by adding `-i id_rsa_key`</span></span>        
   * <span data-ttu-id="e7c63-143">If using a Windows client with PuTTY then</span><span class="sxs-lookup"><span data-stu-id="e7c63-143">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="e7c63-144">Open PuTTY, and enter your connection information.</span><span class="sxs-lookup"><span data-stu-id="e7c63-144">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="e7c63-145">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="e7c63-145">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="e7c63-146">Provide the following information on the **Options controlling SSH port forwarding** form:</span><span class="sxs-lookup"><span data-stu-id="e7c63-146">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="e7c63-147">**Source port** - The port on the client that you wish to forward.</span><span class="sxs-lookup"><span data-stu-id="e7c63-147">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="e7c63-148">For example, **8787**.</span><span class="sxs-lookup"><span data-stu-id="e7c63-148">For example, **8787**.</span></span>
        * <span data-ttu-id="e7c63-149">**Destination** - The destination that must be mapped to the local client machine.</span><span class="sxs-lookup"><span data-stu-id="e7c63-149">**Destination** - The destination that must be mapped to the local client machine.</span></span> <span data-ttu-id="e7c63-150">For example, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="e7c63-150">For example, **localhost:8787**.</span></span>

        <span data-ttu-id="e7c63-151">![Create an SSH tunnel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span><span class="sxs-lookup"><span data-stu-id="e7c63-151">![Create an SSH tunnel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>
     4. <span data-ttu-id="e7c63-152">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span><span class="sxs-lookup"><span data-stu-id="e7c63-152">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>
     5. <span data-ttu-id="e7c63-153">When prompted, log in to the server.</span><span class="sxs-lookup"><span data-stu-id="e7c63-153">When prompted, log in to the server.</span></span> <span data-ttu-id="e7c63-154">This will establish an SSH session and enable the tunnel.</span><span class="sxs-lookup"><span data-stu-id="e7c63-154">This will establish an SSH session and enable the tunnel.</span></span>
8. <span data-ttu-id="e7c63-155">Open a web browser and enter the following URL based on the port you entered for the tunnel.</span><span class="sxs-lookup"><span data-stu-id="e7c63-155">Open a web browser and enter the following URL based on the port you entered for the tunnel.</span></span>

        http://localhost:8787/ 
9. <span data-ttu-id="e7c63-156">You will be prompted to enter the SSH username and password to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="e7c63-156">You will be prompted to enter the SSH username and password to connect to the cluster.</span></span> <span data-ttu-id="e7c63-157">If you used an SSH key while creating the cluster, you must enter the password you created in step 5 above.</span><span class="sxs-lookup"><span data-stu-id="e7c63-157">If you used an SSH key while creating the cluster, you must enter the password you created in step 5 above.</span></span>

    <span data-ttu-id="e7c63-158">![Connect to R Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span><span class="sxs-lookup"><span data-stu-id="e7c63-158">![Connect to R Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>
10. <span data-ttu-id="e7c63-159">To test whether the RStudio installation was successful, you can run a test script that executes R based MapReduce and Spark jobs on the cluster.</span><span class="sxs-lookup"><span data-stu-id="e7c63-159">To test whether the RStudio installation was successful, you can run a test script that executes R based MapReduce and Spark jobs on the cluster.</span></span> <span data-ttu-id="e7c63-160">Go back to the SSH console and enter the following commands to download the test script to run in RStudio.</span><span class="sxs-lookup"><span data-stu-id="e7c63-160">Go back to the SSH console and enter the following commands to download the test script to run in RStudio.</span></span>

*    <span data-ttu-id="e7c63-161">If you created a Hadoop cluster with R, use this command.</span><span class="sxs-lookup"><span data-stu-id="e7c63-161">If you created a Hadoop cluster with R, use this command.</span></span>

           wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
*    <span data-ttu-id="e7c63-162">If you created a Spark cluster with R, use this command.</span><span class="sxs-lookup"><span data-stu-id="e7c63-162">If you created a Spark cluster with R, use this command.</span></span>

                    wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r
11. <span data-ttu-id="e7c63-163">In RStudio, you will see the test script you downloaded.</span><span class="sxs-lookup"><span data-stu-id="e7c63-163">In RStudio, you will see the test script you downloaded.</span></span> <span data-ttu-id="e7c63-164">Double click the file to open it, select the contents of the file, and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="e7c63-164">Double click the file to open it, select the contents of the file, and then click **Run**.</span></span> <span data-ttu-id="e7c63-165">You should see the output in the **Console** pane.</span><span class="sxs-lookup"><span data-stu-id="e7c63-165">You should see the output in the **Console** pane.</span></span>

   <span data-ttu-id="e7c63-166">![Test the installation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test the installation")</span><span class="sxs-lookup"><span data-stu-id="e7c63-166">![Test the installation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test the installation")</span></span>

<span data-ttu-id="e7c63-167">Another option would be to type `source(testhdi.r)` or `source(testhdi_spark.r)` to execute the script.</span><span class="sxs-lookup"><span data-stu-id="e7c63-167">Another option would be to type `source(testhdi.r)` or `source(testhdi_spark.r)` to execute the script.</span></span>

## <a name="see-also"></a><span data-ttu-id="e7c63-168">See also</span><span class="sxs-lookup"><span data-stu-id="e7c63-168">See also</span></span>
* [<span data-ttu-id="e7c63-169">Compute context options for R Server on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="e7c63-169">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="e7c63-170">Azure Storage options for R Server on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7c63-170">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)




