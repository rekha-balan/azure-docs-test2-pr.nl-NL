---
title: Add Hive libraries during HDInsight cluster creation | Microsoft Docs
description: Learn how to add Hive libraries (jar files,) to an HDInsight cluster during cluster creation.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: dd5df541c0362b8fe8265fd26dc73908215076ad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563183"
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="1c001-103">Add custom Hive libraries when creating your HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="1c001-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="1c001-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action to pre-load the libraries during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="1c001-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action to pre-load the libraries during cluster creation.</span></span> <span data-ttu-id="1c001-105">Libraries added using the steps in this document are globally available in Hive - there is no need to use [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) to load them.</span><span class="sxs-lookup"><span data-stu-id="1c001-105">Libraries added using the steps in this document are globally available in Hive - there is no need to use [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) to load them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="1c001-106">How it works</span><span class="sxs-lookup"><span data-stu-id="1c001-106">How it works</span></span>

<span data-ttu-id="1c001-107">When creating a cluster, you can optionally specify a Script Action that runs a script on the cluster nodes while they are being created.</span><span class="sxs-lookup"><span data-stu-id="1c001-107">When creating a cluster, you can optionally specify a Script Action that runs a script on the cluster nodes while they are being created.</span></span> <span data-ttu-id="1c001-108">The script in this document accepts a single parameter, which is a WASB location that contains the libraries (stored as jar files) to be pre-loaded.</span><span class="sxs-lookup"><span data-stu-id="1c001-108">The script in this document accepts a single parameter, which is a WASB location that contains the libraries (stored as jar files) to be pre-loaded.</span></span>

<span data-ttu-id="1c001-109">During cluster creation, the script enumerates the files, copies them to the `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them to the `hive.aux.jars.path` property in the `core-site.xml` file.</span><span class="sxs-lookup"><span data-stu-id="1c001-109">During cluster creation, the script enumerates the files, copies them to the `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them to the `hive.aux.jars.path` property in the `core-site.xml` file.</span></span> <span data-ttu-id="1c001-110">On Linux-based clusters, it also updates the `hive-env.sh` file with the location of the files.</span><span class="sxs-lookup"><span data-stu-id="1c001-110">On Linux-based clusters, it also updates the `hive-env.sh` file with the location of the files.</span></span>

> [!NOTE]
> <span data-ttu-id="1c001-111">Using the script actions in this article makes the libraries available in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="1c001-111">Using the script actions in this article makes the libraries available in the following scenarios:</span></span>
>
> * <span data-ttu-id="1c001-112">**Linux-based HDInsight** - when using the a Hive client, **WebHCat**, and **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="1c001-112">**Linux-based HDInsight** - when using the a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="1c001-113">**Windows-based HDInsight** - when using the Hive client and **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="1c001-113">**Windows-based HDInsight** - when using the Hive client and **WebHCat**.</span></span>

## <a name="the-script"></a><span data-ttu-id="1c001-114">The script</span><span class="sxs-lookup"><span data-stu-id="1c001-114">The script</span></span>

<span data-ttu-id="1c001-115">**Script location**</span><span class="sxs-lookup"><span data-stu-id="1c001-115">**Script location**</span></span>

<span data-ttu-id="1c001-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="1c001-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="1c001-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="1c001-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c001-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="1c001-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1c001-119">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="1c001-119">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

<span data-ttu-id="1c001-120">**Requirements**</span><span class="sxs-lookup"><span data-stu-id="1c001-120">**Requirements**</span></span>

* <span data-ttu-id="1c001-121">The scripts must be applied to both the **Head nodes** and **Worker nodes**.</span><span class="sxs-lookup"><span data-stu-id="1c001-121">The scripts must be applied to both the **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="1c001-122">The jars you wish to install must be stored in Azure Blob Storage in a **single container**.</span><span class="sxs-lookup"><span data-stu-id="1c001-122">The jars you wish to install must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="1c001-123">The storage account containing the library of jar files **must** be linked to the HDInsight cluster during creation.</span><span class="sxs-lookup"><span data-stu-id="1c001-123">The storage account containing the library of jar files **must** be linked to the HDInsight cluster during creation.</span></span> <span data-ttu-id="1c001-124">It must either be the default storage account, or an account added through __optional configuration__.</span><span class="sxs-lookup"><span data-stu-id="1c001-124">It must either be the default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="1c001-125">The WASB path to the container must be specified as a parameter to the Script Action.</span><span class="sxs-lookup"><span data-stu-id="1c001-125">The WASB path to the container must be specified as a parameter to the Script Action.</span></span> <span data-ttu-id="1c001-126">For example, if the jars are stored in a container named **libs** on a storage account named **mystorage**, the parameter would be **wasbs://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="1c001-126">For example, if the jars are stored in a container named **libs** on a storage account named **mystorage**, the parameter would be **wasbs://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1c001-127">This document assumes that you have already create a storage account, blob container, and uploaded the files to it.</span><span class="sxs-lookup"><span data-stu-id="1c001-127">This document assumes that you have already create a storage account, blob container, and uploaded the files to it.</span></span>
  >
  > <span data-ttu-id="1c001-128">If you have not created a storage account, you can do so through the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c001-128">If you have not created a storage account, you can do so through the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1c001-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) to create a container in the account and upload files to it.</span><span class="sxs-lookup"><span data-stu-id="1c001-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) to create a container in the account and upload files to it.</span></span>

