---
title: Script action development with Linux-based HDInsight | Microsoft Docs
description: 'How to customize Linux-based HDInsight clusters with Script Action. Script actions are a way to customize Azure HDInsight clusters by specifying cluster configuration settings or installing additional services, tools, or other software on the cluster. '
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: larryfr
ms.openlocfilehash: 9068e0e92e15491d3377a1b8f42071b56373396e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661146"
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="5f80a-104">Script action development with HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f80a-104">Script action development with HDInsight</span></span>

<span data-ttu-id="5f80a-105">Script actions are a way to customize Azure HDInsight clusters by specifying cluster configuration settings or installing additional services, tools, or other software on the cluster.</span><span class="sxs-lookup"><span data-stu-id="5f80a-105">Script actions are a way to customize Azure HDInsight clusters by specifying cluster configuration settings or installing additional services, tools, or other software on the cluster.</span></span> <span data-ttu-id="5f80a-106">You can use script actions during cluster creation or on a running cluster.</span><span class="sxs-lookup"><span data-stu-id="5f80a-106">You can use script actions during cluster creation or on a running cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f80a-107">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="5f80a-107">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5f80a-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="5f80a-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5f80a-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="5f80a-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="5f80a-110">What are script actions?</span><span class="sxs-lookup"><span data-stu-id="5f80a-110">What are script actions?</span></span>

<span data-ttu-id="5f80a-111">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span><span class="sxs-lookup"><span data-stu-id="5f80a-111">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span></span> <span data-ttu-id="5f80a-112">A script action is executed as root, and provides full access rights to the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="5f80a-112">A script action is executed as root, and provides full access rights to the cluster nodes.</span></span>

<span data-ttu-id="5f80a-113">Script actions can be applied through the following methods:</span><span class="sxs-lookup"><span data-stu-id="5f80a-113">Script actions can be applied through the following methods:</span></span>

| <span data-ttu-id="5f80a-114">Use this to apply a script...</span><span class="sxs-lookup"><span data-stu-id="5f80a-114">Use this to apply a script...</span></span> | <span data-ttu-id="5f80a-115">During cluster creation...</span><span class="sxs-lookup"><span data-stu-id="5f80a-115">During cluster creation...</span></span> | <span data-ttu-id="5f80a-116">On a running cluster...</span><span class="sxs-lookup"><span data-stu-id="5f80a-116">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="5f80a-117">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5f80a-117">Azure Portal</span></span> |<span data-ttu-id="5f80a-118">✓</span><span class="sxs-lookup"><span data-stu-id="5f80a-118">✓</span></span> |<span data-ttu-id="5f80a-119">✓</span><span class="sxs-lookup"><span data-stu-id="5f80a-119">✓</span></span> |
| <span data-ttu-id="5f80a-120">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f80a-120">Azure PowerShell</span></span> |<span data-ttu-id="5f80a-121">✓</span><span class="sxs-lookup"><span data-stu-id="5f80a-121">✓</span></span> |<span data-ttu-id="5f80a-122">✓</span><span class="sxs-lookup"><span data-stu-id="5f80a-122">✓</span></span> |
| <span data-ttu-id="5f80a-123">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5f80a-123">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="5f80a-124">✓</span><span class="sxs-lookup"><span data-stu-id="5f80a-124">✓</span></span> |
| <span data-ttu-id="5f80a-125">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5f80a-125">HDInsight .NET SDK</span></span> |<span data-ttu-id="5f80a-126">✓</span><span class="sxs-lookup"><span data-stu-id="5f80a-126">✓</span></span> |<span data-ttu-id="5f80a-127">✓</span><span class="sxs-lookup"><span data-stu-id="5f80a-127">✓</span></span> |
| <span data-ttu-id="5f80a-128">Azure Resource Manager Template</span><span class="sxs-lookup"><span data-stu-id="5f80a-128">Azure Resource Manager Template</span></span> |<span data-ttu-id="5f80a-129">✓</span><span class="sxs-lookup"><span data-stu-id="5f80a-129">✓</span></span> |&nbsp; |

<span data-ttu-id="5f80a-130">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5f80a-130">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="bestPracticeScripting"></a><span data-ttu-id="5f80a-131">Best practices for script development</span><span class="sxs-lookup"><span data-stu-id="5f80a-131">Best practices for script development</span></span>

