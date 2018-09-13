---
title: Get started with R Server on HDInsight | Microsoft Docs
description: Learn how to create a Apache Spark on HDInsight cluster that includes R Server, and then submit an R script on the cluster.
services: HDInsight
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/13/2017
ms.author: jeffstok
ms.openlocfilehash: c218ecf080b244b1575f79b14d86ff07cf766692
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549298"
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="1c299-103">Get started using R Server on HDInsight</span><span class="sxs-lookup"><span data-stu-id="1c299-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="1c299-104">HDInsight includes an R Server option to be integrated into your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1c299-104">HDInsight includes an R Server option to be integrated into your HDInsight cluster.</span></span> <span data-ttu-id="1c299-105">This allows R scripts to use Spark and MapReduce to run distributed computations.</span><span class="sxs-lookup"><span data-stu-id="1c299-105">This allows R scripts to use Spark and MapReduce to run distributed computations.</span></span> <span data-ttu-id="1c299-106">In this document, you learn how to create an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span><span class="sxs-lookup"><span data-stu-id="1c299-106">In this document, you learn how to create an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c299-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1c299-107">Prerequisites</span></span>

* <span data-ttu-id="1c299-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1c299-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="1c299-109">Go to the article [Get a Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span><span class="sxs-lookup"><span data-stu-id="1c299-109">Go to the article [Get a Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="1c299-110">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span><span class="sxs-lookup"><span data-stu-id="1c299-110">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span></span> <span data-ttu-id="1c299-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="1c299-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="1c299-112">**SSH keys (optional)**: You can secure the SSH account used to connect to the cluster using either a password or a public key.</span><span class="sxs-lookup"><span data-stu-id="1c299-112">**SSH keys (optional)**: You can secure the SSH account used to connect to the cluster using either a password or a public key.</span></span> <span data-ttu-id="1c299-113">Using a password is easier, and allows you to get started without having to create a public/private key pair.</span><span class="sxs-lookup"><span data-stu-id="1c299-113">Using a password is easier, and allows you to get started without having to create a public/private key pair.</span></span> <span data-ttu-id="1c299-114">However, using a key is more secure.</span><span class="sxs-lookup"><span data-stu-id="1c299-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="1c299-115">The steps in this document assume that you are using a password.</span><span class="sxs-lookup"><span data-stu-id="1c299-115">The steps in this document assume that you are using a password.</span></span>


### <a name="access-control-requirements"></a><span data-ttu-id="1c299-116">Access control requirements</span><span class="sxs-lookup"><span data-stu-id="1c299-116">Access control requirements</span></span>

[!INCLUDE [access-control](../../includes/hdinsight-access-control-requirements.md)]

## <a name="automated-cluster-creation"></a><span data-ttu-id="1c299-117">Automated cluster creation</span><span class="sxs-lookup"><span data-stu-id="1c299-117">Automated cluster creation</span></span>

<span data-ttu-id="1c299-118">You can automate the creation of HDInsight R Servers using ARM templates, the SDK, and also PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c299-118">You can automate the creation of HDInsight R Servers using ARM templates, the SDK, and also PowerShell.</span></span>

