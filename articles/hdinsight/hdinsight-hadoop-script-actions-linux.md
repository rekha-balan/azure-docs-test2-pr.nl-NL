---
title: Script action development with Linux-based HDInsight - Azure
description: Learn how to use Bash scripts to customize Linux-based HDInsight clusters. The script action feature of HDInsight allows you to run scripts during or after cluster creation. Scripts can be used to change cluster configuration settings or install additional software.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/10/2018
ms.author: jasonh
ms.openlocfilehash: 0225115fb6c74f736e6a5fba09414dc2ebafd84e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791653"
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="2a61a-105">Script action development with HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a61a-105">Script action development with HDInsight</span></span>

<span data-ttu-id="2a61a-106">Learn how to customize your HDInsight cluster using Bash scripts.</span><span class="sxs-lookup"><span data-stu-id="2a61a-106">Learn how to customize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="2a61a-107">Script actions are a way to customize HDInsight during or after cluster creation.</span><span class="sxs-lookup"><span data-stu-id="2a61a-107">Script actions are a way to customize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a61a-108">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="2a61a-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="2a61a-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="2a61a-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2a61a-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2a61a-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="2a61a-111">What are script actions</span><span class="sxs-lookup"><span data-stu-id="2a61a-111">What are script actions</span></span>

<span data-ttu-id="2a61a-112">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span><span class="sxs-lookup"><span data-stu-id="2a61a-112">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span></span> <span data-ttu-id="2a61a-113">A script action is executed as root, and provides full access rights to the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="2a61a-113">A script action is executed as root, and provides full access rights to the cluster nodes.</span></span>

<span data-ttu-id="2a61a-114">Script actions can be applied through the following methods:</span><span class="sxs-lookup"><span data-stu-id="2a61a-114">Script actions can be applied through the following methods:</span></span>

| <span data-ttu-id="2a61a-115">Use this method to apply a script...</span><span class="sxs-lookup"><span data-stu-id="2a61a-115">Use this method to apply a script...</span></span> | <span data-ttu-id="2a61a-116">During cluster creation...</span><span class="sxs-lookup"><span data-stu-id="2a61a-116">During cluster creation...</span></span> | <span data-ttu-id="2a61a-117">On a running cluster...</span><span class="sxs-lookup"><span data-stu-id="2a61a-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="2a61a-118">Azure portal</span><span class="sxs-lookup"><span data-stu-id="2a61a-118">Azure portal</span></span> |<span data-ttu-id="2a61a-119">✓</span><span class="sxs-lookup"><span data-stu-id="2a61a-119">✓</span></span> |<span data-ttu-id="2a61a-120">✓</span><span class="sxs-lookup"><span data-stu-id="2a61a-120">✓</span></span> |
| <span data-ttu-id="2a61a-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a61a-121">Azure PowerShell</span></span> |<span data-ttu-id="2a61a-122">✓</span><span class="sxs-lookup"><span data-stu-id="2a61a-122">✓</span></span> |<span data-ttu-id="2a61a-123">✓</span><span class="sxs-lookup"><span data-stu-id="2a61a-123">✓</span></span> |
| <span data-ttu-id="2a61a-124">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2a61a-124">Azure CLI 1.0</span></span> |&nbsp; |<span data-ttu-id="2a61a-125">✓</span><span class="sxs-lookup"><span data-stu-id="2a61a-125">✓</span></span> |
| <span data-ttu-id="2a61a-126">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2a61a-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="2a61a-127">✓</span><span class="sxs-lookup"><span data-stu-id="2a61a-127">✓</span></span> |<span data-ttu-id="2a61a-128">✓</span><span class="sxs-lookup"><span data-stu-id="2a61a-128">✓</span></span> |
| <span data-ttu-id="2a61a-129">Azure Resource Manager Template</span><span class="sxs-lookup"><span data-stu-id="2a61a-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="2a61a-130">✓</span><span class="sxs-lookup"><span data-stu-id="2a61a-130">✓</span></span> |&nbsp; |

<span data-ttu-id="2a61a-131">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2a61a-131">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="bestPracticeScripting"></a><span data-ttu-id="2a61a-132">Best practices for script development</span><span class="sxs-lookup"><span data-stu-id="2a61a-132">Best practices for script development</span></span>