<span data-ttu-id="5f80a-132">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span><span class="sxs-lookup"><span data-stu-id="5f80a-132">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* [<span data-ttu-id="5f80a-133">Target the Hadoop version</span><span class="sxs-lookup"><span data-stu-id="5f80a-133">Target the Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="5f80a-134">Target the OS Version</span><span class="sxs-lookup"><span data-stu-id="5f80a-134">Target the OS Version</span></span>](#bps10)
* [<span data-ttu-id="5f80a-135">Provide stable links to script resources</span><span class="sxs-lookup"><span data-stu-id="5f80a-135">Provide stable links to script resources</span></span>](#bPS2)
* [<span data-ttu-id="5f80a-136">Use pre-compiled resources</span><span class="sxs-lookup"><span data-stu-id="5f80a-136">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="5f80a-137">Ensure that the cluster customization script is idempotent</span><span class="sxs-lookup"><span data-stu-id="5f80a-137">Ensure that the cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="5f80a-138">Ensure high availability of the cluster architecture</span><span class="sxs-lookup"><span data-stu-id="5f80a-138">Ensure high availability of the cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="5f80a-139">Configure the custom components to use Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="5f80a-139">Configure the custom components to use Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="5f80a-140">Write information to STDOUT and STDERR</span><span class="sxs-lookup"><span data-stu-id="5f80a-140">Write information to STDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="5f80a-141">Save files as ASCII with LF line endings</span><span class="sxs-lookup"><span data-stu-id="5f80a-141">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="5f80a-142">Use retry logic to recover from transient errors</span><span class="sxs-lookup"><span data-stu-id="5f80a-142">Use retry logic to recover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="5f80a-143">Script actions must complete within 60 minutes, or they will timeout.</span><span class="sxs-lookup"><span data-stu-id="5f80a-143">Script actions must complete within 60 minutes, or they will timeout.</span></span> <span data-ttu-id="5f80a-144">During node provisioning, the script is ran concurrently with other setup and configuration processes.</span><span class="sxs-lookup"><span data-stu-id="5f80a-144">During node provisioning, the script is ran concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="5f80a-145">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span><span class="sxs-lookup"><span data-stu-id="5f80a-145">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>

### <a name="bPS1"></a><span data-ttu-id="5f80a-146">Target the Hadoop version</span><span class="sxs-lookup"><span data-stu-id="5f80a-146">Target the Hadoop version</span></span>

<span data-ttu-id="5f80a-147">Different versions of HDInsight have different versions of Hadoop services and components installed.</span><span class="sxs-lookup"><span data-stu-id="5f80a-147">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="5f80a-148">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span><span class="sxs-lookup"><span data-stu-id="5f80a-148">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span></span> <span data-ttu-id="5f80a-149">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="5f80a-149">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <a name="bps10"></a> <span data-ttu-id="5f80a-150">Target the OS version</span><span class="sxs-lookup"><span data-stu-id="5f80a-150">Target the OS version</span></span>

<span data-ttu-id="5f80a-151">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span><span class="sxs-lookup"><span data-stu-id="5f80a-151">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span></span> <span data-ttu-id="5f80a-152">Different versions of HDInsight rely on different versions of Ubuntu, which may effect how your script behaves.</span><span class="sxs-lookup"><span data-stu-id="5f80a-152">Different versions of HDInsight rely on different versions of Ubuntu, which may effect how your script behaves.</span></span> <span data-ttu-id="5f80a-153">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span><span class="sxs-lookup"><span data-stu-id="5f80a-153">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="5f80a-154">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span><span class="sxs-lookup"><span data-stu-id="5f80a-154">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="5f80a-155">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span><span class="sxs-lookup"><span data-stu-id="5f80a-155">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span></span>

<span data-ttu-id="5f80a-156">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span><span class="sxs-lookup"><span data-stu-id="5f80a-156">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span></span>

<span data-ttu-id="5f80a-157">You can check the OS version by using `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-157">You can check the OS version by using `lsb_release`.</span></span> <span data-ttu-id="5f80a-158">The following code snippets from the Hue install script demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span><span class="sxs-lookup"><span data-stu-id="5f80a-158">The following code snippets from the Hue install script demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="5f80a-159">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="5f80a-159">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="5f80a-160">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="5f80a-160">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="5f80a-161">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="5f80a-161">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <a name="bPS2"></a><span data-ttu-id="5f80a-162">Provide stable links to script resources</span><span class="sxs-lookup"><span data-stu-id="5f80a-162">Provide stable links to script resources</span></span>

<span data-ttu-id="5f80a-163">You should make sure that the scripts and resources used by the script remain available throughout the lifetime of the cluster, and that the versions of these files do not change for the duration.</span><span class="sxs-lookup"><span data-stu-id="5f80a-163">You should make sure that the scripts and resources used by the script remain available throughout the lifetime of the cluster, and that the versions of these files do not change for the duration.</span></span> <span data-ttu-id="5f80a-164">These resources are required if new nodes are added to the cluster during scaling operations.</span><span class="sxs-lookup"><span data-stu-id="5f80a-164">These resources are required if new nodes are added to the cluster during scaling operations.</span></span>

<span data-ttu-id="5f80a-165">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span><span class="sxs-lookup"><span data-stu-id="5f80a-165">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f80a-166">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span><span class="sxs-lookup"><span data-stu-id="5f80a-166">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="5f80a-167">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account, which is a public, read-only container maintained by the HDInsight team.</span><span class="sxs-lookup"><span data-stu-id="5f80a-167">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account, which is a public, read-only container maintained by the HDInsight team.</span></span>

### <a name="bPS4"></a><span data-ttu-id="5f80a-168">Use pre-compiled resources</span><span class="sxs-lookup"><span data-stu-id="5f80a-168">Use pre-compiled resources</span></span>

<span data-ttu-id="5f80a-169">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span><span class="sxs-lookup"><span data-stu-id="5f80a-169">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="5f80a-170">Instead, pre-compile the resources and store the binary version in Azure Blob storage so that it can quickly be downloaded to the cluster from your script.</span><span class="sxs-lookup"><span data-stu-id="5f80a-170">Instead, pre-compile the resources and store the binary version in Azure Blob storage so that it can quickly be downloaded to the cluster from your script.</span></span>

### <a name="bPS3"></a><span data-ttu-id="5f80a-171">Ensure that the cluster customization script is idempotent</span><span class="sxs-lookup"><span data-stu-id="5f80a-171">Ensure that the cluster customization script is idempotent</span></span>

<span data-ttu-id="5f80a-172">Scripts must be designed to be idempotent in the sense that if the script is ran multiple times, it should ensure that the cluster is returned to the same state every time it is ran.</span><span class="sxs-lookup"><span data-stu-id="5f80a-172">Scripts must be designed to be idempotent in the sense that if the script is ran multiple times, it should ensure that the cluster is returned to the same state every time it is ran.</span></span>

<span data-ttu-id="5f80a-173">For example, if a custom script installs an application at /usr/local/bin on its first run, then on each subsequent run the script should check whether the application already exists at the /usr/local/bin location before proceeding with other steps in the script.</span><span class="sxs-lookup"><span data-stu-id="5f80a-173">For example, if a custom script installs an application at /usr/local/bin on its first run, then on each subsequent run the script should check whether the application already exists at the /usr/local/bin location before proceeding with other steps in the script.</span></span>

### <a name="bPS5"></a><span data-ttu-id="5f80a-174">Ensure high availability of the cluster architecture</span><span class="sxs-lookup"><span data-stu-id="5f80a-174">Ensure high availability of the cluster architecture</span></span>

<span data-ttu-id="5f80a-175">Linux-based HDInsight clusters provides two head nodes that are active within the cluster, and script actions are ran for both nodes.</span><span class="sxs-lookup"><span data-stu-id="5f80a-175">Linux-based HDInsight clusters provides two head nodes that are active within the cluster, and script actions are ran for both nodes.</span></span> <span data-ttu-id="5f80a-176">If the components you install expect only one head node, you must design a script that will only install the component on one of the two head nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5f80a-176">If the components you install expect only one head node, you must design a script that will only install the component on one of the two head nodes in the cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f80a-177">Default services installed as part of HDInsight are designed to fail over between the two head nodes as needed, however this functionality is not extended to custom components installed through script ctions.</span><span class="sxs-lookup"><span data-stu-id="5f80a-177">Default services installed as part of HDInsight are designed to fail over between the two head nodes as needed, however this functionality is not extended to custom components installed through script ctions.</span></span> <span data-ttu-id="5f80a-178">If you need the components installed through a script action to be highly available, you must implement your own failover mechanism that uses the two available head nodes.</span><span class="sxs-lookup"><span data-stu-id="5f80a-178">If you need the components installed through a script action to be highly available, you must implement your own failover mechanism that uses the two available head nodes.</span></span>

### <a name="bPS6"></a><span data-ttu-id="5f80a-179">Configure the custom components to use Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="5f80a-179">Configure the custom components to use Azure Blob storage</span></span>

<span data-ttu-id="5f80a-180">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span><span class="sxs-lookup"><span data-stu-id="5f80a-180">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="5f80a-181">HDInsight uses Azure Blob Storage (WASB) as the default storage.</span><span class="sxs-lookup"><span data-stu-id="5f80a-181">HDInsight uses Azure Blob Storage (WASB) as the default storage.</span></span> <span data-ttu-id="5f80a-182">This provides an HDFS compatible file system that persists data even if the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="5f80a-182">This provides an HDFS compatible file system that persists data even if the cluster is deleted.</span></span> <span data-ttu-id="5f80a-183">You should configure components you install to use WASB instead of HDFS.</span><span class="sxs-lookup"><span data-stu-id="5f80a-183">You should configure components you install to use WASB instead of HDFS.</span></span>

<span data-ttu-id="5f80a-184">For example, the following copies the giraph-examples.jar file from the local file system to WASB:</span><span class="sxs-lookup"><span data-stu-id="5f80a-184">For example, the following copies the giraph-examples.jar file from the local file system to WASB:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

### <a name="bPS7"></a><span data-ttu-id="5f80a-185">Write information to STDOUT and STDERR</span><span class="sxs-lookup"><span data-stu-id="5f80a-185">Write information to STDOUT and STDERR</span></span>

<span data-ttu-id="5f80a-186">Information written to STDOUT and STDERR during script execution is logged, and can be viewed using the Ambari web UI.</span><span class="sxs-lookup"><span data-stu-id="5f80a-186">Information written to STDOUT and STDERR during script execution is logged, and can be viewed using the Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="5f80a-187">Ambari will only be available if the cluster is successfully created.</span><span class="sxs-lookup"><span data-stu-id="5f80a-187">Ambari will only be available if the cluster is successfully created.</span></span> <span data-ttu-id="5f80a-188">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span><span class="sxs-lookup"><span data-stu-id="5f80a-188">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="5f80a-189">Most utilities and installation packages will already write information to STDOUT and STDERR, however you may want to add additional logging.</span><span class="sxs-lookup"><span data-stu-id="5f80a-189">Most utilities and installation packages will already write information to STDOUT and STDERR, however you may want to add additional logging.</span></span> <span data-ttu-id="5f80a-190">To send text to STDOUT use `echo`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-190">To send text to STDOUT use `echo`.</span></span> <span data-ttu-id="5f80a-191">For example:</span><span class="sxs-lookup"><span data-stu-id="5f80a-191">For example:</span></span>

```bash
echo "Getting ready to install Foo"
```

<span data-ttu-id="5f80a-192">By default, `echo` will send the string to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="5f80a-192">By default, `echo` will send the string to STDOUT.</span></span> <span data-ttu-id="5f80a-193">To direct it to STDERR, add `>&2` before `echo`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-193">To direct it to STDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="5f80a-194">For example:</span><span class="sxs-lookup"><span data-stu-id="5f80a-194">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="5f80a-195">This redirects information sent to STDOUT (1, which is default so not listed here,) to STDERR (2).</span><span class="sxs-lookup"><span data-stu-id="5f80a-195">This redirects information sent to STDOUT (1, which is default so not listed here,) to STDERR (2).</span></span> <span data-ttu-id="5f80a-196">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="5f80a-196">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="5f80a-197">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="5f80a-197">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <a name="bps8"></a> <span data-ttu-id="5f80a-198">Save files as ASCII with LF line endings</span><span class="sxs-lookup"><span data-stu-id="5f80a-198">Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="5f80a-199">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span><span class="sxs-lookup"><span data-stu-id="5f80a-199">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="5f80a-200">If files are stored as UTF-8, which may include a Byte Order Mark at the beginning of the file, or with line endings of CRLF, which is common for Windows editors, then the script will fail with errors similar to the following:</span><span class="sxs-lookup"><span data-stu-id="5f80a-200">If files are stored as UTF-8, which may include a Byte Order Mark at the beginning of the file, or with line endings of CRLF, which is common for Windows editors, then the script will fail with errors similar to the following:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a> <span data-ttu-id="5f80a-201">Use retry logic to recover from transient errors</span><span class="sxs-lookup"><span data-stu-id="5f80a-201">Use retry logic to recover from transient errors</span></span>

<span data-ttu-id="5f80a-202">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span><span class="sxs-lookup"><span data-stu-id="5f80a-202">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span></span> <span data-ttu-id="5f80a-203">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span><span class="sxs-lookup"><span data-stu-id="5f80a-203">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span></span>

<span data-ttu-id="5f80a-204">To make your script resilient to transient errors, you can implement retry logic.</span><span class="sxs-lookup"><span data-stu-id="5f80a-204">To make your script resilient to transient errors, you can implement retry logic.</span></span> <span data-ttu-id="5f80a-205">The following is an example of a function that will run any command passed to it and (if the command fails,) retry up to three times.</span><span class="sxs-lookup"><span data-stu-id="5f80a-205">The following is an example of a function that will run any command passed to it and (if the command fails,) retry up to three times.</span></span> <span data-ttu-id="5f80a-206">It will wait two seconds between each retry.</span><span class="sxs-lookup"><span data-stu-id="5f80a-206">It will wait two seconds between each retry.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="5f80a-207">The following are examples of using this function.</span><span class="sxs-lookup"><span data-stu-id="5f80a-207">The following are examples of using this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a><span data-ttu-id="5f80a-208">Helper methods for custom scripts</span><span class="sxs-lookup"><span data-stu-id="5f80a-208">Helper methods for custom scripts</span></span>

<span data-ttu-id="5f80a-209">script action helper methods are utilities that you can use while writing custom scripts.</span><span class="sxs-lookup"><span data-stu-id="5f80a-209">script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="5f80a-210">These are defined in [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh), and can be included in your scripts using the following:</span><span class="sxs-lookup"><span data-stu-id="5f80a-210">These are defined in [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh), and can be included in your scripts using the following:</span></span>

```bash
# Import the helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="5f80a-211">This makes the following helpers available for use in your script:</span><span class="sxs-lookup"><span data-stu-id="5f80a-211">This makes the following helpers available for use in your script:</span></span>

| <span data-ttu-id="5f80a-212">Helper usage</span><span class="sxs-lookup"><span data-stu-id="5f80a-212">Helper usage</span></span> | <span data-ttu-id="5f80a-213">Description</span><span class="sxs-lookup"><span data-stu-id="5f80a-213">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="5f80a-214">Downloads a file from the source URI to the specified file path.</span><span class="sxs-lookup"><span data-stu-id="5f80a-214">Downloads a file from the source URI to the specified file path.</span></span> <span data-ttu-id="5f80a-215">By default, it will not overwrite an existing file.</span><span class="sxs-lookup"><span data-stu-id="5f80a-215">By default, it will not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="5f80a-216">Extracts a tar file (using `-xf`,) to the destination directory.</span><span class="sxs-lookup"><span data-stu-id="5f80a-216">Extracts a tar file (using `-xf`,) to the destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="5f80a-217">If ran on a cluster head node, returns 1; otherwise, 0.</span><span class="sxs-lookup"><span data-stu-id="5f80a-217">If ran on a cluster head node, returns 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="5f80a-218">If the current node is a data (worker) node, returns a 1; otherwise, 0.</span><span class="sxs-lookup"><span data-stu-id="5f80a-218">If the current node is a data (worker) node, returns a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="5f80a-219">If the current node is the first data (worker) node (named workernode0,) returns a 1; otherwise, 0.</span><span class="sxs-lookup"><span data-stu-id="5f80a-219">If the current node is the first data (worker) node (named workernode0,) returns a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="5f80a-220">Returns the fully qualified domain name of the headnodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5f80a-220">Returns the fully qualified domain name of the headnodes in the cluster.</span></span> <span data-ttu-id="5f80a-221">Names are comma delimited.</span><span class="sxs-lookup"><span data-stu-id="5f80a-221">Names are comma delimited.</span></span> <span data-ttu-id="5f80a-222">An empty string is returned on error.</span><span class="sxs-lookup"><span data-stu-id="5f80a-222">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="5f80a-223">Gets the fully qualified domain name of the primary headnode.</span><span class="sxs-lookup"><span data-stu-id="5f80a-223">Gets the fully qualified domain name of the primary headnode.</span></span> <span data-ttu-id="5f80a-224">An empty string is returned on error.</span><span class="sxs-lookup"><span data-stu-id="5f80a-224">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="5f80a-225">Gets the fully qualified domain name of the secondary headnode.</span><span class="sxs-lookup"><span data-stu-id="5f80a-225">Gets the fully qualified domain name of the secondary headnode.</span></span> <span data-ttu-id="5f80a-226">An empty string is returned on error.</span><span class="sxs-lookup"><span data-stu-id="5f80a-226">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="5f80a-227">Gets the numeric suffix of the primary headnode.</span><span class="sxs-lookup"><span data-stu-id="5f80a-227">Gets the numeric suffix of the primary headnode.</span></span> <span data-ttu-id="5f80a-228">An empty string is returned on error.</span><span class="sxs-lookup"><span data-stu-id="5f80a-228">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="5f80a-229">Gets the numeric suffix of the secondary headnode.</span><span class="sxs-lookup"><span data-stu-id="5f80a-229">Gets the numeric suffix of the secondary headnode.</span></span> <span data-ttu-id="5f80a-230">An empty string is returned on error.</span><span class="sxs-lookup"><span data-stu-id="5f80a-230">An empty string is returned on error.</span></span> |

## <a name="commonusage"></a><span data-ttu-id="5f80a-231">Common usage patterns</span><span class="sxs-lookup"><span data-stu-id="5f80a-231">Common usage patterns</span></span>

<span data-ttu-id="5f80a-232">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span><span class="sxs-lookup"><span data-stu-id="5f80a-232">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-to-a-script"></a><span data-ttu-id="5f80a-233">Passing parameters to a script</span><span class="sxs-lookup"><span data-stu-id="5f80a-233">Passing parameters to a script</span></span>

<span data-ttu-id="5f80a-234">In some cases, your script may require parameters.</span><span class="sxs-lookup"><span data-stu-id="5f80a-234">In some cases, your script may require parameters.</span></span> <span data-ttu-id="5f80a-235">For example, you may need the admin password for the cluster in order to retrieve information from the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="5f80a-235">For example, you may need the admin password for the cluster in order to retrieve information from the Ambari REST API.</span></span>

<span data-ttu-id="5f80a-236">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span><span class="sxs-lookup"><span data-stu-id="5f80a-236">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span></span> <span data-ttu-id="5f80a-237">`$0` contains the name of the script itself.</span><span class="sxs-lookup"><span data-stu-id="5f80a-237">`$0` contains the name of the script itself.</span></span>

<span data-ttu-id="5f80a-238">Values passed to the script as parameters should be enclosed by single quotes (') so that the passed value is treated as a literal, and special treatment isn't given to included characters such as '!'.</span><span class="sxs-lookup"><span data-stu-id="5f80a-238">Values passed to the script as parameters should be enclosed by single quotes (') so that the passed value is treated as a literal, and special treatment isn't given to included characters such as '!'.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="5f80a-239">Setting environment variables</span><span class="sxs-lookup"><span data-stu-id="5f80a-239">Setting environment variables</span></span>

<span data-ttu-id="5f80a-240">Setting an environment variable is performed by the following:</span><span class="sxs-lookup"><span data-stu-id="5f80a-240">Setting an environment variable is performed by the following:</span></span>

    VARIABLENAME=value

<span data-ttu-id="5f80a-241">Where VARIABLENAME is the name of the variable.</span><span class="sxs-lookup"><span data-stu-id="5f80a-241">Where VARIABLENAME is the name of the variable.</span></span> <span data-ttu-id="5f80a-242">To access the variable after this, use `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-242">To access the variable after this, use `$VARIABLENAME`.</span></span> <span data-ttu-id="5f80a-243">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following:</span><span class="sxs-lookup"><span data-stu-id="5f80a-243">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following:</span></span>

    PASSWORD=$1

<span data-ttu-id="5f80a-244">Subsequent access to the information could then use `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-244">Subsequent access to the information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="5f80a-245">Environment variables set within the script only exist within the scope of the script.</span><span class="sxs-lookup"><span data-stu-id="5f80a-245">Environment variables set within the script only exist within the scope of the script.</span></span> <span data-ttu-id="5f80a-246">In some cases, you may need to add system wide environment variables that will persist after the script has finished.</span><span class="sxs-lookup"><span data-stu-id="5f80a-246">In some cases, you may need to add system wide environment variables that will persist after the script has finished.</span></span> <span data-ttu-id="5f80a-247">Usually this is so that users connecting to the cluster via SSH can use the components installed by your script.</span><span class="sxs-lookup"><span data-stu-id="5f80a-247">Usually this is so that users connecting to the cluster via SSH can use the components installed by your script.</span></span> <span data-ttu-id="5f80a-248">You can accomplish this by adding the environment variable to `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-248">You can accomplish this by adding the environment variable to `/etc/environment`.</span></span> <span data-ttu-id="5f80a-249">For example, the following adds **HADOOP\_CONF\_DIR**:</span><span class="sxs-lookup"><span data-stu-id="5f80a-249">For example, the following adds **HADOOP\_CONF\_DIR**:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="5f80a-250">Access to locations where the custom scripts are stored</span><span class="sxs-lookup"><span data-stu-id="5f80a-250">Access to locations where the custom scripts are stored</span></span>

<span data-ttu-id="5f80a-251">Scripts used to customize a cluster needs to be stored in one of the following locations:</span><span class="sxs-lookup"><span data-stu-id="5f80a-251">Scripts used to customize a cluster needs to be stored in one of the following locations:</span></span>

* <span data-ttu-id="5f80a-252">The __default storage account__ for the cluster.</span><span class="sxs-lookup"><span data-stu-id="5f80a-252">The __default storage account__ for the cluster.</span></span>

* <span data-ttu-id="5f80a-253">An __additional storage account__ associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="5f80a-253">An __additional storage account__ associated with the cluster.</span></span>

* <span data-ttu-id="5f80a-254">A __publicly readable URI__, such as OneDrive, Dropbox, etc.</span><span class="sxs-lookup"><span data-stu-id="5f80a-254">A __publicly readable URI__, such as OneDrive, Dropbox, etc.</span></span>

* <span data-ttu-id="5f80a-255">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5f80a-255">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span></span> <span data-ttu-id="5f80a-256">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5f80a-256">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f80a-257">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span><span class="sxs-lookup"><span data-stu-id="5f80a-257">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

<span data-ttu-id="5f80a-258">If your script accesses resources located elsewhere these also need to be in a publicly accessible (at least public read-only).</span><span class="sxs-lookup"><span data-stu-id="5f80a-258">If your script accesses resources located elsewhere these also need to be in a publicly accessible (at least public read-only).</span></span> <span data-ttu-id="5f80a-259">For instance you might want to download a file to the cluster using `download_file`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-259">For instance you might want to download a file to the cluster using `download_file`.</span></span>

<span data-ttu-id="5f80a-260">Storing the file in an Azure storage account accessible by the cluster (such as the default storage account,) will provide fast access, as this storage is within the Azure network.</span><span class="sxs-lookup"><span data-stu-id="5f80a-260">Storing the file in an Azure storage account accessible by the cluster (such as the default storage account,) will provide fast access, as this storage is within the Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="5f80a-261">The URI format used to reference the script differs depending on the service being used.</span><span class="sxs-lookup"><span data-stu-id="5f80a-261">The URI format used to reference the script differs depending on the service being used.</span></span> <span data-ttu-id="5f80a-262">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-262">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="5f80a-263">For publicly readable URIs, use `http://` or `https://`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-263">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="5f80a-264">For Data Lake Store, use `adl://`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-264">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-the-operating-system-version"></a><span data-ttu-id="5f80a-265">Checking the operating system version</span><span class="sxs-lookup"><span data-stu-id="5f80a-265">Checking the operating system version</span></span>

<span data-ttu-id="5f80a-266">Different versions of HDInsight rely on specific versions of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5f80a-266">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="5f80a-267">There may be differences between OS versions that you must check for in your script.</span><span class="sxs-lookup"><span data-stu-id="5f80a-267">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="5f80a-268">For example, you may need to install a binary that is tied to the version of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5f80a-268">For example, you may need to install a binary that is tied to the version of Ubuntu.</span></span>

<span data-ttu-id="5f80a-269">To check the OS version, use `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-269">To check the OS version, use `lsb_release`.</span></span> <span data-ttu-id="5f80a-270">For example, the following demonstrates how to reference a different tar file depending on the OS version:</span><span class="sxs-lookup"><span data-stu-id="5f80a-270">For example, the following demonstrates how to reference a different tar file depending on the OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a><span data-ttu-id="5f80a-271">Checklist for deploying a script action</span><span class="sxs-lookup"><span data-stu-id="5f80a-271">Checklist for deploying a script action</span></span>

<span data-ttu-id="5f80a-272">Here are the steps we took when preparing to deploy these scripts:</span><span class="sxs-lookup"><span data-stu-id="5f80a-272">Here are the steps we took when preparing to deploy these scripts:</span></span>

* <span data-ttu-id="5f80a-273">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span><span class="sxs-lookup"><span data-stu-id="5f80a-273">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="5f80a-274">This can be any of the default or additional Storage accounts specified at the time of cluster deployment, or any other publicly accessible storage container.</span><span class="sxs-lookup"><span data-stu-id="5f80a-274">This can be any of the default or additional Storage accounts specified at the time of cluster deployment, or any other publicly accessible storage container.</span></span>
* <span data-ttu-id="5f80a-275">Add checks into scripts to make sure that they execute impotently, so that the script can be executed multiple times on the same node.</span><span class="sxs-lookup"><span data-stu-id="5f80a-275">Add checks into scripts to make sure that they execute impotently, so that the script can be executed multiple times on the same node.</span></span>
* <span data-ttu-id="5f80a-276">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span><span class="sxs-lookup"><span data-stu-id="5f80a-276">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="5f80a-277">In the event that OS-level settings or Hadoop service configuration files were changed, you may want to restart HDInsight services so that they can pick up any OS-level settings, such as the environment variables set in the scripts.</span><span class="sxs-lookup"><span data-stu-id="5f80a-277">In the event that OS-level settings or Hadoop service configuration files were changed, you may want to restart HDInsight services so that they can pick up any OS-level settings, such as the environment variables set in the scripts.</span></span>

## <a name="runScriptAction"></a><span data-ttu-id="5f80a-278">How to run a script action</span><span class="sxs-lookup"><span data-stu-id="5f80a-278">How to run a script action</span></span>

<span data-ttu-id="5f80a-279">You can use script actions to customize HDInsight clusters by using the Azure portal, Azure PowerShell, Azure Resource Manager templates or the HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5f80a-279">You can use script actions to customize HDInsight clusters by using the Azure portal, Azure PowerShell, Azure Resource Manager templates or the HDInsight .NET SDK.</span></span> <span data-ttu-id="5f80a-280">For instructions, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5f80a-280">For instructions, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="sampleScripts"></a><span data-ttu-id="5f80a-281">Custom script samples</span><span class="sxs-lookup"><span data-stu-id="5f80a-281">Custom script samples</span></span>

<span data-ttu-id="5f80a-282">Microsoft provides sample scripts to install components on an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5f80a-282">Microsoft provides sample scripts to install components on an HDInsight cluster.</span></span> <span data-ttu-id="5f80a-283">The sample scripts and instructions on how to use them are available at the links below:</span><span class="sxs-lookup"><span data-stu-id="5f80a-283">The sample scripts and instructions on how to use them are available at the links below:</span></span>

* [<span data-ttu-id="5f80a-284">Install and use Hue on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="5f80a-284">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="5f80a-285">Install and use R on HDInsight Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="5f80a-285">Install and use R on HDInsight Hadoop clusters</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* [<span data-ttu-id="5f80a-286">Install and use Solr on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="5f80a-286">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="5f80a-287">Install and use Giraph on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="5f80a-287">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)  

> [!NOTE]
> <span data-ttu-id="5f80a-288">The documents linked above are specific to Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="5f80a-288">The documents linked above are specific to Linux-based HDInsight clusters.</span></span> <span data-ttu-id="5f80a-289">For a scripts that work with Windows-based HDInsight, see [Script action development with HDInsight (Windows)](hdinsight-hadoop-script-actions.md) or use the links available at the top of each article.</span><span class="sxs-lookup"><span data-stu-id="5f80a-289">For a scripts that work with Windows-based HDInsight, see [Script action development with HDInsight (Windows)](hdinsight-hadoop-script-actions.md) or use the links available at the top of each article.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5f80a-290">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="5f80a-290">Troubleshooting</span></span>

<span data-ttu-id="5f80a-291">The following are errors you may encounter when using scripts you have developed:</span><span class="sxs-lookup"><span data-stu-id="5f80a-291">The following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="5f80a-292">**Error**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-292">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="5f80a-293">Sometimes followed by `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-293">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="5f80a-294">*Cause*: This error is caused when the lines in a script end with CRLF.</span><span class="sxs-lookup"><span data-stu-id="5f80a-294">*Cause*: This error is caused when the lines in a script end with CRLF.</span></span> <span data-ttu-id="5f80a-295">Unix systems expect only LF as the line ending.</span><span class="sxs-lookup"><span data-stu-id="5f80a-295">Unix systems expect only LF as the line ending.</span></span>

<span data-ttu-id="5f80a-296">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span><span class="sxs-lookup"><span data-stu-id="5f80a-296">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="5f80a-297">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span><span class="sxs-lookup"><span data-stu-id="5f80a-297">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span></span> <span data-ttu-id="5f80a-298">You may also use the following commands on a Unix system to change the CRLF to an LF:</span><span class="sxs-lookup"><span data-stu-id="5f80a-298">You may also use the following commands on a Unix system to change the CRLF to an LF:</span></span>

> [!NOTE]
> <span data-ttu-id="5f80a-299">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span><span class="sxs-lookup"><span data-stu-id="5f80a-299">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span></span> <span data-ttu-id="5f80a-300">Select one based on the utilities available on your system.</span><span class="sxs-lookup"><span data-stu-id="5f80a-300">Select one based on the utilities available on your system.</span></span>

| <span data-ttu-id="5f80a-301">Command</span><span class="sxs-lookup"><span data-stu-id="5f80a-301">Command</span></span> | <span data-ttu-id="5f80a-302">Notes</span><span class="sxs-lookup"><span data-stu-id="5f80a-302">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="5f80a-303">The original file will be backed up with a .BAK extension</span><span class="sxs-lookup"><span data-stu-id="5f80a-303">The original file will be backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="5f80a-304">OUTFILE will contain a version with only LF endings</span><span class="sxs-lookup"><span data-stu-id="5f80a-304">OUTFILE will contain a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` |<span data-ttu-id="5f80a-305">This will modify the file directly without creating a new file</span><span class="sxs-lookup"><span data-stu-id="5f80a-305">This will modify the file directly without creating a new file</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="5f80a-306">OUTFILE will contain a version with only LF endings.</span><span class="sxs-lookup"><span data-stu-id="5f80a-306">OUTFILE will contain a version with only LF endings.</span></span> |

<span data-ttu-id="5f80a-307">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="5f80a-307">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="5f80a-308">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span><span class="sxs-lookup"><span data-stu-id="5f80a-308">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="5f80a-309">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span><span class="sxs-lookup"><span data-stu-id="5f80a-309">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="5f80a-310">You may also use the following command on a Linux or Unix system to create a new file without the BOM:</span><span class="sxs-lookup"><span data-stu-id="5f80a-310">You may also use the following command on a Linux or Unix system to create a new file without the BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="5f80a-311">For the above command, replace **INFILE** with the file containing the BOM.</span><span class="sxs-lookup"><span data-stu-id="5f80a-311">For the above command, replace **INFILE** with the file containing the BOM.</span></span> <span data-ttu-id="5f80a-312">**OUTFILE** should be a new file name, which will contain the script without the BOM.</span><span class="sxs-lookup"><span data-stu-id="5f80a-312">**OUTFILE** should be a new file name, which will contain the script without the BOM.</span></span>

## <a name="seeAlso"></a><span data-ttu-id="5f80a-313">Next steps</span><span class="sxs-lookup"><span data-stu-id="5f80a-313">Next steps</span></span>

* <span data-ttu-id="5f80a-314">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="5f80a-314">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="5f80a-315">Use the [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) to learn more about creating .NET applications that manage HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f80a-315">Use the [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) to learn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="5f80a-316">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="5f80a-316">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span></span>
