---
title: Tips for using Hadoop on Linux-based HDInsight - Azure | Microsoft Docs
description: Get implementation tips for using Linux-based HDInsight (Hadoop) clusters on a familiar Linux environment running in the Azure cloud.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/02/2017
ms.author: larryfr
ms.openlocfilehash: 79e122beb0f31c46bbb9951a2dee223de4a77e1f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552908"
---
# <a name="information-about-using-hdinsight-on-linux"></a><span data-ttu-id="250f9-103">Information about using HDInsight on Linux</span><span class="sxs-lookup"><span data-stu-id="250f9-103">Information about using HDInsight on Linux</span></span>

<span data-ttu-id="250f9-104">Azure HDInsight clusters provide Hadoop on a familiar Linux environment, running in the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="250f9-104">Azure HDInsight clusters provide Hadoop on a familiar Linux environment, running in the Azure cloud.</span></span> <span data-ttu-id="250f9-105">For most things, it should work exactly as any other Hadoop-on-Linux installation.</span><span class="sxs-lookup"><span data-stu-id="250f9-105">For most things, it should work exactly as any other Hadoop-on-Linux installation.</span></span> <span data-ttu-id="250f9-106">This document calls out specific differences that you should be aware of.</span><span class="sxs-lookup"><span data-stu-id="250f9-106">This document calls out specific differences that you should be aware of.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="250f9-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="250f9-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="250f9-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="250f9-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="250f9-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="250f9-109">Prerequisites</span></span>

<span data-ttu-id="250f9-110">Many of the steps in this document use the following utilities, which may need to be installed on your system.</span><span class="sxs-lookup"><span data-stu-id="250f9-110">Many of the steps in this document use the following utilities, which may need to be installed on your system.</span></span>