<span data-ttu-id="2a61a-133">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span><span class="sxs-lookup"><span data-stu-id="2a61a-133">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* [<span data-ttu-id="2a61a-134">Target the Hadoop version</span><span class="sxs-lookup"><span data-stu-id="2a61a-134">Target the Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="2a61a-135">Target the OS Version</span><span class="sxs-lookup"><span data-stu-id="2a61a-135">Target the OS Version</span></span>](#bps10)
* [<span data-ttu-id="2a61a-136">Provide stable links to script resources</span><span class="sxs-lookup"><span data-stu-id="2a61a-136">Provide stable links to script resources</span></span>](#bPS2)
* [<span data-ttu-id="2a61a-137">Use pre-compiled resources</span><span class="sxs-lookup"><span data-stu-id="2a61a-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="2a61a-138">Ensure that the cluster customization script is idempotent</span><span class="sxs-lookup"><span data-stu-id="2a61a-138">Ensure that the cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="2a61a-139">Ensure high availability of the cluster architecture</span><span class="sxs-lookup"><span data-stu-id="2a61a-139">Ensure high availability of the cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="2a61a-140">Configure the custom components to use Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="2a61a-140">Configure the custom components to use Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="2a61a-141">Write information to STDOUT and STDERR</span><span class="sxs-lookup"><span data-stu-id="2a61a-141">Write information to STDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="2a61a-142">Save files as ASCII with LF line endings</span><span class="sxs-lookup"><span data-stu-id="2a61a-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="2a61a-143">Use retry logic to recover from transient errors</span><span class="sxs-lookup"><span data-stu-id="2a61a-143">Use retry logic to recover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="2a61a-144">Script actions must complete within 60 minutes or the process fails.</span><span class="sxs-lookup"><span data-stu-id="2a61a-144">Script actions must complete within 60 minutes or the process fails.</span></span> <span data-ttu-id="2a61a-145">During node provisioning, the script runs concurrently with other setup and configuration processes.</span><span class="sxs-lookup"><span data-stu-id="2a61a-145">During node provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="2a61a-146">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span><span class="sxs-lookup"><span data-stu-id="2a61a-146">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>

### <a name="bPS1"></a><span data-ttu-id="2a61a-147">Target the Hadoop version</span><span class="sxs-lookup"><span data-stu-id="2a61a-147">Target the Hadoop version</span></span>

<span data-ttu-id="2a61a-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span><span class="sxs-lookup"><span data-stu-id="2a61a-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="2a61a-149">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span><span class="sxs-lookup"><span data-stu-id="2a61a-149">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span></span> <span data-ttu-id="2a61a-150">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="2a61a-150">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <a name="bps10"></a> <span data-ttu-id="2a61a-151">Target the OS version</span><span class="sxs-lookup"><span data-stu-id="2a61a-151">Target the OS version</span></span>

<span data-ttu-id="2a61a-152">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span><span class="sxs-lookup"><span data-stu-id="2a61a-152">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span></span> <span data-ttu-id="2a61a-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span><span class="sxs-lookup"><span data-stu-id="2a61a-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="2a61a-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span><span class="sxs-lookup"><span data-stu-id="2a61a-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="2a61a-155">Versions 3.5 and greater are based on Ubuntu 16.04, which uses Systemd.</span><span class="sxs-lookup"><span data-stu-id="2a61a-155">Versions 3.5 and greater are based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="2a61a-156">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span><span class="sxs-lookup"><span data-stu-id="2a61a-156">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span></span>

<span data-ttu-id="2a61a-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span><span class="sxs-lookup"><span data-stu-id="2a61a-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span></span>

<span data-ttu-id="2a61a-158">You can check the OS version by using `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-158">You can check the OS version by using `lsb_release`.</span></span> <span data-ttu-id="2a61a-159">The following code demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span><span class="sxs-lookup"><span data-stu-id="2a61a-159">The following code demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span></span>

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

<span data-ttu-id="2a61a-160">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="2a61a-160">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="2a61a-161">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="2a61a-161">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="2a61a-162">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="2a61a-162">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <a name="bPS2"></a><span data-ttu-id="2a61a-163">Provide stable links to script resources</span><span class="sxs-lookup"><span data-stu-id="2a61a-163">Provide stable links to script resources</span></span>

<span data-ttu-id="2a61a-164">The script and associated resources must remain available throughout the lifetime of the cluster.</span><span class="sxs-lookup"><span data-stu-id="2a61a-164">The script and associated resources must remain available throughout the lifetime of the cluster.</span></span> <span data-ttu-id="2a61a-165">These resources are required if new nodes are added to the cluster during scaling operations.</span><span class="sxs-lookup"><span data-stu-id="2a61a-165">These resources are required if new nodes are added to the cluster during scaling operations.</span></span>

<span data-ttu-id="2a61a-166">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span><span class="sxs-lookup"><span data-stu-id="2a61a-166">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a61a-167">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span><span class="sxs-lookup"><span data-stu-id="2a61a-167">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="2a61a-168">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span><span class="sxs-lookup"><span data-stu-id="2a61a-168">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="2a61a-169">This location is a public, read-only container maintained by the HDInsight team.</span><span class="sxs-lookup"><span data-stu-id="2a61a-169">This location is a public, read-only container maintained by the HDInsight team.</span></span>

### <a name="bPS4"></a><span data-ttu-id="2a61a-170">Use pre-compiled resources</span><span class="sxs-lookup"><span data-stu-id="2a61a-170">Use pre-compiled resources</span></span>

<span data-ttu-id="2a61a-171">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span><span class="sxs-lookup"><span data-stu-id="2a61a-171">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="2a61a-172">For example, pre-compile resources and store them in an Azure Storage account blob in the same data center as HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a61a-172">For example, pre-compile resources and store them in an Azure Storage account blob in the same data center as HDInsight.</span></span>

### <a name="bPS3"></a><span data-ttu-id="2a61a-173">Ensure that the cluster customization script is idempotent</span><span class="sxs-lookup"><span data-stu-id="2a61a-173">Ensure that the cluster customization script is idempotent</span></span>

<span data-ttu-id="2a61a-174">Scripts must be idempotent.</span><span class="sxs-lookup"><span data-stu-id="2a61a-174">Scripts must be idempotent.</span></span> <span data-ttu-id="2a61a-175">If the script runs multiple times, it should return the cluster to the same state every time.</span><span class="sxs-lookup"><span data-stu-id="2a61a-175">If the script runs multiple times, it should return the cluster to the same state every time.</span></span>

<span data-ttu-id="2a61a-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span><span class="sxs-lookup"><span data-stu-id="2a61a-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <a name="bPS5"></a><span data-ttu-id="2a61a-177">Ensure high availability of the cluster architecture</span><span class="sxs-lookup"><span data-stu-id="2a61a-177">Ensure high availability of the cluster architecture</span></span>

<span data-ttu-id="2a61a-178">Linux-based HDInsight clusters provide two head nodes that are active within the cluster, and script actions run on both nodes.</span><span class="sxs-lookup"><span data-stu-id="2a61a-178">Linux-based HDInsight clusters provide two head nodes that are active within the cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="2a61a-179">If the components you install expect only one head node, do not install the components on both head nodes.</span><span class="sxs-lookup"><span data-stu-id="2a61a-179">If the components you install expect only one head node, do not install the components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a61a-180">Services provided as part of HDInsight are designed to fail over between the two head nodes as needed.</span><span class="sxs-lookup"><span data-stu-id="2a61a-180">Services provided as part of HDInsight are designed to fail over between the two head nodes as needed.</span></span> <span data-ttu-id="2a61a-181">This functionality is not extended to custom components installed through script actions.</span><span class="sxs-lookup"><span data-stu-id="2a61a-181">This functionality is not extended to custom components installed through script actions.</span></span> <span data-ttu-id="2a61a-182">If you need high availability for custom components, you must implement your own failover mechanism.</span><span class="sxs-lookup"><span data-stu-id="2a61a-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <a name="bPS6"></a><span data-ttu-id="2a61a-183">Configure the custom components to use Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="2a61a-183">Configure the custom components to use Azure Blob storage</span></span>

<span data-ttu-id="2a61a-184">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span><span class="sxs-lookup"><span data-stu-id="2a61a-184">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="2a61a-185">HDInsight uses either Azure Storage or Data Lake Store as the default storage.</span><span class="sxs-lookup"><span data-stu-id="2a61a-185">HDInsight uses either Azure Storage or Data Lake Store as the default storage.</span></span> <span data-ttu-id="2a61a-186">Both provide an HDFS compatible file system that persists data even if the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="2a61a-186">Both provide an HDFS compatible file system that persists data even if the cluster is deleted.</span></span> <span data-ttu-id="2a61a-187">You may need to configure components you install to use WASB or ADL instead of HDFS.</span><span class="sxs-lookup"><span data-stu-id="2a61a-187">You may need to configure components you install to use WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="2a61a-188">For most operations, you do not need to specify the file system.</span><span class="sxs-lookup"><span data-stu-id="2a61a-188">For most operations, you do not need to specify the file system.</span></span> <span data-ttu-id="2a61a-189">For example, the following copies the giraph-examples.jar file from the local file system to cluster storage:</span><span class="sxs-lookup"><span data-stu-id="2a61a-189">For example, the following copies the giraph-examples.jar file from the local file system to cluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="2a61a-190">In this example, the `hdfs` command transparently uses the default cluster storage.</span><span class="sxs-lookup"><span data-stu-id="2a61a-190">In this example, the `hdfs` command transparently uses the default cluster storage.</span></span> <span data-ttu-id="2a61a-191">For some operations, you may need to specify the URI.</span><span class="sxs-lookup"><span data-stu-id="2a61a-191">For some operations, you may need to specify the URI.</span></span> <span data-ttu-id="2a61a-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2a61a-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <a name="bPS7"></a><span data-ttu-id="2a61a-193">Write information to STDOUT and STDERR</span><span class="sxs-lookup"><span data-stu-id="2a61a-193">Write information to STDOUT and STDERR</span></span>

<span data-ttu-id="2a61a-194">HDInsight logs script output that is written to STDOUT and STDERR.</span><span class="sxs-lookup"><span data-stu-id="2a61a-194">HDInsight logs script output that is written to STDOUT and STDERR.</span></span> <span data-ttu-id="2a61a-195">You can view this information using the Ambari web UI.</span><span class="sxs-lookup"><span data-stu-id="2a61a-195">You can view this information using the Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="2a61a-196">Ambari is only available if the cluster is successfully created.</span><span class="sxs-lookup"><span data-stu-id="2a61a-196">Ambari is only available if the cluster is successfully created.</span></span> <span data-ttu-id="2a61a-197">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span><span class="sxs-lookup"><span data-stu-id="2a61a-197">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="2a61a-198">Most utilities and installation packages already write information to STDOUT and STDERR, however you may want to add additional logging.</span><span class="sxs-lookup"><span data-stu-id="2a61a-198">Most utilities and installation packages already write information to STDOUT and STDERR, however you may want to add additional logging.</span></span> <span data-ttu-id="2a61a-199">To send text to STDOUT, use `echo`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-199">To send text to STDOUT, use `echo`.</span></span> <span data-ttu-id="2a61a-200">For example:</span><span class="sxs-lookup"><span data-stu-id="2a61a-200">For example:</span></span>

```bash
echo "Getting ready to install Foo"
```

<span data-ttu-id="2a61a-201">By default, `echo` sends the string to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="2a61a-201">By default, `echo` sends the string to STDOUT.</span></span> <span data-ttu-id="2a61a-202">To direct it to STDERR, add `>&2` before `echo`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-202">To direct it to STDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="2a61a-203">For example:</span><span class="sxs-lookup"><span data-stu-id="2a61a-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="2a61a-204">This redirects information written to STDOUT to STDERR (2) instead.</span><span class="sxs-lookup"><span data-stu-id="2a61a-204">This redirects information written to STDOUT to STDERR (2) instead.</span></span> <span data-ttu-id="2a61a-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="2a61a-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="2a61a-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="2a61a-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <a name="bps8"></a> <span data-ttu-id="2a61a-207">Save files as ASCII with LF line endings</span><span class="sxs-lookup"><span data-stu-id="2a61a-207">Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="2a61a-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span><span class="sxs-lookup"><span data-stu-id="2a61a-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="2a61a-209">Files that are stored as UTF-8, or use CRLF as the line ending may fail with the following error:</span><span class="sxs-lookup"><span data-stu-id="2a61a-209">Files that are stored as UTF-8, or use CRLF as the line ending may fail with the following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a> <span data-ttu-id="2a61a-210">Use retry logic to recover from transient errors</span><span class="sxs-lookup"><span data-stu-id="2a61a-210">Use retry logic to recover from transient errors</span></span>

<span data-ttu-id="2a61a-211">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span><span class="sxs-lookup"><span data-stu-id="2a61a-211">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span></span> <span data-ttu-id="2a61a-212">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span><span class="sxs-lookup"><span data-stu-id="2a61a-212">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span></span>

<span data-ttu-id="2a61a-213">To make your script resilient to transient errors, you can implement retry logic.</span><span class="sxs-lookup"><span data-stu-id="2a61a-213">To make your script resilient to transient errors, you can implement retry logic.</span></span> <span data-ttu-id="2a61a-214">The following function demonstrates how to implement retry logic.</span><span class="sxs-lookup"><span data-stu-id="2a61a-214">The following function demonstrates how to implement retry logic.</span></span> <span data-ttu-id="2a61a-215">It retries the operation three times before failing.</span><span class="sxs-lookup"><span data-stu-id="2a61a-215">It retries the operation three times before failing.</span></span>

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

<span data-ttu-id="2a61a-216">The following examples demonstrate how to use this function.</span><span class="sxs-lookup"><span data-stu-id="2a61a-216">The following examples demonstrate how to use this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a><span data-ttu-id="2a61a-217">Helper methods for custom scripts</span><span class="sxs-lookup"><span data-stu-id="2a61a-217">Helper methods for custom scripts</span></span>

<span data-ttu-id="2a61a-218">Script action helper methods are utilities that you can use while writing custom scripts.</span><span class="sxs-lookup"><span data-stu-id="2a61a-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="2a61a-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span><span class="sxs-lookup"><span data-stu-id="2a61a-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="2a61a-220">Use the following to download and use them as part of your script:</span><span class="sxs-lookup"><span data-stu-id="2a61a-220">Use the following to download and use them as part of your script:</span></span>

```bash
# Import the helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="2a61a-221">The following helpers available for use in your script:</span><span class="sxs-lookup"><span data-stu-id="2a61a-221">The following helpers available for use in your script:</span></span>

| <span data-ttu-id="2a61a-222">Helper usage</span><span class="sxs-lookup"><span data-stu-id="2a61a-222">Helper usage</span></span> | <span data-ttu-id="2a61a-223">Description</span><span class="sxs-lookup"><span data-stu-id="2a61a-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="2a61a-224">Downloads a file from the source URI to the specified file path.</span><span class="sxs-lookup"><span data-stu-id="2a61a-224">Downloads a file from the source URI to the specified file path.</span></span> <span data-ttu-id="2a61a-225">By default, it does not overwrite an existing file.</span><span class="sxs-lookup"><span data-stu-id="2a61a-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="2a61a-226">Extracts a tar file (using `-xf`) to the destination directory.</span><span class="sxs-lookup"><span data-stu-id="2a61a-226">Extracts a tar file (using `-xf`) to the destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="2a61a-227">If ran on a cluster head node, return 1; otherwise, 0.</span><span class="sxs-lookup"><span data-stu-id="2a61a-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="2a61a-228">If the current node is a data (worker) node, return a 1; otherwise, 0.</span><span class="sxs-lookup"><span data-stu-id="2a61a-228">If the current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="2a61a-229">If the current node is the first data (worker) node (named workernode0) return a 1; otherwise, 0.</span><span class="sxs-lookup"><span data-stu-id="2a61a-229">If the current node is the first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="2a61a-230">Return the fully qualified domain name of the headnodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="2a61a-230">Return the fully qualified domain name of the headnodes in the cluster.</span></span> <span data-ttu-id="2a61a-231">Names are comma delimited.</span><span class="sxs-lookup"><span data-stu-id="2a61a-231">Names are comma delimited.</span></span> <span data-ttu-id="2a61a-232">An empty string is returned on error.</span><span class="sxs-lookup"><span data-stu-id="2a61a-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="2a61a-233">Gets the fully qualified domain name of the primary headnode.</span><span class="sxs-lookup"><span data-stu-id="2a61a-233">Gets the fully qualified domain name of the primary headnode.</span></span> <span data-ttu-id="2a61a-234">An empty string is returned on error.</span><span class="sxs-lookup"><span data-stu-id="2a61a-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="2a61a-235">Gets the fully qualified domain name of the secondary headnode.</span><span class="sxs-lookup"><span data-stu-id="2a61a-235">Gets the fully qualified domain name of the secondary headnode.</span></span> <span data-ttu-id="2a61a-236">An empty string is returned on error.</span><span class="sxs-lookup"><span data-stu-id="2a61a-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="2a61a-237">Gets the numeric suffix of the primary headnode.</span><span class="sxs-lookup"><span data-stu-id="2a61a-237">Gets the numeric suffix of the primary headnode.</span></span> <span data-ttu-id="2a61a-238">An empty string is returned on error.</span><span class="sxs-lookup"><span data-stu-id="2a61a-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="2a61a-239">Gets the numeric suffix of the secondary headnode.</span><span class="sxs-lookup"><span data-stu-id="2a61a-239">Gets the numeric suffix of the secondary headnode.</span></span> <span data-ttu-id="2a61a-240">An empty string is returned on error.</span><span class="sxs-lookup"><span data-stu-id="2a61a-240">An empty string is returned on error.</span></span> |

## <a name="commonusage"></a><span data-ttu-id="2a61a-241">Common usage patterns</span><span class="sxs-lookup"><span data-stu-id="2a61a-241">Common usage patterns</span></span>

<span data-ttu-id="2a61a-242">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span><span class="sxs-lookup"><span data-stu-id="2a61a-242">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-to-a-script"></a><span data-ttu-id="2a61a-243">Passing parameters to a script</span><span class="sxs-lookup"><span data-stu-id="2a61a-243">Passing parameters to a script</span></span>

<span data-ttu-id="2a61a-244">In some cases, your script may require parameters.</span><span class="sxs-lookup"><span data-stu-id="2a61a-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="2a61a-245">For example, you may need the admin password for the cluster when using the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="2a61a-245">For example, you may need the admin password for the cluster when using the Ambari REST API.</span></span>

<span data-ttu-id="2a61a-246">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span><span class="sxs-lookup"><span data-stu-id="2a61a-246">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span></span> <span data-ttu-id="2a61a-247">`$0` contains the name of the script itself.</span><span class="sxs-lookup"><span data-stu-id="2a61a-247">`$0` contains the name of the script itself.</span></span>

<span data-ttu-id="2a61a-248">Values passed to the script as parameters should be enclosed by single quotes (').</span><span class="sxs-lookup"><span data-stu-id="2a61a-248">Values passed to the script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="2a61a-249">Doing so ensures that the passed value is treated as a literal.</span><span class="sxs-lookup"><span data-stu-id="2a61a-249">Doing so ensures that the passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="2a61a-250">Setting environment variables</span><span class="sxs-lookup"><span data-stu-id="2a61a-250">Setting environment variables</span></span>

<span data-ttu-id="2a61a-251">Setting an environment variable is performed by the following statement:</span><span class="sxs-lookup"><span data-stu-id="2a61a-251">Setting an environment variable is performed by the following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="2a61a-252">Where VARIABLENAME is the name of the variable.</span><span class="sxs-lookup"><span data-stu-id="2a61a-252">Where VARIABLENAME is the name of the variable.</span></span> <span data-ttu-id="2a61a-253">To access the variable, use `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-253">To access the variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="2a61a-254">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following statement:</span><span class="sxs-lookup"><span data-stu-id="2a61a-254">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="2a61a-255">Subsequent access to the information could then use `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-255">Subsequent access to the information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="2a61a-256">Environment variables set within the script only exist within the scope of the script.</span><span class="sxs-lookup"><span data-stu-id="2a61a-256">Environment variables set within the script only exist within the scope of the script.</span></span> <span data-ttu-id="2a61a-257">In some cases, you may need to add system-wide environment variables that will persist after the script has finished.</span><span class="sxs-lookup"><span data-stu-id="2a61a-257">In some cases, you may need to add system-wide environment variables that will persist after the script has finished.</span></span> <span data-ttu-id="2a61a-258">To add system-wide environment variables, add the variable to `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-258">To add system-wide environment variables, add the variable to `/etc/environment`.</span></span> <span data-ttu-id="2a61a-259">For example, the following statement adds `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="2a61a-259">For example, the following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="2a61a-260">Access to locations where the custom scripts are stored</span><span class="sxs-lookup"><span data-stu-id="2a61a-260">Access to locations where the custom scripts are stored</span></span>

<span data-ttu-id="2a61a-261">Scripts used to customize a cluster needs to be stored in one of the following locations:</span><span class="sxs-lookup"><span data-stu-id="2a61a-261">Scripts used to customize a cluster needs to be stored in one of the following locations:</span></span>

* <span data-ttu-id="2a61a-262">An __Azure Storage account__ that is associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="2a61a-262">An __Azure Storage account__ that is associated with the cluster.</span></span>

* <span data-ttu-id="2a61a-263">An __additional storage account__ associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="2a61a-263">An __additional storage account__ associated with the cluster.</span></span>

* <span data-ttu-id="2a61a-264">A __publicly readable URI__.</span><span class="sxs-lookup"><span data-stu-id="2a61a-264">A __publicly readable URI__.</span></span> <span data-ttu-id="2a61a-265">For example, a URL to data stored on OneDrive, Dropbox, or other file hosting service.</span><span class="sxs-lookup"><span data-stu-id="2a61a-265">For example, a URL to data stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="2a61a-266">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="2a61a-266">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span></span> <span data-ttu-id="2a61a-267">For more information on using Azure Data Lake Store with HDInsight, see [Quickstart: Set up clusters in HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="2a61a-267">For more information on using Azure Data Lake Store with HDInsight, see [Quickstart: Set up clusters in HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="2a61a-268">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span><span class="sxs-lookup"><span data-stu-id="2a61a-268">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

<span data-ttu-id="2a61a-269">Resources used by the script must also be publicly available.</span><span class="sxs-lookup"><span data-stu-id="2a61a-269">Resources used by the script must also be publicly available.</span></span>

<span data-ttu-id="2a61a-270">Storing the files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within the Azure network.</span><span class="sxs-lookup"><span data-stu-id="2a61a-270">Storing the files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within the Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="2a61a-271">The URI format used to reference the script differs depending on the service being used.</span><span class="sxs-lookup"><span data-stu-id="2a61a-271">The URI format used to reference the script differs depending on the service being used.</span></span> <span data-ttu-id="2a61a-272">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-272">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="2a61a-273">For publicly readable URIs, use `http://` or `https://`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="2a61a-274">For Data Lake Store, use `adl://`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-the-operating-system-version"></a><span data-ttu-id="2a61a-275">Checking the operating system version</span><span class="sxs-lookup"><span data-stu-id="2a61a-275">Checking the operating system version</span></span>

<span data-ttu-id="2a61a-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2a61a-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="2a61a-277">There may be differences between OS versions that you must check for in your script.</span><span class="sxs-lookup"><span data-stu-id="2a61a-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="2a61a-278">For example, you may need to install a binary that is tied to the version of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2a61a-278">For example, you may need to install a binary that is tied to the version of Ubuntu.</span></span>

<span data-ttu-id="2a61a-279">To check the OS version, use `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-279">To check the OS version, use `lsb_release`.</span></span> <span data-ttu-id="2a61a-280">For example, the following script demonstrates how to reference a specific tar file depending on the OS version:</span><span class="sxs-lookup"><span data-stu-id="2a61a-280">For example, the following script demonstrates how to reference a specific tar file depending on the OS version:</span></span>

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

## <a name="deployScript"></a><span data-ttu-id="2a61a-281">Checklist for deploying a script action</span><span class="sxs-lookup"><span data-stu-id="2a61a-281">Checklist for deploying a script action</span></span>

<span data-ttu-id="2a61a-282">Here are the steps take when preparing to deploy a script:</span><span class="sxs-lookup"><span data-stu-id="2a61a-282">Here are the steps take when preparing to deploy a script:</span></span>

* <span data-ttu-id="2a61a-283">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span><span class="sxs-lookup"><span data-stu-id="2a61a-283">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="2a61a-284">For example, the default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="2a61a-284">For example, the default storage for the cluster.</span></span> <span data-ttu-id="2a61a-285">Files can also be stored in publicly readable hosting services.</span><span class="sxs-lookup"><span data-stu-id="2a61a-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="2a61a-286">Verify that the script is idempotent.</span><span class="sxs-lookup"><span data-stu-id="2a61a-286">Verify that the script is idempotent.</span></span> <span data-ttu-id="2a61a-287">Doing so allows the script to be executed multiple times on the same node.</span><span class="sxs-lookup"><span data-stu-id="2a61a-287">Doing so allows the script to be executed multiple times on the same node.</span></span>
* <span data-ttu-id="2a61a-288">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span><span class="sxs-lookup"><span data-stu-id="2a61a-288">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="2a61a-289">If OS-level settings or Hadoop service configuration files are changed, you may want to restart HDInsight services.</span><span class="sxs-lookup"><span data-stu-id="2a61a-289">If OS-level settings or Hadoop service configuration files are changed, you may want to restart HDInsight services.</span></span>

## <a name="runScriptAction"></a><span data-ttu-id="2a61a-290">How to run a script action</span><span class="sxs-lookup"><span data-stu-id="2a61a-290">How to run a script action</span></span>

<span data-ttu-id="2a61a-291">You can use script actions to customize HDInsight clusters using the following methods:</span><span class="sxs-lookup"><span data-stu-id="2a61a-291">You can use script actions to customize HDInsight clusters using the following methods:</span></span>

* <span data-ttu-id="2a61a-292">Azure portal</span><span class="sxs-lookup"><span data-stu-id="2a61a-292">Azure portal</span></span>
* <span data-ttu-id="2a61a-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a61a-293">Azure PowerShell</span></span>
* <span data-ttu-id="2a61a-294">Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="2a61a-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="2a61a-295">The HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2a61a-295">The HDInsight .NET SDK.</span></span>

<span data-ttu-id="2a61a-296">For more information on using each method, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2a61a-296">For more information on using each method, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="sampleScripts"></a><span data-ttu-id="2a61a-297">Custom script samples</span><span class="sxs-lookup"><span data-stu-id="2a61a-297">Custom script samples</span></span>

<span data-ttu-id="2a61a-298">Microsoft provides sample scripts to install components on an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="2a61a-298">Microsoft provides sample scripts to install components on an HDInsight cluster.</span></span> <span data-ttu-id="2a61a-299">See the following links for more example script actions.</span><span class="sxs-lookup"><span data-stu-id="2a61a-299">See the following links for more example script actions.</span></span>

* [<span data-ttu-id="2a61a-300">Install and use Hue on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="2a61a-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="2a61a-301">Install and use Solr on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="2a61a-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="2a61a-302">Install and use Giraph on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="2a61a-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="2a61a-303">Install or upgrade Mono on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="2a61a-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="2a61a-304">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="2a61a-304">Troubleshooting</span></span>

<span data-ttu-id="2a61a-305">The following are errors you may encounter when using scripts you have developed:</span><span class="sxs-lookup"><span data-stu-id="2a61a-305">The following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="2a61a-306">**Error**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="2a61a-307">Sometimes followed by `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="2a61a-308">*Cause*: This error is caused when the lines in a script end with CRLF.</span><span class="sxs-lookup"><span data-stu-id="2a61a-308">*Cause*: This error is caused when the lines in a script end with CRLF.</span></span> <span data-ttu-id="2a61a-309">Unix systems expect only LF as the line ending.</span><span class="sxs-lookup"><span data-stu-id="2a61a-309">Unix systems expect only LF as the line ending.</span></span>

<span data-ttu-id="2a61a-310">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span><span class="sxs-lookup"><span data-stu-id="2a61a-310">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="2a61a-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span><span class="sxs-lookup"><span data-stu-id="2a61a-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span></span> <span data-ttu-id="2a61a-312">You may also use the following commands on a Unix system to change the CRLF to an LF:</span><span class="sxs-lookup"><span data-stu-id="2a61a-312">You may also use the following commands on a Unix system to change the CRLF to an LF:</span></span>

> [!NOTE]
> <span data-ttu-id="2a61a-313">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span><span class="sxs-lookup"><span data-stu-id="2a61a-313">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span></span> <span data-ttu-id="2a61a-314">Select one based on the utilities available on your system.</span><span class="sxs-lookup"><span data-stu-id="2a61a-314">Select one based on the utilities available on your system.</span></span>

| <span data-ttu-id="2a61a-315">Command</span><span class="sxs-lookup"><span data-stu-id="2a61a-315">Command</span></span> | <span data-ttu-id="2a61a-316">Notes</span><span class="sxs-lookup"><span data-stu-id="2a61a-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="2a61a-317">The original file is backed up with a .BAK extension</span><span class="sxs-lookup"><span data-stu-id="2a61a-317">The original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="2a61a-318">OUTFILE contains a version with only LF endings</span><span class="sxs-lookup"><span data-stu-id="2a61a-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="2a61a-319">Modifies the file directly</span><span class="sxs-lookup"><span data-stu-id="2a61a-319">Modifies the file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="2a61a-320">OUTFILE contains a version with only LF endings.</span><span class="sxs-lookup"><span data-stu-id="2a61a-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="2a61a-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="2a61a-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="2a61a-322">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span><span class="sxs-lookup"><span data-stu-id="2a61a-322">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="2a61a-323">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span><span class="sxs-lookup"><span data-stu-id="2a61a-323">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="2a61a-324">You may also use the following command on a Linux or Unix system to create a file without the BOM:</span><span class="sxs-lookup"><span data-stu-id="2a61a-324">You may also use the following command on a Linux or Unix system to create a file without the BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="2a61a-325">Replace `INFILE` with the file containing the BOM.</span><span class="sxs-lookup"><span data-stu-id="2a61a-325">Replace `INFILE` with the file containing the BOM.</span></span> <span data-ttu-id="2a61a-326">`OUTFILE` should be a new file name, which contains the script without the BOM.</span><span class="sxs-lookup"><span data-stu-id="2a61a-326">`OUTFILE` should be a new file name, which contains the script without the BOM.</span></span>

## <a name="seeAlso"></a><span data-ttu-id="2a61a-327">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a61a-327">Next steps</span></span>

* <span data-ttu-id="2a61a-328">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="2a61a-328">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="2a61a-329">Use the [HDInsight .NET SDK reference](https://docs.microsoft.com/dotnet/api/overview/azure/hdinsight) to learn more about creating .NET applications that manage HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a61a-329">Use the [HDInsight .NET SDK reference](https://docs.microsoft.com/dotnet/api/overview/azure/hdinsight) to learn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="2a61a-330">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="2a61a-330">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span></span>