## <a name="create-a-cluster-using-the-script"></a><span data-ttu-id="1c001-130">Create a cluster using the script</span><span class="sxs-lookup"><span data-stu-id="1c001-130">Create a cluster using the script</span></span>

> [!NOTE]
> <span data-ttu-id="1c001-131">The following steps create a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1c001-131">The following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="1c001-132">To create a Windows-based cluster, select **Windows** as the cluster OS when creating the cluster, and use the Windows (PowerShell) script instead of the bash script.</span><span class="sxs-lookup"><span data-stu-id="1c001-132">To create a Windows-based cluster, select **Windows** as the cluster OS when creating the cluster, and use the Windows (PowerShell) script instead of the bash script.</span></span>
>
> <span data-ttu-id="1c001-133">You can also use Azure PowerShell or the HDInsight .NET SDK to create a cluster using this script.</span><span class="sxs-lookup"><span data-stu-id="1c001-133">You can also use Azure PowerShell or the HDInsight .NET SDK to create a cluster using this script.</span></span> <span data-ttu-id="1c001-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1c001-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="1c001-135">Start provisioning a cluster by using the steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span><span class="sxs-lookup"><span data-stu-id="1c001-135">Start provisioning a cluster by using the steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="1c001-136">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span><span class="sxs-lookup"><span data-stu-id="1c001-136">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="1c001-137">**NAME**: Enter a friendly name for the script action.</span><span class="sxs-lookup"><span data-stu-id="1c001-137">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="1c001-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="1c001-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="1c001-139">**HEAD**: Check this option.</span><span class="sxs-lookup"><span data-stu-id="1c001-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="1c001-140">**WORKER**: Check this option.</span><span class="sxs-lookup"><span data-stu-id="1c001-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="1c001-141">**ZOOKEEPER**: Leave this blank.</span><span class="sxs-lookup"><span data-stu-id="1c001-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="1c001-142">**PARAMETERS**: Enter the WASB address to the container and storage account that contains the jars.</span><span class="sxs-lookup"><span data-stu-id="1c001-142">**PARAMETERS**: Enter the WASB address to the container and storage account that contains the jars.</span></span> <span data-ttu-id="1c001-143">For example, **wasbs://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="1c001-143">For example, **wasbs://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="1c001-144">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="1c001-144">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span>

4. <span data-ttu-id="1c001-145">On the **Optional Configuration** blade, select **Linked Storage Accounts** and select the **Add a storage key** link.</span><span class="sxs-lookup"><span data-stu-id="1c001-145">On the **Optional Configuration** blade, select **Linked Storage Accounts** and select the **Add a storage key** link.</span></span> <span data-ttu-id="1c001-146">Select the storage account that contains the jars, and then use the **select** buttons to save settings and return the **Optional Configuration** blade.</span><span class="sxs-lookup"><span data-stu-id="1c001-146">Select the storage account that contains the jars, and then use the **select** buttons to save settings and return the **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="1c001-147">Use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span><span class="sxs-lookup"><span data-stu-id="1c001-147">Use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

6. <span data-ttu-id="1c001-148">Continue provisioning the cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1c001-148">Continue provisioning the cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="1c001-149">Once cluster creation finishes, you are able to use the jars added through this script from Hive without having to use the `ADD JAR` statement.</span><span class="sxs-lookup"><span data-stu-id="1c001-149">Once cluster creation finishes, you are able to use the jars added through this script from Hive without having to use the `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c001-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c001-150">Next steps</span></span>

<span data-ttu-id="1c001-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="1c001-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