* <span data-ttu-id="250f9-111">[cURL](https://curl.haxx.se/) - used to communicate with web-based services</span><span class="sxs-lookup"><span data-stu-id="250f9-111">[cURL](https://curl.haxx.se/) - used to communicate with web-based services</span></span>
* <span data-ttu-id="250f9-112">[jq](https://stedolan.github.io/jq/) - used to parse JSON documents</span><span class="sxs-lookup"><span data-stu-id="250f9-112">[jq](https://stedolan.github.io/jq/) - used to parse JSON documents</span></span>
* <span data-ttu-id="250f9-113">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (preview) - used to remotely manage Azure services</span><span class="sxs-lookup"><span data-stu-id="250f9-113">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (preview) - used to remotely manage Azure services</span></span>

## <a name="users"></a><span data-ttu-id="250f9-114">Users</span><span class="sxs-lookup"><span data-stu-id="250f9-114">Users</span></span>

<span data-ttu-id="250f9-115">Unless [domain-joined](hdinsight-domain-joined-introduction.md), HDInsight should be considered a **single-user** system.</span><span class="sxs-lookup"><span data-stu-id="250f9-115">Unless [domain-joined](hdinsight-domain-joined-introduction.md), HDInsight should be considered a **single-user** system.</span></span> <span data-ttu-id="250f9-116">A single SSH user account is created with the cluster, with administrator level permissions.</span><span class="sxs-lookup"><span data-stu-id="250f9-116">A single SSH user account is created with the cluster, with administrator level permissions.</span></span> <span data-ttu-id="250f9-117">Additional SSH accounts can be created, but they also have administrator access to the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-117">Additional SSH accounts can be created, but they also have administrator access to the cluster.</span></span>

<span data-ttu-id="250f9-118">Domain-joined HDInsight supports multiple users and more granular permission and role settings.</span><span class="sxs-lookup"><span data-stu-id="250f9-118">Domain-joined HDInsight supports multiple users and more granular permission and role settings.</span></span> <span data-ttu-id="250f9-119">For more information, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="250f9-119">For more information, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="domain-names"></a><span data-ttu-id="250f9-120">Domain names</span><span class="sxs-lookup"><span data-stu-id="250f9-120">Domain names</span></span>

<span data-ttu-id="250f9-121">The fully qualified domain name (FQDN) to use when connecting to the cluster from the internet is **&lt;clustername>.azurehdinsight.net** or (for SSH only) **&lt;clustername-ssh>.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="250f9-121">The fully qualified domain name (FQDN) to use when connecting to the cluster from the internet is **&lt;clustername>.azurehdinsight.net** or (for SSH only) **&lt;clustername-ssh>.azurehdinsight.net**.</span></span>

<span data-ttu-id="250f9-122">Internally, each node in the cluster has a name that is assigned during cluster configuration.</span><span class="sxs-lookup"><span data-stu-id="250f9-122">Internally, each node in the cluster has a name that is assigned during cluster configuration.</span></span> <span data-ttu-id="250f9-123">To find the cluster names, see the **Hosts** page on the Ambari Web UI.</span><span class="sxs-lookup"><span data-stu-id="250f9-123">To find the cluster names, see the **Hosts** page on the Ambari Web UI.</span></span> <span data-ttu-id="250f9-124">You can also use the following to return a list of hosts from the Ambari REST API:</span><span class="sxs-lookup"><span data-stu-id="250f9-124">You can also use the following to return a list of hosts from the Ambari REST API:</span></span>

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

<span data-ttu-id="250f9-125">Replace **PASSWORD** with the password of the admin account, and **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-125">Replace **PASSWORD** with the password of the admin account, and **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="250f9-126">This command returns a JSON document that contains a list of the hosts in the cluster, then jq pulls out the `host_name` element value for each host in the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-126">This command returns a JSON document that contains a list of the hosts in the cluster, then jq pulls out the `host_name` element value for each host in the cluster.</span></span>

<span data-ttu-id="250f9-127">If you need to find the name of the node for a specific service, you can query Ambari for that component.</span><span class="sxs-lookup"><span data-stu-id="250f9-127">If you need to find the name of the node for a specific service, you can query Ambari for that component.</span></span> <span data-ttu-id="250f9-128">For example, to find the hosts for the HDFS name node, use the following command:</span><span class="sxs-lookup"><span data-stu-id="250f9-128">For example, to find the hosts for the HDFS name node, use the following command:</span></span>

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

<span data-ttu-id="250f9-129">This command returns a JSON document describing the service, and then jq pulls out only the `host_name` value for the hosts.</span><span class="sxs-lookup"><span data-stu-id="250f9-129">This command returns a JSON document describing the service, and then jq pulls out only the `host_name` value for the hosts.</span></span>

## <a name="remote-access-to-services"></a><span data-ttu-id="250f9-130">Remote access to services</span><span class="sxs-lookup"><span data-stu-id="250f9-130">Remote access to services</span></span>

* <span data-ttu-id="250f9-131">**Ambari (web)** - https://&lt;clustername>.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="250f9-131">**Ambari (web)** - https://&lt;clustername>.azurehdinsight.net</span></span>

    <span data-ttu-id="250f9-132">Authenticate by using the cluster administrator user and password, and then log in to Ambari.</span><span class="sxs-lookup"><span data-stu-id="250f9-132">Authenticate by using the cluster administrator user and password, and then log in to Ambari.</span></span> <span data-ttu-id="250f9-133">You must authenticate using the cluster administrator user and password.</span><span class="sxs-lookup"><span data-stu-id="250f9-133">You must authenticate using the cluster administrator user and password.</span></span>

    <span data-ttu-id="250f9-134">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span><span class="sxs-lookup"><span data-stu-id="250f9-134">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="250f9-135">While Ambari for your cluster is accessible directly over the Internet, some functionality relies on accessing nodes by the internal domain name used by the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-135">While Ambari for your cluster is accessible directly over the Internet, some functionality relies on accessing nodes by the internal domain name used by the cluster.</span></span> <span data-ttu-id="250f9-136">Since internal domain name are not publicly accessible, you may receive "server not found" errors when trying to access some features over the Internet.</span><span class="sxs-lookup"><span data-stu-id="250f9-136">Since internal domain name are not publicly accessible, you may receive "server not found" errors when trying to access some features over the Internet.</span></span>
    >
    > <span data-ttu-id="250f9-137">To use the full functionality of the Ambari web UI, use an SSH tunnel to proxy web traffic to the cluster head node.</span><span class="sxs-lookup"><span data-stu-id="250f9-137">To use the full functionality of the Ambari web UI, use an SSH tunnel to proxy web traffic to the cluster head node.</span></span> <span data-ttu-id="250f9-138">See [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="250f9-138">See [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

* <span data-ttu-id="250f9-139">**Ambari (REST)** - https://&lt;clustername>.azurehdinsight.net/ambari</span><span class="sxs-lookup"><span data-stu-id="250f9-139">**Ambari (REST)** - https://&lt;clustername>.azurehdinsight.net/ambari</span></span>

    > [!NOTE]
    > <span data-ttu-id="250f9-140">Authenticate by using the cluster administrator user and password.</span><span class="sxs-lookup"><span data-stu-id="250f9-140">Authenticate by using the cluster administrator user and password.</span></span>
    >
    > <span data-ttu-id="250f9-141">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span><span class="sxs-lookup"><span data-stu-id="250f9-141">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span></span>

* <span data-ttu-id="250f9-142">**WebHCat (Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton</span><span class="sxs-lookup"><span data-stu-id="250f9-142">**WebHCat (Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton</span></span>

    > [!NOTE]
    > <span data-ttu-id="250f9-143">Authenticate by using the cluster administrator user and password.</span><span class="sxs-lookup"><span data-stu-id="250f9-143">Authenticate by using the cluster administrator user and password.</span></span>
    >
    > <span data-ttu-id="250f9-144">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span><span class="sxs-lookup"><span data-stu-id="250f9-144">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span></span>

* <span data-ttu-id="250f9-145">**SSH** - &lt;clustername>-ssh.azurehdinsight.net on port 22 or 23.</span><span class="sxs-lookup"><span data-stu-id="250f9-145">**SSH** - &lt;clustername>-ssh.azurehdinsight.net on port 22 or 23.</span></span> <span data-ttu-id="250f9-146">Port 22 is used to connect to the primary headnode, while 23 is used to connect to the secondary.</span><span class="sxs-lookup"><span data-stu-id="250f9-146">Port 22 is used to connect to the primary headnode, while 23 is used to connect to the secondary.</span></span> <span data-ttu-id="250f9-147">For more information on the head nodes, see [Availability and reliability of Hadoop clusters in HDInsight](hdinsight-high-availability-linux.md).</span><span class="sxs-lookup"><span data-stu-id="250f9-147">For more information on the head nodes, see [Availability and reliability of Hadoop clusters in HDInsight](hdinsight-high-availability-linux.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="250f9-148">You can only access the cluster head nodes through SSH from a client machine.</span><span class="sxs-lookup"><span data-stu-id="250f9-148">You can only access the cluster head nodes through SSH from a client machine.</span></span> <span data-ttu-id="250f9-149">Once connected, you can then access the worker nodes by using SSH from a headnode.</span><span class="sxs-lookup"><span data-stu-id="250f9-149">Once connected, you can then access the worker nodes by using SSH from a headnode.</span></span>

## <a name="file-locations"></a><span data-ttu-id="250f9-150">File locations</span><span class="sxs-lookup"><span data-stu-id="250f9-150">File locations</span></span>

<span data-ttu-id="250f9-151">Hadoop-related files can be found on the cluster nodes at `/usr/hdp`.</span><span class="sxs-lookup"><span data-stu-id="250f9-151">Hadoop-related files can be found on the cluster nodes at `/usr/hdp`.</span></span> <span data-ttu-id="250f9-152">This directory contains the following subdirectories:</span><span class="sxs-lookup"><span data-stu-id="250f9-152">This directory contains the following subdirectories:</span></span>

* <span data-ttu-id="250f9-153">**2.2.4.9-1**: This directory is named for the version of the Hortonworks Data Platform used by HDInsight, so the number on your cluster may be different than the one listed here.</span><span class="sxs-lookup"><span data-stu-id="250f9-153">**2.2.4.9-1**: This directory is named for the version of the Hortonworks Data Platform used by HDInsight, so the number on your cluster may be different than the one listed here.</span></span>
* <span data-ttu-id="250f9-154">**current**: This directory contains links to sub-directories under the **2.2.4.9-1** directory.</span><span class="sxs-lookup"><span data-stu-id="250f9-154">**current**: This directory contains links to sub-directories under the **2.2.4.9-1** directory.</span></span> <span data-ttu-id="250f9-155">This directory exists so that you don't have to type a version number (which might change) every time you want to access a file.</span><span class="sxs-lookup"><span data-stu-id="250f9-155">This directory exists so that you don't have to type a version number (which might change) every time you want to access a file.</span></span>

<span data-ttu-id="250f9-156">Example data and JAR files can be found on Hadoop Distributed File System at `/example` and `/HdiSamples`</span><span class="sxs-lookup"><span data-stu-id="250f9-156">Example data and JAR files can be found on Hadoop Distributed File System at `/example` and `/HdiSamples`</span></span>

## <a name="hdfs-azure-storage-and-data-lake-store"></a><span data-ttu-id="250f9-157">HDFS, Azure Storage, and Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="250f9-157">HDFS, Azure Storage, and Data Lake Store</span></span>

<span data-ttu-id="250f9-158">In most Hadoop distributions, HDFS is backed by local storage on the machines in the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-158">In most Hadoop distributions, HDFS is backed by local storage on the machines in the cluster.</span></span> <span data-ttu-id="250f9-159">While using local storage is efficient, it can be costly for a cloud-based solution where you are charged hourly or by minute for compute resources.</span><span class="sxs-lookup"><span data-stu-id="250f9-159">While using local storage is efficient, it can be costly for a cloud-based solution where you are charged hourly or by minute for compute resources.</span></span>

<span data-ttu-id="250f9-160">HDInsight uses either blobs in Azure Storage or Azure Data Lake Store as the default store.</span><span class="sxs-lookup"><span data-stu-id="250f9-160">HDInsight uses either blobs in Azure Storage or Azure Data Lake Store as the default store.</span></span> <span data-ttu-id="250f9-161">These services provide the following benefits:</span><span class="sxs-lookup"><span data-stu-id="250f9-161">These services provide the following benefits:</span></span>

* <span data-ttu-id="250f9-162">Cheap long-term storage</span><span class="sxs-lookup"><span data-stu-id="250f9-162">Cheap long-term storage</span></span>
* <span data-ttu-id="250f9-163">Accessibility from external services such as websites, file upload/download utilities, various language SDKs, and web browsers</span><span class="sxs-lookup"><span data-stu-id="250f9-163">Accessibility from external services such as websites, file upload/download utilities, various language SDKs, and web browsers</span></span>

> [!WARNING]
> <span data-ttu-id="250f9-164">HDInsight only supports __General purpose__ Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="250f9-164">HDInsight only supports __General purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="250f9-165">It does not currently support the __Blob storage__ account type.</span><span class="sxs-lookup"><span data-stu-id="250f9-165">It does not currently support the __Blob storage__ account type.</span></span>

<span data-ttu-id="250f9-166">An Azure Storage account can hold up to 4.75 TB, though individual blobs (or files from an HDInsight perspective) can only go up to 195 GB.</span><span class="sxs-lookup"><span data-stu-id="250f9-166">An Azure Storage account can hold up to 4.75 TB, though individual blobs (or files from an HDInsight perspective) can only go up to 195 GB.</span></span> <span data-ttu-id="250f9-167">Azure Data Lake Store can grow dynamically to hold trillions of files, with individual files greater than a petabyte.</span><span class="sxs-lookup"><span data-stu-id="250f9-167">Azure Data Lake Store can grow dynamically to hold trillions of files, with individual files greater than a petabyte.</span></span> <span data-ttu-id="250f9-168">For more information, see [Understanding blobs](https://docs.microsoft.com/rest/api/storageservices/fileservices/understanding-block-blobs--append-blobs--and-page-blobs) and [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="250f9-168">For more information, see [Understanding blobs](https://docs.microsoft.com/rest/api/storageservices/fileservices/understanding-block-blobs--append-blobs--and-page-blobs) and [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span>

<span data-ttu-id="250f9-169">When using either Azure Storage or Data Lake Store, you don't have to do anything special from HDInsight to access the data.</span><span class="sxs-lookup"><span data-stu-id="250f9-169">When using either Azure Storage or Data Lake Store, you don't have to do anything special from HDInsight to access the data.</span></span> <span data-ttu-id="250f9-170">For example, the following command lists files in the `/example/data` folder regardless of whether it is stored on Azure Storage or Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="250f9-170">For example, the following command lists files in the `/example/data` folder regardless of whether it is stored on Azure Storage or Data Lake Store:</span></span>

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a><span data-ttu-id="250f9-171">URI and scheme</span><span class="sxs-lookup"><span data-stu-id="250f9-171">URI and scheme</span></span>

<span data-ttu-id="250f9-172">Some commands may require you to specify the scheme as part of the URI when accessing a file.</span><span class="sxs-lookup"><span data-stu-id="250f9-172">Some commands may require you to specify the scheme as part of the URI when accessing a file.</span></span> <span data-ttu-id="250f9-173">For example, the Storm-HDFS component requires you to specify the scheme.</span><span class="sxs-lookup"><span data-stu-id="250f9-173">For example, the Storm-HDFS component requires you to specify the scheme.</span></span> <span data-ttu-id="250f9-174">When using non-default storage (storage added as "additional" storage to the cluster), you must always use the scheme as part of the URI.</span><span class="sxs-lookup"><span data-stu-id="250f9-174">When using non-default storage (storage added as "additional" storage to the cluster), you must always use the scheme as part of the URI.</span></span>

<span data-ttu-id="250f9-175">When using __Azure Storage__, use one of the following URI schemes:</span><span class="sxs-lookup"><span data-stu-id="250f9-175">When using __Azure Storage__, use one of the following URI schemes:</span></span>

* <span data-ttu-id="250f9-176">`wasb:///`: Access default storage using unencrypted communication.</span><span class="sxs-lookup"><span data-stu-id="250f9-176">`wasb:///`: Access default storage using unencrypted communication.</span></span>

* <span data-ttu-id="250f9-177">`wasbs:///`: Access default storage using encrypted communication.</span><span class="sxs-lookup"><span data-stu-id="250f9-177">`wasbs:///`: Access default storage using encrypted communication.</span></span>

* <span data-ttu-id="250f9-178">`wasbs://<container-name>@<account-name>.blob.core.windows.net/`: Used when communicating with a non-default storage account.</span><span class="sxs-lookup"><span data-stu-id="250f9-178">`wasbs://<container-name>@<account-name>.blob.core.windows.net/`: Used when communicating with a non-default storage account.</span></span> <span data-ttu-id="250f9-179">For example, when you have an additional storage account or when accessing data stored in a publicly accessible storage account.</span><span class="sxs-lookup"><span data-stu-id="250f9-179">For example, when you have an additional storage account or when accessing data stored in a publicly accessible storage account.</span></span>

<span data-ttu-id="250f9-180">When using __Data Lake Store__, use one of the following URI schemes:</span><span class="sxs-lookup"><span data-stu-id="250f9-180">When using __Data Lake Store__, use one of the following URI schemes:</span></span>

* <span data-ttu-id="250f9-181">`adl:///`: Access the default Data Lake Store for the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-181">`adl:///`: Access the default Data Lake Store for the cluster.</span></span>

* <span data-ttu-id="250f9-182">`adl://<storage-name>.azuredatalakestore.net/`: Used when communicating with a non-default Data Lake Store or accessing data outside the root directory of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-182">`adl://<storage-name>.azuredatalakestore.net/`: Used when communicating with a non-default Data Lake Store or accessing data outside the root directory of your HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="250f9-183">When using Data Lake Store as the default store for HDInsight, you must specify a path within the store to use as the root of HDInsight storage.</span><span class="sxs-lookup"><span data-stu-id="250f9-183">When using Data Lake Store as the default store for HDInsight, you must specify a path within the store to use as the root of HDInsight storage.</span></span> <span data-ttu-id="250f9-184">The default path is `/clusters/<cluster-name>/`.</span><span class="sxs-lookup"><span data-stu-id="250f9-184">The default path is `/clusters/<cluster-name>/`.</span></span>
>
> <span data-ttu-id="250f9-185">When using `/` or `adl:///` to access data, you can only access data stored in the root (for example, `/clusters/<cluster-name>/`) of the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-185">When using `/` or `adl:///` to access data, you can only access data stored in the root (for example, `/clusters/<cluster-name>/`) of the cluster.</span></span> <span data-ttu-id="250f9-186">To access data anywhere in the store, use the `adl://<storage-name>.azuredatalakestore.net/` format.</span><span class="sxs-lookup"><span data-stu-id="250f9-186">To access data anywhere in the store, use the `adl://<storage-name>.azuredatalakestore.net/` format.</span></span>

### <a name="what-storage-is-the-cluster-using"></a><span data-ttu-id="250f9-187">What storage is the cluster using</span><span class="sxs-lookup"><span data-stu-id="250f9-187">What storage is the cluster using</span></span>

<span data-ttu-id="250f9-188">You can use Ambari to retrieve the default storage configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-188">You can use Ambari to retrieve the default storage configuration for the cluster.</span></span> <span data-ttu-id="250f9-189">Use the following command to retrieve HDFS configuration information using curl, and filter it using [jq](https://stedolan.github.io/jq/):</span><span class="sxs-lookup"><span data-stu-id="250f9-189">Use the following command to retrieve HDFS configuration information using curl, and filter it using [jq](https://stedolan.github.io/jq/):</span></span>

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> <span data-ttu-id="250f9-190">This returns the first configuration applied to the server (`service_config_version=1`), which contains this information.</span><span class="sxs-lookup"><span data-stu-id="250f9-190">This returns the first configuration applied to the server (`service_config_version=1`), which contains this information.</span></span> <span data-ttu-id="250f9-191">If you are retrieving a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span><span class="sxs-lookup"><span data-stu-id="250f9-191">If you are retrieving a value that has been modified after cluster creation, you may need to list the configuration versions and retrieve the latest one.</span></span>

<span data-ttu-id="250f9-192">This command returns a value similar to the following:</span><span class="sxs-lookup"><span data-stu-id="250f9-192">This command returns a value similar to the following:</span></span>

* <span data-ttu-id="250f9-193">`wasbs://<container-name>@<account-name>.blob.core.windows.net` if using an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="250f9-193">`wasbs://<container-name>@<account-name>.blob.core.windows.net` if using an Azure Storage account.</span></span>

    <span data-ttu-id="250f9-194">The account name is the name of the Azure Storage account, while the container name is the blob container that is the root of the cluster storage.</span><span class="sxs-lookup"><span data-stu-id="250f9-194">The account name is the name of the Azure Storage account, while the container name is the blob container that is the root of the cluster storage.</span></span>

* <span data-ttu-id="250f9-195">`adl://home` if using Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="250f9-195">`adl://home` if using Azure Data Lake Store.</span></span> <span data-ttu-id="250f9-196">To get the Data Lake Store name, use the following REST call:</span><span class="sxs-lookup"><span data-stu-id="250f9-196">To get the Data Lake Store name, use the following REST call:</span></span>

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    <span data-ttu-id="250f9-197">This command returns the following host name: `<data-lake-store-account-name>.azuredatalakestore.net`.</span><span class="sxs-lookup"><span data-stu-id="250f9-197">This command returns the following host name: `<data-lake-store-account-name>.azuredatalakestore.net`.</span></span>

    <span data-ttu-id="250f9-198">To get the directory within the store that is the root for HDInsight, use the following REST call:</span><span class="sxs-lookup"><span data-stu-id="250f9-198">To get the directory within the store that is the root for HDInsight, use the following REST call:</span></span>

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    <span data-ttu-id="250f9-199">This command returns a path similar to the following: `/clusters/<hdinsight-cluster-name>/`.</span><span class="sxs-lookup"><span data-stu-id="250f9-199">This command returns a path similar to the following: `/clusters/<hdinsight-cluster-name>/`.</span></span>

<span data-ttu-id="250f9-200">You can also find the storage information using the Azure portal by using the following steps:</span><span class="sxs-lookup"><span data-stu-id="250f9-200">You can also find the storage information using the Azure portal by using the following steps:</span></span>

1. <span data-ttu-id="250f9-201">In the [Azure portal](https://portal.azure.com/), select your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-201">In the [Azure portal](https://portal.azure.com/), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="250f9-202">From the **Properties** section, select **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="250f9-202">From the **Properties** section, select **Storage Accounts**.</span></span> <span data-ttu-id="250f9-203">The storage information for the cluster is displayed.</span><span class="sxs-lookup"><span data-stu-id="250f9-203">The storage information for the cluster is displayed.</span></span>

### <a name="how-do-i-access-files-from-outside-hdinsight"></a><span data-ttu-id="250f9-204">How do I access files from outside HDInsight</span><span class="sxs-lookup"><span data-stu-id="250f9-204">How do I access files from outside HDInsight</span></span>

<span data-ttu-id="250f9-205">There are a various ways to access data from outside the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-205">There are a various ways to access data from outside the HDInsight cluster.</span></span> <span data-ttu-id="250f9-206">The following are a few links to utilities and SDKs that can be used to work with your data:</span><span class="sxs-lookup"><span data-stu-id="250f9-206">The following are a few links to utilities and SDKs that can be used to work with your data:</span></span>

<span data-ttu-id="250f9-207">If using __Azure Storage__, see the following links for ways that you can access your data:</span><span class="sxs-lookup"><span data-stu-id="250f9-207">If using __Azure Storage__, see the following links for ways that you can access your data:</span></span>

* <span data-ttu-id="250f9-208">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): Command-Line interface commands for working with Azure.</span><span class="sxs-lookup"><span data-stu-id="250f9-208">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): Command-Line interface commands for working with Azure.</span></span> <span data-ttu-id="250f9-209">After installing, use the `az storage` command for help on using storage, or `az storage blob` for blob-specific commands.</span><span class="sxs-lookup"><span data-stu-id="250f9-209">After installing, use the `az storage` command for help on using storage, or `az storage blob` for blob-specific commands.</span></span>
* <span data-ttu-id="250f9-210">[blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): A python script for working with blobs in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="250f9-210">[blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): A python script for working with blobs in Azure Storage.</span></span>
* <span data-ttu-id="250f9-211">Various SDKs:</span><span class="sxs-lookup"><span data-stu-id="250f9-211">Various SDKs:</span></span>

    * [<span data-ttu-id="250f9-212">Java</span><span class="sxs-lookup"><span data-stu-id="250f9-212">Java</span></span>](https://github.com/Azure/azure-sdk-for-java)
    * [<span data-ttu-id="250f9-213">Node.js</span><span class="sxs-lookup"><span data-stu-id="250f9-213">Node.js</span></span>](https://github.com/Azure/azure-sdk-for-node)
    * [<span data-ttu-id="250f9-214">PHP</span><span class="sxs-lookup"><span data-stu-id="250f9-214">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php)
    * [<span data-ttu-id="250f9-215">Python</span><span class="sxs-lookup"><span data-stu-id="250f9-215">Python</span></span>](https://github.com/Azure/azure-sdk-for-python)
    * [<span data-ttu-id="250f9-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="250f9-216">Ruby</span></span>](https://github.com/Azure/azure-sdk-for-ruby)
    * [<span data-ttu-id="250f9-217">.NET</span><span class="sxs-lookup"><span data-stu-id="250f9-217">.NET</span></span>](https://github.com/Azure/azure-sdk-for-net)
    * [<span data-ttu-id="250f9-218">Storage REST API</span><span class="sxs-lookup"><span data-stu-id="250f9-218">Storage REST API</span></span>](https://msdn.microsoft.com/library/azure/dd135733.aspx)

<span data-ttu-id="250f9-219">If using __Azure Data Lake Store__, see the following links for ways that you can access your data:</span><span class="sxs-lookup"><span data-stu-id="250f9-219">If using __Azure Data Lake Store__, see the following links for ways that you can access your data:</span></span>

* [<span data-ttu-id="250f9-220">Web browser</span><span class="sxs-lookup"><span data-stu-id="250f9-220">Web browser</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* [<span data-ttu-id="250f9-221">PowerShell</span><span class="sxs-lookup"><span data-stu-id="250f9-221">PowerShell</span></span>](../data-lake-store/data-lake-store-get-started-powershell.md)
* [<span data-ttu-id="250f9-222">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="250f9-222">Azure CLI</span></span>](../data-lake-store/data-lake-store-get-started-cli.md)
* [<span data-ttu-id="250f9-223">WebHDFS REST API</span><span class="sxs-lookup"><span data-stu-id="250f9-223">WebHDFS REST API</span></span>](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [<span data-ttu-id="250f9-224">Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="250f9-224">Data Lake Tools for Visual Studio</span></span>](https://www.microsoft.com/download/details.aspx?id=49504)
* [<span data-ttu-id="250f9-225">.NET</span><span class="sxs-lookup"><span data-stu-id="250f9-225">.NET</span></span>](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="250f9-226">Java</span><span class="sxs-lookup"><span data-stu-id="250f9-226">Java</span></span>](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="250f9-227">Python</span><span class="sxs-lookup"><span data-stu-id="250f9-227">Python</span></span>](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a><span data-ttu-id="250f9-228">Scaling your cluster</span><span class="sxs-lookup"><span data-stu-id="250f9-228">Scaling your cluster</span></span>

<span data-ttu-id="250f9-229">The cluster scaling feature allows you to change the number of data nodes used by a cluster without having to delete and re-create the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-229">The cluster scaling feature allows you to change the number of data nodes used by a cluster without having to delete and re-create the cluster.</span></span> <span data-ttu-id="250f9-230">You can perform scaling operations while other jobs or processes are running on a cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-230">You can perform scaling operations while other jobs or processes are running on a cluster.</span></span>

<span data-ttu-id="250f9-231">The different cluster types are affected by scaling as follows:</span><span class="sxs-lookup"><span data-stu-id="250f9-231">The different cluster types are affected by scaling as follows:</span></span>

* <span data-ttu-id="250f9-232">**Hadoop**: When scaling down the number of nodes in a cluster, some of the services in the cluster are restarted.</span><span class="sxs-lookup"><span data-stu-id="250f9-232">**Hadoop**: When scaling down the number of nodes in a cluster, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="250f9-233">This can cause jobs running or pending to fail at the completion of the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="250f9-233">This can cause jobs running or pending to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="250f9-234">You can resubmit the jobs once the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="250f9-234">You can resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="250f9-235">**HBase**: Regional servers are automatically balanced within a few minutes after completion of the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="250f9-235">**HBase**: Regional servers are automatically balanced within a few minutes after completion of the scaling operation.</span></span> <span data-ttu-id="250f9-236">To manually balance regional servers, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="250f9-236">To manually balance regional servers, use the following steps:</span></span>

    1. <span data-ttu-id="250f9-237">Connect to the HDInsight cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="250f9-237">Connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="250f9-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="250f9-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

    2. <span data-ttu-id="250f9-239">Use the following to start the HBase shell:</span><span class="sxs-lookup"><span data-stu-id="250f9-239">Use the following to start the HBase shell:</span></span>

            hbase shell

    3. <span data-ttu-id="250f9-240">Once the HBase shell has loaded, use the following to manually balance the regional servers:</span><span class="sxs-lookup"><span data-stu-id="250f9-240">Once the HBase shell has loaded, use the following to manually balance the regional servers:</span></span>

            balancer

* <span data-ttu-id="250f9-241">**Storm**: You should rebalance any running Storm topologies after a scaling operation has been performed.</span><span class="sxs-lookup"><span data-stu-id="250f9-241">**Storm**: You should rebalance any running Storm topologies after a scaling operation has been performed.</span></span> <span data-ttu-id="250f9-242">This allows the topology to readjust parallelism settings based on the new number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-242">This allows the topology to readjust parallelism settings based on the new number of nodes in the cluster.</span></span> <span data-ttu-id="250f9-243">To rebalance running topologies, use one of the following options:</span><span class="sxs-lookup"><span data-stu-id="250f9-243">To rebalance running topologies, use one of the following options:</span></span>

    * <span data-ttu-id="250f9-244">**SSH**: Connect to the server and use the following command to rebalance a topology:</span><span class="sxs-lookup"><span data-stu-id="250f9-244">**SSH**: Connect to the server and use the following command to rebalance a topology:</span></span>

            storm rebalance TOPOLOGYNAME

        <span data-ttu-id="250f9-245">You can also specify parameters to override the parallelism hints originally provided by the topology.</span><span class="sxs-lookup"><span data-stu-id="250f9-245">You can also specify parameters to override the parallelism hints originally provided by the topology.</span></span> <span data-ttu-id="250f9-246">For example, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` reconfigures the topology to 5 worker processes, 3 executors for the blue-spout component, and 10 executors for the yellow-bolt component.</span><span class="sxs-lookup"><span data-stu-id="250f9-246">For example, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` reconfigures the topology to 5 worker processes, 3 executors for the blue-spout component, and 10 executors for the yellow-bolt component.</span></span>

    * <span data-ttu-id="250f9-247">**Storm UI**: Use the following steps to rebalance a topology using the Storm UI.</span><span class="sxs-lookup"><span data-stu-id="250f9-247">**Storm UI**: Use the following steps to rebalance a topology using the Storm UI.</span></span>

        1. <span data-ttu-id="250f9-248">Open **https://CLUSTERNAME.azurehdinsight.net/stormui** in your web browser, where CLUSTERNAME is the name of your Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-248">Open **https://CLUSTERNAME.azurehdinsight.net/stormui** in your web browser, where CLUSTERNAME is the name of your Storm cluster.</span></span> <span data-ttu-id="250f9-249">If prompted, enter the HDInsight cluster administrator (admin) name and password you specified when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-249">If prompted, enter the HDInsight cluster administrator (admin) name and password you specified when creating the cluster.</span></span>
        2. <span data-ttu-id="250f9-250">Select the topology you wish to rebalance, then select the **Rebalance** button.</span><span class="sxs-lookup"><span data-stu-id="250f9-250">Select the topology you wish to rebalance, then select the **Rebalance** button.</span></span> <span data-ttu-id="250f9-251">Enter the delay before the rebalance operation is performed.</span><span class="sxs-lookup"><span data-stu-id="250f9-251">Enter the delay before the rebalance operation is performed.</span></span>

<span data-ttu-id="250f9-252">For specific information on scaling your HDInsight cluster, see:</span><span class="sxs-lookup"><span data-stu-id="250f9-252">For specific information on scaling your HDInsight cluster, see:</span></span>

* [<span data-ttu-id="250f9-253">Manage Hadoop clusters in HDInsight by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="250f9-253">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [<span data-ttu-id="250f9-254">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="250f9-254">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a><span data-ttu-id="250f9-255">How do I install Hue (or other Hadoop component)?</span><span class="sxs-lookup"><span data-stu-id="250f9-255">How do I install Hue (or other Hadoop component)?</span></span>

<span data-ttu-id="250f9-256">HDInsight is a managed service.</span><span class="sxs-lookup"><span data-stu-id="250f9-256">HDInsight is a managed service.</span></span> <span data-ttu-id="250f9-257">If Azure detects a problem with the cluster, it may delete the failing node and create a node to replace it.</span><span class="sxs-lookup"><span data-stu-id="250f9-257">If Azure detects a problem with the cluster, it may delete the failing node and create a node to replace it.</span></span> <span data-ttu-id="250f9-258">If you manually install things on the cluster, they are not persisted when this operation occurs..</span><span class="sxs-lookup"><span data-stu-id="250f9-258">If you manually install things on the cluster, they are not persisted when this operation occurs..</span></span> <span data-ttu-id="250f9-259">Instead, use [HDInsight Script Actions](hdinsight-hadoop-customize-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="250f9-259">Instead, use [HDInsight Script Actions](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="250f9-260">A script action can be used to make the following changes:</span><span class="sxs-lookup"><span data-stu-id="250f9-260">A script action can be used to make the following changes:</span></span>

* <span data-ttu-id="250f9-261">Install and configure a service or web site such as Spark or Hue.</span><span class="sxs-lookup"><span data-stu-id="250f9-261">Install and configure a service or web site such as Spark or Hue.</span></span>
* <span data-ttu-id="250f9-262">Install and configure a component that requires configuration changes on multiple nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-262">Install and configure a component that requires configuration changes on multiple nodes in the cluster.</span></span> <span data-ttu-id="250f9-263">For example, a required environment variable, creating of a logging directory, or creation of a configuration file.</span><span class="sxs-lookup"><span data-stu-id="250f9-263">For example, a required environment variable, creating of a logging directory, or creation of a configuration file.</span></span>

<span data-ttu-id="250f9-264">Script Actions are Bash scripts that run during cluster provisioning, and can be used to install and configure additional components on the cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-264">Script Actions are Bash scripts that run during cluster provisioning, and can be used to install and configure additional components on the cluster.</span></span> <span data-ttu-id="250f9-265">Example scripts are provided for installing the following components:</span><span class="sxs-lookup"><span data-stu-id="250f9-265">Example scripts are provided for installing the following components:</span></span>

* [<span data-ttu-id="250f9-266">Hue</span><span class="sxs-lookup"><span data-stu-id="250f9-266">Hue</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="250f9-267">Giraph</span><span class="sxs-lookup"><span data-stu-id="250f9-267">Giraph</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="250f9-268">Solr</span><span class="sxs-lookup"><span data-stu-id="250f9-268">Solr</span></span>](hdinsight-hadoop-solr-install-linux.md)

<span data-ttu-id="250f9-269">For information on developing your own Script Actions, see [Script Action development with HDInsight](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="250f9-269">For information on developing your own Script Actions, see [Script Action development with HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>

### <a name="jar-files"></a><span data-ttu-id="250f9-270">Jar files</span><span class="sxs-lookup"><span data-stu-id="250f9-270">Jar files</span></span>

<span data-ttu-id="250f9-271">Some Hadoop technologies are provided in self-contained jar files that contain functions used as part of a MapReduce job, or from inside Pig or Hive.</span><span class="sxs-lookup"><span data-stu-id="250f9-271">Some Hadoop technologies are provided in self-contained jar files that contain functions used as part of a MapReduce job, or from inside Pig or Hive.</span></span> <span data-ttu-id="250f9-272">While these can be installed using Script Actions, they often don't require any setup and can be uploaded to the cluster after provisioning and used directly.</span><span class="sxs-lookup"><span data-stu-id="250f9-272">While these can be installed using Script Actions, they often don't require any setup and can be uploaded to the cluster after provisioning and used directly.</span></span> <span data-ttu-id="250f9-273">If you want to make sure the component survives reimaging of the cluster, you can store the jar file in the default storage for your cluster (WASB or ADL).</span><span class="sxs-lookup"><span data-stu-id="250f9-273">If you want to make sure the component survives reimaging of the cluster, you can store the jar file in the default storage for your cluster (WASB or ADL).</span></span>

<span data-ttu-id="250f9-274">For example, if you want to use the latest version of [DataFu](http://datafu.incubator.apache.org/), you can download a jar containing the project and upload it to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="250f9-274">For example, if you want to use the latest version of [DataFu](http://datafu.incubator.apache.org/), you can download a jar containing the project and upload it to the HDInsight cluster.</span></span> <span data-ttu-id="250f9-275">Then follow the DataFu documentation on how to use it from Pig or Hive.</span><span class="sxs-lookup"><span data-stu-id="250f9-275">Then follow the DataFu documentation on how to use it from Pig or Hive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="250f9-276">Some components that are standalone jar files are provided with HDInsight, but are not in the path.</span><span class="sxs-lookup"><span data-stu-id="250f9-276">Some components that are standalone jar files are provided with HDInsight, but are not in the path.</span></span> <span data-ttu-id="250f9-277">If you are looking for a specific component, you can use the follow to search for it on your cluster:</span><span class="sxs-lookup"><span data-stu-id="250f9-277">If you are looking for a specific component, you can use the follow to search for it on your cluster:</span></span>
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> <span data-ttu-id="250f9-278">This command returns the path of any matching jar files.</span><span class="sxs-lookup"><span data-stu-id="250f9-278">This command returns the path of any matching jar files.</span></span>

<span data-ttu-id="250f9-279">If you want to use a different version than the one that comes with the cluster, you can upload a new version of the component to the and try using it in your jobs.</span><span class="sxs-lookup"><span data-stu-id="250f9-279">If you want to use a different version than the one that comes with the cluster, you can upload a new version of the component to the and try using it in your jobs.</span></span>

> [!WARNING]
> <span data-ttu-id="250f9-280">Components provided with the HDInsight cluster are fully supported and Microsoft Support helps to isolate and resolve issues related to these components.</span><span class="sxs-lookup"><span data-stu-id="250f9-280">Components provided with the HDInsight cluster are fully supported and Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="250f9-281">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="250f9-281">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="250f9-282">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span><span class="sxs-lookup"><span data-stu-id="250f9-282">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="250f9-283">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="250f9-283">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="250f9-284">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="250f9-284">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="250f9-285">Next steps</span><span class="sxs-lookup"><span data-stu-id="250f9-285">Next steps</span></span>

* [<span data-ttu-id="250f9-286">Migrate from Windows-based HDInsight to Linux-based</span><span class="sxs-lookup"><span data-stu-id="250f9-286">Migrate from Windows-based HDInsight to Linux-based</span></span>](hdinsight-migrate-from-windows-to-linux.md)
* [<span data-ttu-id="250f9-287">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="250f9-287">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="250f9-288">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="250f9-288">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="250f9-289">Use MapReduce jobs with HDInsight</span><span class="sxs-lookup"><span data-stu-id="250f9-289">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