* <span data-ttu-id="1c299-119">To create an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster.](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="1c299-119">To create an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster.](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="1c299-120">To create an R Server using the .NET SDK, see [create Linux-based clusters in HDInsight using the .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="1c299-120">To create an R Server using the .NET SDK, see [create Linux-based clusters in HDInsight using the .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="1c299-121">To deploy R Server using powershell see the article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1c299-121">To deploy R Server using powershell see the article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


## <a name="create-the-cluster-using-the-azure-portal"></a><span data-ttu-id="1c299-122">Create the cluster using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1c299-122">Create the cluster using the Azure portal</span></span>

1. <span data-ttu-id="1c299-123">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c299-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="1c299-124">Select **NEW**, **Intelligence+ Analytics**, and then **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1c299-124">Select **NEW**, **Intelligence+ Analytics**, and then **HDInsight**.</span></span>

    ![Image of creating a new cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/newcluster.png)

3. <span data-ttu-id="1c299-126">In the **Quick create** experience, enter a name for the cluster in the **Cluster Name** field.</span><span class="sxs-lookup"><span data-stu-id="1c299-126">In the **Quick create** experience, enter a name for the cluster in the **Cluster Name** field.</span></span> <span data-ttu-id="1c299-127">If you have multiple Azure subscriptions, use the **Subscription** entry to select the one you want to use.</span><span class="sxs-lookup"><span data-stu-id="1c299-127">If you have multiple Azure subscriptions, use the **Subscription** entry to select the one you want to use.</span></span>

    ![Cluster name and subscription selections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/clustername.png)

4. <span data-ttu-id="1c299-129">Select **Cluster type** to open the **Cluster configuration** blade.</span><span class="sxs-lookup"><span data-stu-id="1c299-129">Select **Cluster type** to open the **Cluster configuration** blade.</span></span> <span data-ttu-id="1c299-130">On the **Cluster Configuration** blade, select the following options:</span><span class="sxs-lookup"><span data-stu-id="1c299-130">On the **Cluster Configuration** blade, select the following options:</span></span>

   * <span data-ttu-id="1c299-131">**Cluster Type**: R Server</span><span class="sxs-lookup"><span data-stu-id="1c299-131">**Cluster Type**: R Server</span></span>
   * <span data-ttu-id="1c299-132">**Version**: select the version of R Server to install on the cluster.</span><span class="sxs-lookup"><span data-stu-id="1c299-132">**Version**: select the version of R Server to install on the cluster.</span></span> <span data-ttu-id="1c299-133">Select the newest version for the latest capabilities.</span><span class="sxs-lookup"><span data-stu-id="1c299-133">Select the newest version for the latest capabilities.</span></span> <span data-ttu-id="1c299-134">Other versions are available if needed for compatibility.</span><span class="sxs-lookup"><span data-stu-id="1c299-134">Other versions are available if needed for compatibility.</span></span> <span data-ttu-id="1c299-135">Release notes for each of the available versions are available [here](https://msdn.microsoft.com/en-us/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="1c299-135">Release notes for each of the available versions are available [here](https://msdn.microsoft.com/en-us/microsoft-r/notes/r-server-notes).</span></span>
   * <span data-ttu-id="1c299-136">**R Studio community edition for R Server**: this browser-based IDE is installed by default on the edge node.</span><span class="sxs-lookup"><span data-stu-id="1c299-136">**R Studio community edition for R Server**: this browser-based IDE is installed by default on the edge node.</span></span>  <span data-ttu-id="1c299-137">If you would prefer to not have it installed, then un-check the check box.</span><span class="sxs-lookup"><span data-stu-id="1c299-137">If you would prefer to not have it installed, then un-check the check box.</span></span> <span data-ttu-id="1c299-138">If you choose to have it installed then you’ll find the URL for accessing the RStudio Server login on a portal application blade for your cluster once it’s been created.</span><span class="sxs-lookup"><span data-stu-id="1c299-138">If you choose to have it installed then you’ll find the URL for accessing the RStudio Server login on a portal application blade for your cluster once it’s been created.</span></span>

   <span data-ttu-id="1c299-139">Leave the other options at the default values and use the **Select** button to save the cluster type.</span><span class="sxs-lookup"><span data-stu-id="1c299-139">Leave the other options at the default values and use the **Select** button to save the cluster type.</span></span>

   ![Cluster type blade screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/clustertypeconfig.png)

5. <span data-ttu-id="1c299-141">Enter a **Cluster login username** and **Cluster login password**.</span><span class="sxs-lookup"><span data-stu-id="1c299-141">Enter a **Cluster login username** and **Cluster login password**.</span></span>

   <span data-ttu-id="1c299-142">Specify an **SSH Username**.</span><span class="sxs-lookup"><span data-stu-id="1c299-142">Specify an **SSH Username**.</span></span>  <span data-ttu-id="1c299-143">SSH is used to remotely connect to the cluster using a **Secure Shell (SSH)** client.</span><span class="sxs-lookup"><span data-stu-id="1c299-143">SSH is used to remotely connect to the cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="1c299-144">You can either specify the SSH user in this dialog or after the cluster has been created (Configuration tab for the cluster).</span><span class="sxs-lookup"><span data-stu-id="1c299-144">You can either specify the SSH user in this dialog or after the cluster has been created (Configuration tab for the cluster).</span></span> <span data-ttu-id="1c299-145">R Server is configured to expect an **SSH username** of “remoteuser”.</span><span class="sxs-lookup"><span data-stu-id="1c299-145">R Server is configured to expect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="1c299-146">**If you use a different username, you will have to perform an additional step after the cluster is created.**</span><span class="sxs-lookup"><span data-stu-id="1c299-146">**If you use a different username, you will have to perform an additional step after the cluster is created.**</span></span>

   <span data-ttu-id="1c299-147">Leave the box checked for **Use same password as cluster login** to use **PASSWORD** as the authentication type unless you prefer use of a public key.</span><span class="sxs-lookup"><span data-stu-id="1c299-147">Leave the box checked for **Use same password as cluster login** to use **PASSWORD** as the authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="1c299-148">You’ll need a public/private key pair if you’d like to access R Server on the cluster via a remote client, for example RTVS, RStudio or another desktop IDE.</span><span class="sxs-lookup"><span data-stu-id="1c299-148">You’ll need a public/private key pair if you’d like to access R Server on the cluster via a remote client, for example RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="1c299-149">You will need to choose an SSH password if you install RStudio Server community edition.</span><span class="sxs-lookup"><span data-stu-id="1c299-149">You will need to choose an SSH password if you install RStudio Server community edition.</span></span>     

   <span data-ttu-id="1c299-150">To create and use a public/private key pair un-check **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span><span class="sxs-lookup"><span data-stu-id="1c299-150">To create and use a public/private key pair un-check **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span>  <span data-ttu-id="1c299-151">These instructions assume that you have Cygwin with ssh-keygen or equivalent installed.</span><span class="sxs-lookup"><span data-stu-id="1c299-151">These instructions assume that you have Cygwin with ssh-keygen or equivalent installed.</span></span>

   * <span data-ttu-id="1c299-152">Generate a public/private key pair from the command prompt on your laptop:</span><span class="sxs-lookup"><span data-stu-id="1c299-152">Generate a public/private key pair from the command prompt on your laptop:</span></span>

   `ssh-keygen -t rsa -b 2048`

   * <span data-ttu-id="1c299-153">Follow the prompt to name a key file and then enter a passphrase for added security.</span><span class="sxs-lookup"><span data-stu-id="1c299-153">Follow the prompt to name a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="1c299-154">Your screen should look something like the following:</span><span class="sxs-lookup"><span data-stu-id="1c299-154">Your screen should look something like the following:</span></span>

   ![SSH cmd line in Windows](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/sshcmdline.png)

   * <span data-ttu-id="1c299-156">This creates a private key file and a public key file under the name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="1c299-156">This creates a private key file and a public key file under the name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

   ![SSH dir](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/dir.png)

   * <span data-ttu-id="1c299-158">Then specify the public key file (\*.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**</span><span class="sxs-lookup"><span data-stu-id="1c299-158">Then specify the public key file (\*.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**</span></span>

   ![Credentials blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/publickeyfile.png)  

   * <span data-ttu-id="1c299-160">Change permissions on the private keyfile on your laptop</span><span class="sxs-lookup"><span data-stu-id="1c299-160">Change permissions on the private keyfile on your laptop</span></span>

   `chmod 600 <private-key-filename>`

   * <span data-ttu-id="1c299-161">Use the private key file with SSH for remote login</span><span class="sxs-lookup"><span data-stu-id="1c299-161">Use the private key file with SSH for remote login</span></span>

   `ssh –i <private-key-filename> remoteuser@<hostname public ip>`

   <span data-ttu-id="1c299-162">or as part the definition of your Hadoop Spark compute context for R Server on the client (see Using Microsoft R Server as a Hadoop Client in the [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark) section of the online [Get started with SacaleR on Apache Spark document](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started).)</span><span class="sxs-lookup"><span data-stu-id="1c299-162">or as part the definition of your Hadoop Spark compute context for R Server on the client (see Using Microsoft R Server as a Hadoop Client in the [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark) section of the online [Get started with SacaleR on Apache Spark document](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started).)</span></span>

6. <span data-ttu-id="1c299-163">The quick create transitions you to the **Storage** blade to select the storage account settings to be used for the primary location of the HDFS file system used by the cluster.</span><span class="sxs-lookup"><span data-stu-id="1c299-163">The quick create transitions you to the **Storage** blade to select the storage account settings to be used for the primary location of the HDFS file system used by the cluster.</span></span> <span data-ttu-id="1c299-164">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span><span class="sxs-lookup"><span data-stu-id="1c299-164">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

   1. <span data-ttu-id="1c299-165">If you select an Azure Storage account you may select an existing storage account by selecting **Select a storage account** and then selecting the account.</span><span class="sxs-lookup"><span data-stu-id="1c299-165">If you select an Azure Storage account you may select an existing storage account by selecting **Select a storage account** and then selecting the account.</span></span> <span data-ttu-id="1c299-166">Or create a new account using the **Create New** link in the **Select a storage account** section.</span><span class="sxs-lookup"><span data-stu-id="1c299-166">Or create a new account using the **Create New** link in the **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="1c299-167">If you select **New** you must enter a name for the new storage account.</span><span class="sxs-lookup"><span data-stu-id="1c299-167">If you select **New** you must enter a name for the new storage account.</span></span> <span data-ttu-id="1c299-168">A green check will appear if the name is accepted.</span><span class="sxs-lookup"><span data-stu-id="1c299-168">A green check will appear if the name is accepted.</span></span>

      <span data-ttu-id="1c299-169">The **Default Container** will default to the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="1c299-169">The **Default Container** will default to the name of the cluster.</span></span> <span data-ttu-id="1c299-170">Leave this as the value.</span><span class="sxs-lookup"><span data-stu-id="1c299-170">Leave this as the value.</span></span>

      <span data-ttu-id="1c299-171">If a new storage account option was selected a prompt to select **Location** will be given to select which region to create the storage account.</span><span class="sxs-lookup"><span data-stu-id="1c299-171">If a new storage account option was selected a prompt to select **Location** will be given to select which region to create the storage account.</span></span>  

         ![Data source blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="1c299-173">Selecting the location for the default data source will also set the location of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1c299-173">Selecting the location for the default data source will also set the location of the HDInsight cluster.</span></span> <span data-ttu-id="1c299-174">The cluster and default data source must be in the same region.</span><span class="sxs-lookup"><span data-stu-id="1c299-174">The cluster and default data source must be in the same region.</span></span>

   2. <span data-ttu-id="1c299-175">If you select use of an existing Data Lake Store then select the ADLS storage account to use and add the cluster ADD identity to your cluster to allow access to the store.</span><span class="sxs-lookup"><span data-stu-id="1c299-175">If you select use of an existing Data Lake Store then select the ADLS storage account to use and add the cluster ADD identity to your cluster to allow access to the store.</span></span> <span data-ttu-id="1c299-176">For more information on this process review [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span><span class="sxs-lookup"><span data-stu-id="1c299-176">For more information on this process review [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

   <span data-ttu-id="1c299-177">Use the **Select** button to save the data source configuration.</span><span class="sxs-lookup"><span data-stu-id="1c299-177">Use the **Select** button to save the data source configuration.</span></span>


7. <span data-ttu-id="1c299-178">The **Summary** blade will then display to validate all your settings.</span><span class="sxs-lookup"><span data-stu-id="1c299-178">The **Summary** blade will then display to validate all your settings.</span></span> <span data-ttu-id="1c299-179">Here you can change your **Cluster size** to modify the number of servers in your cluster and also specify any **Script actions** you want to run.</span><span class="sxs-lookup"><span data-stu-id="1c299-179">Here you can change your **Cluster size** to modify the number of servers in your cluster and also specify any **Script actions** you want to run.</span></span> <span data-ttu-id="1c299-180">Unless you know that you need a larger cluster, leave the number of worker nodes at the default of `4`.</span><span class="sxs-lookup"><span data-stu-id="1c299-180">Unless you know that you need a larger cluster, leave the number of worker nodes at the default of `4`.</span></span> <span data-ttu-id="1c299-181">The estimated cost of the cluster will be shown within the blade.</span><span class="sxs-lookup"><span data-stu-id="1c299-181">The estimated cost of the cluster will be shown within the blade.</span></span>

   ![cluster summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="1c299-183">If needed, you can re-size your cluster later through the Portal (Cluster -> Settings -> Scale Cluster) to increase or decrease the number of worker nodes.</span><span class="sxs-lookup"><span data-stu-id="1c299-183">If needed, you can re-size your cluster later through the Portal (Cluster -> Settings -> Scale Cluster) to increase or decrease the number of worker nodes.</span></span>  <span data-ttu-id="1c299-184">This can be useful for idling down the cluster when not in use, or for adding capacity to meet the needs of larger tasks.</span><span class="sxs-lookup"><span data-stu-id="1c299-184">This can be useful for idling down the cluster when not in use, or for adding capacity to meet the needs of larger tasks.</span></span>
   >
   >

    <span data-ttu-id="1c299-185">Some factors to keep in mind when sizing your cluster, the data nodes, and the edge node include:</span><span class="sxs-lookup"><span data-stu-id="1c299-185">Some factors to keep in mind when sizing your cluster, the data nodes, and the edge node include:</span></span>  

   * <span data-ttu-id="1c299-186">The performance of distributed R Server analyses on Spark is proportional to the number of worker nodes when the data is large.</span><span class="sxs-lookup"><span data-stu-id="1c299-186">The performance of distributed R Server analyses on Spark is proportional to the number of worker nodes when the data is large.</span></span>  

   * <span data-ttu-id="1c299-187">The performance of R Server analyses is linear in the size of data being analyzed.</span><span class="sxs-lookup"><span data-stu-id="1c299-187">The performance of R Server analyses is linear in the size of data being analyzed.</span></span> <span data-ttu-id="1c299-188">For example:</span><span class="sxs-lookup"><span data-stu-id="1c299-188">For example:</span></span>  

     * <span data-ttu-id="1c299-189">For small to modest data, performance will be best when analyzed in a local compute context on the edge node.</span><span class="sxs-lookup"><span data-stu-id="1c299-189">For small to modest data, performance will be best when analyzed in a local compute context on the edge node.</span></span>  <span data-ttu-id="1c299-190">For more information on the scenarios under which the local and Spark compute contexts work best see  Compute context options for R Server on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c299-190">For more information on the scenarios under which the local and Spark compute contexts work best see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="1c299-191">If you log in to the edge node and run your R script then all but the ScaleR rx-functions will execute <strong>locally</strong> on the edge node so the memory and number of cores of the edge node should be sized accordingly.</span><span class="sxs-lookup"><span data-stu-id="1c299-191">If you log in to the edge node and run your R script then all but the ScaleR rx-functions will execute <strong>locally</strong> on the edge node so the memory and number of cores of the edge node should be sized accordingly.</span></span> <span data-ttu-id="1c299-192">The same applies if you use R Server on HDI as a remote compute context from your laptop.</span><span class="sxs-lookup"><span data-stu-id="1c299-192">The same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Node pricing tiers blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/pricingtier.png)

     <span data-ttu-id="1c299-194">Use the **Select** button to save the node pricing configuration.</span><span class="sxs-lookup"><span data-stu-id="1c299-194">Use the **Select** button to save the node pricing configuration.</span></span>

   <span data-ttu-id="1c299-195">You will note that there is also a link for **Download template and parameters**.</span><span class="sxs-lookup"><span data-stu-id="1c299-195">You will note that there is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="1c299-196">Clicking on this link will display scripts that can be used to automate the creation of a cluster with the selected configuration.</span><span class="sxs-lookup"><span data-stu-id="1c299-196">Clicking on this link will display scripts that can be used to automate the creation of a cluster with the selected configuration.</span></span> <span data-ttu-id="1c299-197">These scripts are also available from the Azure portal entry for your cluster once it has been created.</span><span class="sxs-lookup"><span data-stu-id="1c299-197">These scripts are also available from the Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1c299-198">It will take some time for the cluster to be created, usually around 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="1c299-198">It will take some time for the cluster to be created, usually around 20 minutes.</span></span> <span data-ttu-id="1c299-199">Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the creation process.</span><span class="sxs-lookup"><span data-stu-id="1c299-199">Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the creation process.</span></span>
   >
   >

## <a name="connect-to-rstudio-server"></a><span data-ttu-id="1c299-200">Connect to RStudio Server</span><span class="sxs-lookup"><span data-stu-id="1c299-200">Connect to RStudio Server</span></span>

<span data-ttu-id="1c299-201">If you’ve chosen to include RStudio Server community edition in your installation then you can access the RStudio login via two different methods.</span><span class="sxs-lookup"><span data-stu-id="1c299-201">If you’ve chosen to include RStudio Server community edition in your installation then you can access the RStudio login via two different methods.</span></span>

1. <span data-ttu-id="1c299-202">Either by going to the following URL (where **CLUSTERNAME** is the name of the cluster you've created):</span><span class="sxs-lookup"><span data-stu-id="1c299-202">Either by going to the following URL (where **CLUSTERNAME** is the name of the cluster you've created):</span></span>

    <span data-ttu-id="1c299-203">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="1c299-203">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="1c299-204">Or by opening the entry for your cluster in the Azure portal, selecting the R Server Dashboards quick link and then selecting the R Studio Dashboard:</span><span class="sxs-lookup"><span data-stu-id="1c299-204">Or by opening the entry for your cluster in the Azure portal, selecting the R Server Dashboards quick link and then selecting the R Studio Dashboard:</span></span>

     ![Access the R studio dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Access the R studio dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="1c299-207">No matter the method, the first time you log in you will need to authenticate two times.</span><span class="sxs-lookup"><span data-stu-id="1c299-207">No matter the method, the first time you log in you will need to authenticate two times.</span></span>  <span data-ttu-id="1c299-208">At the first authentication, provide the cluster Admin userid and password.</span><span class="sxs-lookup"><span data-stu-id="1c299-208">At the first authentication, provide the cluster Admin userid and password.</span></span> <span data-ttu-id="1c299-209">At the second prompt provide the SSH userid and password.</span><span class="sxs-lookup"><span data-stu-id="1c299-209">At the second prompt provide the SSH userid and password.</span></span> <span data-ttu-id="1c299-210">Subsequent logins will only require the SSH password and userid.</span><span class="sxs-lookup"><span data-stu-id="1c299-210">Subsequent logins will only require the SSH password and userid.</span></span>

## <a name="connect-to-the-r-server-edge-node"></a><span data-ttu-id="1c299-211">Connect to the R Server edge node</span><span class="sxs-lookup"><span data-stu-id="1c299-211">Connect to the R Server edge node</span></span>

<span data-ttu-id="1c299-212">Connect to R Server edge node of the HDInsight cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="1c299-212">Connect to R Server edge node of the HDInsight cluster using SSH:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="1c299-213">You can also find the `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in the Azure portal by selecting your cluster then **All Settings**, **Apps**, and **RServer**.</span><span class="sxs-lookup"><span data-stu-id="1c299-213">You can also find the `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in the Azure portal by selecting your cluster then **All Settings**, **Apps**, and **RServer**.</span></span> <span data-ttu-id="1c299-214">This will display the SSH Endpoint information for the edge node.</span><span class="sxs-lookup"><span data-stu-id="1c299-214">This will display the SSH Endpoint information for the edge node.</span></span>
>
> ![Image of the SSH Endpoint for the edge node](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/sshendpoint.png)
>
>

<span data-ttu-id="1c299-216">If you used a password to secure your SSH user account you will be prompted to enter it.</span><span class="sxs-lookup"><span data-stu-id="1c299-216">If you used a password to secure your SSH user account you will be prompted to enter it.</span></span> <span data-ttu-id="1c299-217">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span><span class="sxs-lookup"><span data-stu-id="1c299-217">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="1c299-218">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="1c299-218">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`.</span></span>

<span data-ttu-id="1c299-219">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1c299-219">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="1c299-220">Once connected, you will arrive at a prompt similar to the following.</span><span class="sxs-lookup"><span data-stu-id="1c299-220">Once connected, you will arrive at a prompt similar to the following.</span></span>

`username@ed00-myrser:~$`

## <a name="use-the-r-console"></a><span data-ttu-id="1c299-221">Use the R console</span><span class="sxs-lookup"><span data-stu-id="1c299-221">Use the R console</span></span>

1. <span data-ttu-id="1c299-222">From the SSH session, use the following command to start the R console.</span><span class="sxs-lookup"><span data-stu-id="1c299-222">From the SSH session, use the following command to start the R console.</span></span>  

   ```
   R

   You will see output similar to the following.
   R version 3.2.2 (2015-08-14) -- "Fire Safety"
   Copyright (C) 2015 The R Foundation for Statistical Computing
   Platform: x86_64-pc-linux-gnu (64-bit)

   R is free software and comes with ABSOLUTELY NO WARRANTY.
   You are welcome to redistribute it under certain conditions.
   Type 'license()' or 'licence()' for distribution details.

   Natural language support but running in an English locale

   R is a collaborative project with many contributors.
   Type 'contributors()' for more information and
   'citation()' on how to cite R or R packages in publications.

   Type 'demo()' for some demos, 'help()' for on-line help, or
   'help.start()' for an HTML browser interface to help.
   Type 'q()' to quit R.

   Microsoft R Server version 8.0: an enhanced distribution of R
   Microsoft packages Copyright (C) 2016 Microsoft Corporation

   Type 'readme()' for release notes.
   >
   ```

2. <span data-ttu-id="1c299-223">From the `>` prompt, you can enter R code.</span><span class="sxs-lookup"><span data-stu-id="1c299-223">From the `>` prompt, you can enter R code.</span></span> <span data-ttu-id="1c299-224">R server includes packages that allow you to easily interact with Hadoop and run distributed computations.</span><span class="sxs-lookup"><span data-stu-id="1c299-224">R server includes packages that allow you to easily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="1c299-225">For example, use the following command to view the root of the default file system for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1c299-225">For example, use the following command to view the root of the default file system for the HDInsight cluster.</span></span>

`rxHadoopListFiles("/")`

<span data-ttu-id="1c299-226">You can also use the WASB style addressing.</span><span class="sxs-lookup"><span data-stu-id="1c299-226">You can also use the WASB style addressing.</span></span>

`rxHadoopListFiles("wasbs:///")`

## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="1c299-227">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="1c299-227">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="1c299-228">Per the section above regarding use of public/private key pairs to access the cluster, it is possible to set up access to the HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop (see Using Microsoft R Server as a Hadoop Client in the [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark) section of the online [RevoScaleR Hadoop Spark Getting Started guide](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)).</span><span class="sxs-lookup"><span data-stu-id="1c299-228">Per the section above regarding use of public/private key pairs to access the cluster, it is possible to set up access to the HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop (see Using Microsoft R Server as a Hadoop Client in the [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark) section of the online [RevoScaleR Hadoop Spark Getting Started guide](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)).</span></span>  <span data-ttu-id="1c299-229">To do so you will need to specify the following options when defining the RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="1c299-229">To do so you will need to specify the following options when defining the RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="1c299-230">For example:</span><span class="sxs-lookup"><span data-stu-id="1c299-230">For example:</span></span>

```
    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
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
```


## <a name="use-a-compute-context"></a><span data-ttu-id="1c299-231">Use a compute context</span><span class="sxs-lookup"><span data-stu-id="1c299-231">Use a compute context</span></span>

<span data-ttu-id="1c299-232">A compute context allows you to control whether computation will be performed locally on the edge node, or whether it will be distributed across the nodes in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1c299-232">A compute context allows you to control whether computation will be performed locally on the edge node, or whether it will be distributed across the nodes in the HDInsight cluster.</span></span>

1. <span data-ttu-id="1c299-233">From RStudio Server or the R console (in an SSH session), use the following to load example data into the default storage for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c299-233">From RStudio Server or the R console (in an SSH session), use the following to load example data into the default storage for HDInsight.</span></span>

        # Set the HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data to the tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
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

2. <span data-ttu-id="1c299-234">Next, let's create some data info and define two data sources so that we can work with the data.</span><span class="sxs-lookup"><span data-stu-id="1c299-234">Next, let's create some data info and define two data sources so that we can work with the data.</span></span>

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

3. <span data-ttu-id="1c299-235">Let's run a logistic regression over the data using the local compute context.</span><span class="sxs-lookup"><span data-stu-id="1c299-235">Let's run a logistic regression over the data using the local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="1c299-236">You should see output that ends with lines similar to the following.</span><span class="sxs-lookup"><span data-stu-id="1c299-236">You should see output that ends with lines similar to the following.</span></span>

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

4. <span data-ttu-id="1c299-237">Next, let's run the same logistic regression using the Spark context.</span><span class="sxs-lookup"><span data-stu-id="1c299-237">Next, let's run the same logistic regression using the Spark context.</span></span> <span data-ttu-id="1c299-238">The Spark context will distribute the processing over all the worker nodes in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1c299-238">The Spark context will distribute the processing over all the worker nodes in the HDInsight cluster.</span></span>

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
   > <span data-ttu-id="1c299-239">You can also use MapReduce to distribute computation across cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="1c299-239">You can also use MapReduce to distribute computation across cluster nodes.</span></span> <span data-ttu-id="1c299-240">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span><span class="sxs-lookup"><span data-stu-id="1c299-240">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-to-multiple-nodes"></a><span data-ttu-id="1c299-241">Distribute R code to multiple nodes</span><span class="sxs-lookup"><span data-stu-id="1c299-241">Distribute R code to multiple nodes</span></span>

<span data-ttu-id="1c299-242">With R Server you can easily take existing R code and run it across multiple nodes in the cluster by using `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="1c299-242">With R Server you can easily take existing R code and run it across multiple nodes in the cluster by using `rxExec`.</span></span> <span data-ttu-id="1c299-243">This is useful when doing a parameter sweep or simulations.</span><span class="sxs-lookup"><span data-stu-id="1c299-243">This is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="1c299-244">The following is an example of how to use `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="1c299-244">The following is an example of how to use `rxExec`.</span></span>

`rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )`

<span data-ttu-id="1c299-245">If you are still using the Spark or MapReduce context, this will return the nodename value for the worker nodes that the code `(Sys.info()["nodename"])` is ran on.</span><span class="sxs-lookup"><span data-stu-id="1c299-245">If you are still using the Spark or MapReduce context, this will return the nodename value for the worker nodes that the code `(Sys.info()["nodename"])` is ran on.</span></span> <span data-ttu-id="1c299-246">For example, on a four node cluster, you may receive output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="1c299-246">For example, on a four node cluster, you may receive output similar to the following.</span></span>


    ```
    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"
    ```

## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="1c299-247">Accessing Data in Hive and Parquet</span><span class="sxs-lookup"><span data-stu-id="1c299-247">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="1c299-248">A new feature available in R Server 9.0 and above allows direct access to data in Hive and Parquet for use by ScaleR functions in the Spark compute context.</span><span class="sxs-lookup"><span data-stu-id="1c299-248">A new feature available in R Server 9.0 and above allows direct access to data in Hive and Parquet for use by ScaleR functions in the Spark compute context.</span></span> <span data-ttu-id="1c299-249">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL to load data directly into a Spark DataFrame for analysis by ScaleR.</span><span class="sxs-lookup"><span data-stu-id="1c299-249">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL to load data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="1c299-250">The following provides some sample code on use of the new functions:</span><span class="sxs-lookup"><span data-stu-id="1c299-250">The following provides some sample code on use of the new functions:</span></span>



    ```
    #..create a Spark compute context

    myHadoopCluster <- rxSparkConnect(reset = TRUE)
    ```


    ```
    #..retrieve some sample data from Hive and run a model

    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)
    ```

    ```
    #..retrieve some sample data from Parquet and run a model

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
    ```


    ```
    #..check on Spark data objects, cleanup, and close the Spark session

    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)
    ```

<span data-ttu-id="1c299-251">For additional info on use of these new functions see the online help in R Server through use of the ?RxHivedata and ?RxParquetData commands.</span><span class="sxs-lookup"><span data-stu-id="1c299-251">For additional info on use of these new functions see the online help in R Server through use of the ?RxHivedata and ?RxParquetData commands.</span></span>  


## <a name="install-r-packages"></a><span data-ttu-id="1c299-252">Install R packages</span><span class="sxs-lookup"><span data-stu-id="1c299-252">Install R packages</span></span>

<span data-ttu-id="1c299-253">If you would like to install additional R packages on the edge node, you can use `install.packages()` directly from within the R console when connected to the edge node through SSH.</span><span class="sxs-lookup"><span data-stu-id="1c299-253">If you would like to install additional R packages on the edge node, you can use `install.packages()` directly from within the R console when connected to the edge node through SSH.</span></span> <span data-ttu-id="1c299-254">However, if you need to install R packages on the worker nodes of the cluster, you must use a Script Action.</span><span class="sxs-lookup"><span data-stu-id="1c299-254">However, if you need to install R packages on the worker nodes of the cluster, you must use a Script Action.</span></span>

<span data-ttu-id="1c299-255">Script Actions are Bash scripts that are used to make configuration changes to the HDInsight cluster, or to install additional software.</span><span class="sxs-lookup"><span data-stu-id="1c299-255">Script Actions are Bash scripts that are used to make configuration changes to the HDInsight cluster, or to install additional software.</span></span> <span data-ttu-id="1c299-256">In this case, to install additional R packages.</span><span class="sxs-lookup"><span data-stu-id="1c299-256">In this case, to install additional R packages.</span></span> <span data-ttu-id="1c299-257">To install additional packages using a Script Action, use the following steps.</span><span class="sxs-lookup"><span data-stu-id="1c299-257">To install additional packages using a Script Action, use the following steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c299-258">Using Script Actions to install additional R packages can only be used after the cluster has been created.</span><span class="sxs-lookup"><span data-stu-id="1c299-258">Using Script Actions to install additional R packages can only be used after the cluster has been created.</span></span> <span data-ttu-id="1c299-259">It should not be used during cluster creation, as the script relies on R Server being completely installed and configured.</span><span class="sxs-lookup"><span data-stu-id="1c299-259">It should not be used during cluster creation, as the script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="1c299-260">From the [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1c299-260">From the [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="1c299-261">From the **Settings** blade select **Script Actions** and then **Submit New** to submit a new Script Action.</span><span class="sxs-lookup"><span data-stu-id="1c299-261">From the **Settings** blade select **Script Actions** and then **Submit New** to submit a new Script Action.</span></span>

   ![Image of script actions blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/scriptaction.png)

3. <span data-ttu-id="1c299-263">From the **Submit script action** blade, provide the following information.</span><span class="sxs-lookup"><span data-stu-id="1c299-263">From the **Submit script action** blade, provide the following information.</span></span>

   * <span data-ttu-id="1c299-264">**Name**: A friendly name to identify this script</span><span class="sxs-lookup"><span data-stu-id="1c299-264">**Name**: A friendly name to identify this script</span></span>

   * <span data-ttu-id="1c299-265">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="1c299-265">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="1c299-266">**Head**: This should be **un-checked**</span><span class="sxs-lookup"><span data-stu-id="1c299-266">**Head**: This should be **un-checked**</span></span>

   * <span data-ttu-id="1c299-267">**Worker**: This should be **checked**</span><span class="sxs-lookup"><span data-stu-id="1c299-267">**Worker**: This should be **checked**</span></span>

   * <span data-ttu-id="1c299-268">**Edge nodes**: This should be **un-checked**.</span><span class="sxs-lookup"><span data-stu-id="1c299-268">**Edge nodes**: This should be **un-checked**.</span></span>

   * <span data-ttu-id="1c299-269">**Zookeeper**: This should be **un-checked**</span><span class="sxs-lookup"><span data-stu-id="1c299-269">**Zookeeper**: This should be **un-checked**</span></span>

   * <span data-ttu-id="1c299-270">**Parameters**: The R packages to be installed.</span><span class="sxs-lookup"><span data-stu-id="1c299-270">**Parameters**: The R packages to be installed.</span></span> <span data-ttu-id="1c299-271">For example, `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="1c299-271">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="1c299-272">**Persist this script...**: This should be **Checked**</span><span class="sxs-lookup"><span data-stu-id="1c299-272">**Persist this script...**: This should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="1c299-273">By default, all R packages are installed from a snapshot of the Microsoft MRAN repository consistent with the version of R Server that has been installed.</span><span class="sxs-lookup"><span data-stu-id="1c299-273">By default, all R packages are installed from a snapshot of the Microsoft MRAN repository consistent with the version of R Server that has been installed.</span></span>  <span data-ttu-id="1c299-274">If you would like to install newer versions of packages then there is some risk of incompatibility, however this is possible by specifying `useCRAN` as the first element of the package list, for example `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="1c299-274">If you would like to install newer versions of packages then there is some risk of incompatibility, however this is possible by specifying `useCRAN` as the first element of the package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="1c299-275">Some R packages will require additional Linux system libraries.</span><span class="sxs-lookup"><span data-stu-id="1c299-275">Some R packages will require additional Linux system libraries.</span></span> <span data-ttu-id="1c299-276">For convenience, we have pre-installed the dependencies needed by the top 100 most popular R packages.</span><span class="sxs-lookup"><span data-stu-id="1c299-276">For convenience, we have pre-installed the dependencies needed by the top 100 most popular R packages.</span></span> <span data-ttu-id="1c299-277">However, if the R package(s) you install require libraries beyond these then you must download the base script used here and add steps to install the system libraries.</span><span class="sxs-lookup"><span data-stu-id="1c299-277">However, if the R package(s) you install require libraries beyond these then you must download the base script used here and add steps to install the system libraries.</span></span> <span data-ttu-id="1c299-278">You must then upload the modified script to a public blob container in Azure storage and use the modified script to install the packages.</span><span class="sxs-lookup"><span data-stu-id="1c299-278">You must then upload the modified script to a public blob container in Azure storage and use the modified script to install the packages.</span></span>
   >    <span data-ttu-id="1c299-279">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1c299-279">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Adding a script action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="1c299-281">Select **Create** to run the script.</span><span class="sxs-lookup"><span data-stu-id="1c299-281">Select **Create** to run the script.</span></span> <span data-ttu-id="1c299-282">Once the script completes, the R packages will be available on all worker nodes.</span><span class="sxs-lookup"><span data-stu-id="1c299-282">Once the script completes, the R packages will be available on all worker nodes.</span></span>

## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="1c299-283">Using Microsoft R Server Operationalization</span><span class="sxs-lookup"><span data-stu-id="1c299-283">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="1c299-284">When your data modeling is complete, you can operationalize the model to make predictions.</span><span class="sxs-lookup"><span data-stu-id="1c299-284">When your data modeling is complete, you can operationalize the model to make predictions.</span></span> <span data-ttu-id="1c299-285">To configure for Microsoft R Server operationalization perform the steps below.</span><span class="sxs-lookup"><span data-stu-id="1c299-285">To configure for Microsoft R Server operationalization perform the steps below.</span></span>

<span data-ttu-id="1c299-286">First, ssh into the Edge node.</span><span class="sxs-lookup"><span data-stu-id="1c299-286">First, ssh into the Edge node.</span></span> <span data-ttu-id="1c299-287">For example, ```ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net```.</span><span class="sxs-lookup"><span data-stu-id="1c299-287">For example, ```ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net```.</span></span>

<span data-ttu-id="1c299-288">After using ssh, change directory to the following directory and sudo the dotnet dll as shown below.</span><span class="sxs-lookup"><span data-stu-id="1c299-288">After using ssh, change directory to the following directory and sudo the dotnet dll as shown below.</span></span>

```
   cd /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil
   sudo dotnet Microsoft.DeployR.Utils.AdminUtil.dll
```

<span data-ttu-id="1c299-289">To configure Microsoft R Server operationalization with a One-box configuration do the following;</span><span class="sxs-lookup"><span data-stu-id="1c299-289">To configure Microsoft R Server operationalization with a One-box configuration do the following;</span></span>

* <span data-ttu-id="1c299-290">Select “1.</span><span class="sxs-lookup"><span data-stu-id="1c299-290">Select “1.</span></span> <span data-ttu-id="1c299-291">Configure R Server for Operationalization”</span><span class="sxs-lookup"><span data-stu-id="1c299-291">Configure R Server for Operationalization”</span></span>
* <span data-ttu-id="1c299-292">Select “A.</span><span class="sxs-lookup"><span data-stu-id="1c299-292">Select “A.</span></span> <span data-ttu-id="1c299-293">One-box (web + compute nodes)”</span><span class="sxs-lookup"><span data-stu-id="1c299-293">One-box (web + compute nodes)”</span></span>
* <span data-ttu-id="1c299-294">Enter a password for the **admin** user</span><span class="sxs-lookup"><span data-stu-id="1c299-294">Enter a password for the **admin** user</span></span>

![one box op](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="1c299-296">As an optional step you can perform Diagnostic checks by running a diagnostic test as shown below.</span><span class="sxs-lookup"><span data-stu-id="1c299-296">As an optional step you can perform Diagnostic checks by running a diagnostic test as shown below.</span></span>

* <span data-ttu-id="1c299-297">Select “6.</span><span class="sxs-lookup"><span data-stu-id="1c299-297">Select “6.</span></span> <span data-ttu-id="1c299-298">Run diagnostic tests”</span><span class="sxs-lookup"><span data-stu-id="1c299-298">Run diagnostic tests”</span></span>
* <span data-ttu-id="1c299-299">Select “A.</span><span class="sxs-lookup"><span data-stu-id="1c299-299">Select “A.</span></span> <span data-ttu-id="1c299-300">Test configuration”</span><span class="sxs-lookup"><span data-stu-id="1c299-300">Test configuration”</span></span>
* <span data-ttu-id="1c299-301">Enter Username = “admin” and password from configuration step above</span><span class="sxs-lookup"><span data-stu-id="1c299-301">Enter Username = “admin” and password from configuration step above</span></span>
* <span data-ttu-id="1c299-302">Confirm Overall Health = pass</span><span class="sxs-lookup"><span data-stu-id="1c299-302">Confirm Overall Health = pass</span></span>
* <span data-ttu-id="1c299-303">Exit the Admin Utility</span><span class="sxs-lookup"><span data-stu-id="1c299-303">Exit the Admin Utility</span></span>
* <span data-ttu-id="1c299-304">Exit SSH</span><span class="sxs-lookup"><span data-stu-id="1c299-304">Exit SSH</span></span>

![Diagnostic for op](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)

<span data-ttu-id="1c299-306">At this stage, the configuration for Operationalization is complete.</span><span class="sxs-lookup"><span data-stu-id="1c299-306">At this stage, the configuration for Operationalization is complete.</span></span> <span data-ttu-id="1c299-307">Now you can use the ‘mrsdeploy’ package on your RClient to connect to the Operationalization on Edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="1c299-307">Now you can use the ‘mrsdeploy’ package on your RClient to connect to the Operationalization on Edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="1c299-308">Depending on whether your cluster is set up on a virtual network or not, you may need to set up port forward tunneling through SSH login, as explained below:</span><span class="sxs-lookup"><span data-stu-id="1c299-308">Depending on whether your cluster is set up on a virtual network or not, you may need to set up port forward tunneling through SSH login, as explained below:</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="1c299-309">RServer Cluster on virtual network</span><span class="sxs-lookup"><span data-stu-id="1c299-309">RServer Cluster on virtual network</span></span>

<span data-ttu-id="1c299-310">Make sure you allow traffic through port 12800 to the Edge node.</span><span class="sxs-lookup"><span data-stu-id="1c299-310">Make sure you allow traffic through port 12800 to the Edge node.</span></span> <span data-ttu-id="1c299-311">That way, you can use the Edge node to connect to the Operationalization feature.</span><span class="sxs-lookup"><span data-stu-id="1c299-311">That way, you can use the Edge node to connect to the Operationalization feature.</span></span>

```
library(mrsdeploy)

remoteLogin(
    deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
    username = "admin",
    password = "xxxxxxx"
)
```

<span data-ttu-id="1c299-312">If the remoteLogin() cannot connect to the Edge node, but if you can SSH to the Edge node, you need to verify if the rule to allow traffic on port 12800 has been set properly or not.</span><span class="sxs-lookup"><span data-stu-id="1c299-312">If the remoteLogin() cannot connect to the Edge node, but if you can SSH to the Edge node, you need to verify if the rule to allow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="1c299-313">If you continue to face the issue, you can use a workaround by setting up port forward tunneling through SSH.</span><span class="sxs-lookup"><span data-stu-id="1c299-313">If you continue to face the issue, you can use a workaround by setting up port forward tunneling through SSH.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="1c299-314">RServer Cluster not set up on virtual network</span><span class="sxs-lookup"><span data-stu-id="1c299-314">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="1c299-315">If your cluster is not set up on vnet OR if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling as below:</span><span class="sxs-lookup"><span data-stu-id="1c299-315">If your cluster is not set up on vnet OR if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling as below:</span></span>

```
ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net
```

<span data-ttu-id="1c299-316">On Putty, you can set it up as well.</span><span class="sxs-lookup"><span data-stu-id="1c299-316">On Putty, you can set it up as well.</span></span>

![putty ssh connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="1c299-318">Once your SSH session is active, the traffic from your machine’s port 12800 will be forwarded to the Edge node’s port 12800 through SSH session.</span><span class="sxs-lookup"><span data-stu-id="1c299-318">Once your SSH session is active, the traffic from your machine’s port 12800 will be forwarded to the Edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="1c299-319">Make sure you use `127.0.0.1:12800` in your remoteLogin() method.</span><span class="sxs-lookup"><span data-stu-id="1c299-319">Make sure you use `127.0.0.1:12800` in your remoteLogin() method.</span></span> <span data-ttu-id="1c299-320">This will log in to the Edge node’s operationalization through port forwarding.</span><span class="sxs-lookup"><span data-stu-id="1c299-320">This will log in to the Edge node’s operationalization through port forwarding.</span></span>

```
library(mrsdeploy)

remoteLogin(
    deployr_endpoint = "http://127.0.0.1:12800",
    username = "admin",
    password = "xxxxxxx"
)
```

## <a name="how-to-scale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="1c299-321">How to scale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes?</span><span class="sxs-lookup"><span data-stu-id="1c299-321">How to scale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes?</span></span>


### <a name="decommission-the-worker-nodes"></a><span data-ttu-id="1c299-322">Decommission the worker node(s)</span><span class="sxs-lookup"><span data-stu-id="1c299-322">Decommission the worker node(s)</span></span>

<span data-ttu-id="1c299-323">Microsoft R Server is currently not managed through Yarn.</span><span class="sxs-lookup"><span data-stu-id="1c299-323">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="1c299-324">If the worker nodes are not decommissioned, Yarn resource manager will not work as expected because it will not be aware of the resources being taken up by the server.</span><span class="sxs-lookup"><span data-stu-id="1c299-324">If the worker nodes are not decommissioned, Yarn resource manager will not work as expected because it will not be aware of the resources being taken up by the server.</span></span> <span data-ttu-id="1c299-325">In order to avoid that, we recommend decommissioning the worker nodes where you want to scale the compute nodes to.</span><span class="sxs-lookup"><span data-stu-id="1c299-325">In order to avoid that, we recommend decommissioning the worker nodes where you want to scale the compute nodes to.</span></span>

<span data-ttu-id="1c299-326">Steps to decommissioning worker nodes:</span><span class="sxs-lookup"><span data-stu-id="1c299-326">Steps to decommissioning worker nodes:</span></span>

* <span data-ttu-id="1c299-327">Log in to HDI cluster's Ambari console and click on "hosts" tab</span><span class="sxs-lookup"><span data-stu-id="1c299-327">Log in to HDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="1c299-328">Select worker nodes (to be decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span><span class="sxs-lookup"><span data-stu-id="1c299-328">Select worker nodes (to be decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="1c299-329">For example, in the image below we have selected wn3 and wn4 to decommission.</span><span class="sxs-lookup"><span data-stu-id="1c299-329">For example, in the image below we have selected wn3 and wn4 to decommission.</span></span>  

   ![decommission worker nodes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="1c299-331">Select "Actions" > "Selected Hosts" > "DataNodes" > click on "Decommission"</span><span class="sxs-lookup"><span data-stu-id="1c299-331">Select "Actions" > "Selected Hosts" > "DataNodes" > click on "Decommission"</span></span>
* <span data-ttu-id="1c299-332">Select "Actions" > "Selected Hosts" > "NodeManagers" > click on "Decommission"</span><span class="sxs-lookup"><span data-stu-id="1c299-332">Select "Actions" > "Selected Hosts" > "NodeManagers" > click on "Decommission"</span></span>
* <span data-ttu-id="1c299-333">Select "Actions" > "Selected Hosts" > "DataNodes" > click on "Stop"</span><span class="sxs-lookup"><span data-stu-id="1c299-333">Select "Actions" > "Selected Hosts" > "DataNodes" > click on "Stop"</span></span>
* <span data-ttu-id="1c299-334">Select "Actions" > "Selected Hosts" > "NodeManagers" > click on "Stop"</span><span class="sxs-lookup"><span data-stu-id="1c299-334">Select "Actions" > "Selected Hosts" > "NodeManagers" > click on "Stop"</span></span>
* <span data-ttu-id="1c299-335">Select "Actions" > "Selected Hosts" > "Hosts" > click on "Stop All Components"</span><span class="sxs-lookup"><span data-stu-id="1c299-335">Select "Actions" > "Selected Hosts" > "Hosts" > click on "Stop All Components"</span></span>
* <span data-ttu-id="1c299-336">Unselect the worker nodes and Select the head nodes</span><span class="sxs-lookup"><span data-stu-id="1c299-336">Unselect the worker nodes and Select the head nodes</span></span>
* <span data-ttu-id="1c299-337">Select "Actions" > "Selected Hosts" > "Hosts" > "Restart All Components</span><span class="sxs-lookup"><span data-stu-id="1c299-337">Select "Actions" > "Selected Hosts" > "Hosts" > "Restart All Components</span></span>


### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="1c299-338">Configure Compute nodes on each decommissioned worker node(s)</span><span class="sxs-lookup"><span data-stu-id="1c299-338">Configure Compute nodes on each decommissioned worker node(s)</span></span>

* <span data-ttu-id="1c299-339">SSH into each decommissioned worker node</span><span class="sxs-lookup"><span data-stu-id="1c299-339">SSH into each decommissioned worker node</span></span>
* <span data-ttu-id="1c299-340">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`</span><span class="sxs-lookup"><span data-stu-id="1c299-340">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`</span></span>
* <span data-ttu-id="1c299-341">Enter "1" to select option "1.</span><span class="sxs-lookup"><span data-stu-id="1c299-341">Enter "1" to select option "1.</span></span> <span data-ttu-id="1c299-342">Configure R Server for Operationalization"</span><span class="sxs-lookup"><span data-stu-id="1c299-342">Configure R Server for Operationalization"</span></span>
* <span data-ttu-id="1c299-343">Enter "c" to select option "C.</span><span class="sxs-lookup"><span data-stu-id="1c299-343">Enter "c" to select option "C.</span></span> <span data-ttu-id="1c299-344">Compute node".</span><span class="sxs-lookup"><span data-stu-id="1c299-344">Compute node".</span></span> <span data-ttu-id="1c299-345">This will configure compute node on the worker node.</span><span class="sxs-lookup"><span data-stu-id="1c299-345">This will configure compute node on the worker node.</span></span>
* <span data-ttu-id="1c299-346">Exit the Admin Utility</span><span class="sxs-lookup"><span data-stu-id="1c299-346">Exit the Admin Utility</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="1c299-347">Add compute nodes details on Web Node</span><span class="sxs-lookup"><span data-stu-id="1c299-347">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="1c299-348">Once all decommissioned worker nodes have been configured to run compute node, come back on the Edge node and add decommissioned worker nodes' IP addresses in the Microsoft R Server web node's configuration:</span><span class="sxs-lookup"><span data-stu-id="1c299-348">Once all decommissioned worker nodes have been configured to run compute node, come back on the Edge node and add decommissioned worker nodes' IP addresses in the Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="1c299-349">SSH into the Edge node</span><span class="sxs-lookup"><span data-stu-id="1c299-349">SSH into the Edge node</span></span>
* <span data-ttu-id="1c299-350">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`</span><span class="sxs-lookup"><span data-stu-id="1c299-350">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`</span></span>
* <span data-ttu-id="1c299-351">Look for the "URIs" section, and add worker node's IP and port details.</span><span class="sxs-lookup"><span data-stu-id="1c299-351">Look for the "URIs" section, and add worker node's IP and port details.</span></span>

![decommission worker nodes cmdline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)

## <a name="next-steps"></a><span data-ttu-id="1c299-353">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c299-353">Next steps</span></span>

<span data-ttu-id="1c299-354">Now that you understand how to create a new HDInsight cluster that includes R Server, and the basics of using the R console from an SSH session, use the following to discover other ways of working with R Server on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c299-354">Now that you understand how to create a new HDInsight cluster that includes R Server, and the basics of using the R console from an SSH session, use the following to discover other ways of working with R Server on HDInsight.</span></span>

* [<span data-ttu-id="1c299-355">Add RStudio Server to HDInsight (if not installed during cluster creation)</span><span class="sxs-lookup"><span data-stu-id="1c299-355">Add RStudio Server to HDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="1c299-356">Compute context options for R Server on HDInsight</span><span class="sxs-lookup"><span data-stu-id="1c299-356">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="1c299-357">Azure Storage options for R Server on HDInsight</span><span class="sxs-lookup"><span data-stu-id="1c299-357">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)



















