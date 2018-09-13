---
title: Customize HDInsight clusters using script actions | Microsoft Docs
description: Learn how to add custom components to Linux-based HDInsight clusters using Script Actions. Script Actions are Bash scripts that on the cluster nodes, and can be used to customize the cluster configuration or add additional services and utilities like Hue, Solr, or R.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: larryfr
ms.openlocfilehash: 9eb7acae8b68074a79752dd540dfe33b4ea71032
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552920"
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="dcbf8-104">Customize Linux-based HDInsight clusters using Script Action</span><span class="sxs-lookup"><span data-stu-id="dcbf8-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="dcbf8-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize the cluster.</span></span> <span data-ttu-id="dcbf8-106">These scripts can be used during cluster creation, or on an already running cluster, and are used to install additional components or change configuration settings.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-106">These scripts can be used during cluster creation, or on an already running cluster, and are used to install additional components or change configuration settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcbf8-107">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-107">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="dcbf8-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dcbf8-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>


<span data-ttu-id="dcbf8-110">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-110">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="dcbf8-111">Some of the examples in this document show how you can install an HDInsight application using script action commands from PowerShell and the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-111">Some of the examples in this document show how you can install an HDInsight application using script action commands from PowerShell and the .NET SDK.</span></span> <span data-ttu-id="dcbf8-112">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-112">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="dcbf8-113">Permissions</span><span class="sxs-lookup"><span data-stu-id="dcbf8-113">Permissions</span></span>

<span data-ttu-id="dcbf8-114">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-114">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span></span>

* <span data-ttu-id="dcbf8-115">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-115">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="dcbf8-116">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-116">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="dcbf8-117">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-117">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="dcbf8-118">Access control</span><span class="sxs-lookup"><span data-stu-id="dcbf8-118">Access control</span></span>

<span data-ttu-id="dcbf8-119">If you use an Azure subscription where you are not the administrator/owner, such as a company owned subscription, you must verify that your Azure account has at least **Contributor** access to the Azure resource group that contains the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-119">If you use an Azure subscription where you are not the administrator/owner, such as a company owned subscription, you must verify that your Azure account has at least **Contributor** access to the Azure resource group that contains the HDInsight cluster.</span></span>

<span data-ttu-id="dcbf8-120">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-120">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span></span> <span data-ttu-id="dcbf8-121">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-121">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span></span> <span data-ttu-id="dcbf8-122">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-122">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="dcbf8-123">For more information on working with access management, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-123">For more information on working with access management, see the following documents:</span></span>

* [<span data-ttu-id="dcbf8-124">Get started with access management in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dcbf8-124">Get started with access management in the Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="dcbf8-125">Use role assignments to manage access to your Azure subscription resources</span><span class="sxs-lookup"><span data-stu-id="dcbf8-125">Use role assignments to manage access to your Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="dcbf8-126">Understanding Script Actions</span><span class="sxs-lookup"><span data-stu-id="dcbf8-126">Understanding Script Actions</span></span>

<span data-ttu-id="dcbf8-127">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-127">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="dcbf8-128">The script runs on nodes in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-128">The script runs on nodes in the HDInsight cluster.</span></span> <span data-ttu-id="dcbf8-129">The following are characteristics and features of script actions.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-129">The following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="dcbf8-130">Must be stored on a URI that is accessible from the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-130">Must be stored on a URI that is accessible from the HDInsight cluster.</span></span> <span data-ttu-id="dcbf8-131">The following are possible storage locations:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-131">The following are possible storage locations:</span></span>

    * <span data-ttu-id="dcbf8-132">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-132">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span></span> <span data-ttu-id="dcbf8-133">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-133">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="dcbf8-134">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-134">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="dcbf8-135">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-135">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

    * <span data-ttu-id="dcbf8-136">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-136">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span></span> <span data-ttu-id="dcbf8-137">Since HDInsight is granted access to both of these types of storage accounts during cluster creation, these provide a way to use a non-public script action.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-137">Since HDInsight is granted access to both of these types of storage accounts during cluster creation, these provide a way to use a non-public script action.</span></span>

    * <span data-ttu-id="dcbf8-138">An public file sharing service such as an Azure Blob, GitHub, OneDrive, Dropbox, etc.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-138">An public file sharing service such as an Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="dcbf8-139">For examples of the URI for scripts stored in blob container (publicly readable,) see the [Example script action scripts](#example-script-action-scripts) section.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-139">For examples of the URI for scripts stored in blob container (publicly readable,) see the [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="dcbf8-140">HDInsight only supports __General purpose__ Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-140">HDInsight only supports __General purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="dcbf8-141">It does not currently support the __Blob storage__ account type.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-141">It does not currently support the __Blob storage__ account type.</span></span>

* <span data-ttu-id="dcbf8-142">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-142">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="dcbf8-143">When used with HDInsight Premium, you can specify that the script should be used on the edge node.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-143">When used with HDInsight Premium, you can specify that the script should be used on the edge node.</span></span>

* <span data-ttu-id="dcbf8-144">Can be **persisted** or **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-144">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="dcbf8-145">**Persisted** scripts are scripts that are applied to worker nodes and run automatically on new nodes created when scaling up a cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-145">**Persisted** scripts are scripts that are applied to worker nodes and run automatically on new nodes created when scaling up a cluster.</span></span>

    <span data-ttu-id="dcbf8-146">A persisted script might also apply changes to another node type, such as a head node, but from a functionality perspective the only reason to persist a script is so it applies to new worker nodes created when a cluster is scaled out.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-146">A persisted script might also apply changes to another node type, such as a head node, but from a functionality perspective the only reason to persist a script is so it applies to new worker nodes created when a cluster is scaled out.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="dcbf8-147">Persisted script actions must have a unique name.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-147">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="dcbf8-148">**Ad hoc** scripts are not persisted; however, you can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-148">**Ad hoc** scripts are not persisted; however, you can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="dcbf8-149">Script actions used during cluster creation are automatically persisted.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-149">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="dcbf8-150">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-150">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="dcbf8-151">Can accept **parameters** that are used by the script during execution.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-151">Can accept **parameters** that are used by the script during execution.</span></span>
* <span data-ttu-id="dcbf8-152">Run with **root level privileges** on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-152">Run with **root level privileges** on the cluster nodes.</span></span>
* <span data-ttu-id="dcbf8-153">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="dcbf8-153">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="dcbf8-154">To assist in understanding what scripts have been applied to a cluster, and in determining the ID of scripts for promotion or demotion, the cluster keeps a history of all scripts that have been ran.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-154">To assist in understanding what scripts have been applied to a cluster, and in determining the ID of scripts for promotion or demotion, the cluster keeps a history of all scripts that have been ran.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcbf8-155">There is no automatic way to undo the changes made by a script action.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-155">There is no automatic way to undo the changes made by a script action.</span></span> <span data-ttu-id="dcbf8-156">If you need to reverse the effects of a script, you must understand what changes were made and manually reverse them (or provide a script action that reverses them.)</span><span class="sxs-lookup"><span data-stu-id="dcbf8-156">If you need to reverse the effects of a script, you must understand what changes were made and manually reverse them (or provide a script action that reverses them.)</span></span>


### <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="dcbf8-157">Script Action in the cluster creation process</span><span class="sxs-lookup"><span data-stu-id="dcbf8-157">Script Action in the cluster creation process</span></span>

<span data-ttu-id="dcbf8-158">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-158">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="dcbf8-159">The script is **automatically persisted**.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-159">The script is **automatically persisted**.</span></span>
* <span data-ttu-id="dcbf8-160">A **failure** in the script can cause the cluster creation process to fail.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-160">A **failure** in the script can cause the cluster creation process to fail.</span></span>

<span data-ttu-id="dcbf8-161">The following diagram illustrates when Script Action is executed during the creation process:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-161">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="dcbf8-162">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="dcbf8-162">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="dcbf8-163">The script runs while HDInsight is being configured.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-163">The script runs while HDInsight is being configured.</span></span> <span data-ttu-id="dcbf8-164">At this stage, the script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-164">At this stage, the script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="dcbf8-165">Because the script runs with root level privilege on the cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-165">Because the script runs with root level privilege on the cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="dcbf8-166">If you stop services, you must ensure that the Ambari service and other Hadoop-related services are up and running before the script finishes running.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-166">If you stop services, you must ensure that the Ambari service and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="dcbf8-167">These services are required to successfully determine the health and state of the cluster while it is being created.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-167">These services are required to successfully determine the health and state of the cluster while it is being created.</span></span>


<span data-ttu-id="dcbf8-168">During cluster creation, you can specify multiple script actions that are invoked in the order in which they were specified.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-168">During cluster creation, you can specify multiple script actions that are invoked in the order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcbf8-169">Script actions must complete within 60 minutes, or timeout.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-169">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="dcbf8-170">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-170">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="dcbf8-171">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-171">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>
>
> <span data-ttu-id="dcbf8-172">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-172">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="dcbf8-173">Instead, pre-compile the application and store the binary in Azure Storage so that it can quickly be downloaded to the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-173">Instead, pre-compile the application and store the binary in Azure Storage so that it can quickly be downloaded to the cluster.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="dcbf8-174">Script action on a running cluster</span><span class="sxs-lookup"><span data-stu-id="dcbf8-174">Script action on a running cluster</span></span>

<span data-ttu-id="dcbf8-175">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-175">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span></span> <span data-ttu-id="dcbf8-176">Once a script completes, the cluster should return to a "running" state.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-176">Once a script completes, the cluster should return to a "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcbf8-177">This does not mean that your running cluster is immune to scripts that do bad things.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-177">This does not mean that your running cluster is immune to scripts that do bad things.</span></span> <span data-ttu-id="dcbf8-178">For example, a script could delete files needed by the cluster, change configuration so that services fail, etc.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-178">For example, a script could delete files needed by the cluster, change configuration so that services fail, etc.</span></span>
>
> <span data-ttu-id="dcbf8-179">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it to your cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-179">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it to your cluster.</span></span>

<span data-ttu-id="dcbf8-180">When applying a script to a cluster, the cluster state changes to from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-180">When applying a script to a cluster, the cluster state changes to from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span></span> <span data-ttu-id="dcbf8-181">The script status is logged in the script action history, and you can use this to determine if the script succeeded or failed.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-181">The script status is logged in the script action history, and you can use this to determine if the script succeeded or failed.</span></span> <span data-ttu-id="dcbf8-182">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-182">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span></span> <span data-ttu-id="dcbf8-183">It returns information similar to the following:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-183">It returns information similar to the following:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 2/23/2016 7:40:55 PM
    EndTime           : 2/23/2016 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="dcbf8-184">If you have changed the cluster user (admin) password after the cluster was created, this may cause script actions ran against this cluster to fail.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-184">If you have changed the cluster user (admin) password after the cluster was created, this may cause script actions ran against this cluster to fail.</span></span> <span data-ttu-id="dcbf8-185">If you have any persisted script actions that target worker nodes, these may fail when you add nodes to the cluster through resize operations.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-185">If you have any persisted script actions that target worker nodes, these may fail when you add nodes to the cluster through resize operations.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="dcbf8-186">Example Script Action scripts</span><span class="sxs-lookup"><span data-stu-id="dcbf8-186">Example Script Action scripts</span></span>

<span data-ttu-id="dcbf8-187">Script Action scripts can be used from the Azure portal, Azure PowerShell, Azure CLI, or the HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-187">Script Action scripts can be used from the Azure portal, Azure PowerShell, Azure CLI, or the HDInsight .NET SDK.</span></span> <span data-ttu-id="dcbf8-188">HDInsight provides scripts to install the following components on HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-188">HDInsight provides scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="dcbf8-189">Name</span><span class="sxs-lookup"><span data-stu-id="dcbf8-189">Name</span></span> | <span data-ttu-id="dcbf8-190">Script</span><span class="sxs-lookup"><span data-stu-id="dcbf8-190">Script</span></span> |
| --- | --- |
| <span data-ttu-id="dcbf8-191">**Add an Azure Storage account**</span><span class="sxs-lookup"><span data-stu-id="dcbf8-191">**Add an Azure Storage account**</span></span> |<span data-ttu-id="dcbf8-192">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-192">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="dcbf8-193">**Install Hue**</span><span class="sxs-lookup"><span data-stu-id="dcbf8-193">**Install Hue**</span></span> |<span data-ttu-id="dcbf8-194">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-194">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="dcbf8-195">**Install R**</span><span class="sxs-lookup"><span data-stu-id="dcbf8-195">**Install R**</span></span> |<span data-ttu-id="dcbf8-196">https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh. See [Install and use R on HDInsight clusters](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-196">https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh. See [Install and use R on HDInsight clusters](hdinsight-hadoop-r-scripts-linux.md).</span></span> |
| <span data-ttu-id="dcbf8-197">**Install Solr**</span><span class="sxs-lookup"><span data-stu-id="dcbf8-197">**Install Solr**</span></span> |<span data-ttu-id="dcbf8-198">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-198">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="dcbf8-199">**Install Giraph**</span><span class="sxs-lookup"><span data-stu-id="dcbf8-199">**Install Giraph**</span></span> |<span data-ttu-id="dcbf8-200">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-200">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="dcbf8-201">**Pre-load Hive libraries**</span><span class="sxs-lookup"><span data-stu-id="dcbf8-201">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="dcbf8-202">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="dcbf8-202">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="dcbf8-203">Use a Script Action during cluster creation</span><span class="sxs-lookup"><span data-stu-id="dcbf8-203">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="dcbf8-204">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster- from the Azure portal, using an Azure Resource Manager template, using PowerShell CMDlets, and using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-204">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster- from the Azure portal, using an Azure Resource Manager template, using PowerShell CMDlets, and using the .NET SDK.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a><span data-ttu-id="dcbf8-205">Use a Script Action during cluster creation from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dcbf8-205">Use a Script Action during cluster creation from the Azure portal</span></span>

1. <span data-ttu-id="dcbf8-206">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-206">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="dcbf8-207">Under **Optional Configuration**, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-207">Under **Optional Configuration**, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span></span>

    ![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/HDI.CreateCluster.8.png)

    | <span data-ttu-id="dcbf8-209">Property</span><span class="sxs-lookup"><span data-stu-id="dcbf8-209">Property</span></span> | <span data-ttu-id="dcbf8-210">Value</span><span class="sxs-lookup"><span data-stu-id="dcbf8-210">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="dcbf8-211">Name</span><span class="sxs-lookup"><span data-stu-id="dcbf8-211">Name</span></span> |<span data-ttu-id="dcbf8-212">Specify a name for the script action.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-212">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="dcbf8-213">Script URI</span><span class="sxs-lookup"><span data-stu-id="dcbf8-213">Script URI</span></span> |<span data-ttu-id="dcbf8-214">Specify the URI to the script that is invoked to customize the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-214">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="dcbf8-215">Head/Worker</span><span class="sxs-lookup"><span data-stu-id="dcbf8-215">Head/Worker</span></span> |<span data-ttu-id="dcbf8-216">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-216">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="dcbf8-217">Parameters</span><span class="sxs-lookup"><span data-stu-id="dcbf8-217">Parameters</span></span> |<span data-ttu-id="dcbf8-218">Specify the parameters, if required by the script.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-218">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="dcbf8-219">Press ENTER to add more than one script action to install multiple components on the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-219">Press ENTER to add more than one script action to install multiple components on the cluster.</span></span>

3. <span data-ttu-id="dcbf8-220">Click **Select** to save the configuration and continue with cluster creation.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-220">Click **Select** to save the configuration and continue with cluster creation.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="dcbf8-221">Use a Script Action from Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="dcbf8-221">Use a Script Action from Azure Resource Manager templates</span></span>
<span data-ttu-id="dcbf8-222">In this section, we use Azure Resource Manager templates to create an HDInsight cluster and also use a script action to install custom components (R, in this example) on the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-222">In this section, we use Azure Resource Manager templates to create an HDInsight cluster and also use a script action to install custom components (R, in this example) on the cluster.</span></span> <span data-ttu-id="dcbf8-223">This section provides a sample template to create a cluster using script action.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-223">This section provides a sample template to create a cluster using script action.</span></span>

> [!NOTE]
> <span data-ttu-id="dcbf8-224">The steps in this section demonstrate creating a cluster using a script action.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-224">The steps in this section demonstrate creating a cluster using a script action.</span></span> <span data-ttu-id="dcbf8-225">For an example of creating a cluster from a template using an HDInsight application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-225">For an example of creating a cluster from a template using an HDInsight application, see [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="dcbf8-226">Before you begin</span><span class="sxs-lookup"><span data-stu-id="dcbf8-226">Before you begin</span></span>

* <span data-ttu-id="dcbf8-227">For information about configuring a workstation to run HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-227">For information about configuring a workstation to run HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="dcbf8-228">For instructions on how to create templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-228">For instructions on how to create templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="dcbf8-229">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-229">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="dcbf8-230">Create clusters using Script Action</span><span class="sxs-lookup"><span data-stu-id="dcbf8-230">Create clusters using Script Action</span></span>

1. <span data-ttu-id="dcbf8-231">Copy the following template to a location on your computer.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-231">Copy the following template to a location on your computer.</span></span> <span data-ttu-id="dcbf8-232">This template installs Giraph on the headnodes as well as worker nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-232">This template installs Giraph on the headnodes as well as worker nodes in the cluster.</span></span> <span data-ttu-id="dcbf8-233">You can also verify if the JSON template is valid.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-233">You can also verify if the JSON template is valid.</span></span> <span data-ttu-id="dcbf8-234">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-234">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="dcbf8-235">Start Azure PowerShell and Log in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-235">Start Azure PowerShell and Log in to your Azure account.</span></span> <span data-ttu-id="dcbf8-236">After providing your credentials, the command returns information about your account.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-236">After providing your credentials, the command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="dcbf8-237">If you have multiple subscriptions, provide the subscription id you wish to use for deployment.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-237">If you have multiple subscriptions, provide the subscription id you wish to use for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="dcbf8-238">You can use `Get-AzureRmSubscription` to get a list of all subscriptions associated with your account, which includes the subscription Id for each one.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-238">You can use `Get-AzureRmSubscription` to get a list of all subscriptions associated with your account, which includes the subscription Id for each one.</span></span>

4. <span data-ttu-id="dcbf8-239">If you do not have an existing resource group, create a new resource group.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-239">If you do not have an existing resource group, create a new resource group.</span></span> <span data-ttu-id="dcbf8-240">Provide the name of the resource group and location that you need for your solution.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-240">Provide the name of the resource group and location that you need for your solution.</span></span> <span data-ttu-id="dcbf8-241">A summary of the new resource group is returned.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-241">A summary of the new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="dcbf8-242">To create a new deployment for your resource group, run the **New-AzureRmResourceGroupDeployment** command and provide the necessary parameters.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-242">To create a new deployment for your resource group, run the **New-AzureRmResourceGroupDeployment** command and provide the necessary parameters.</span></span> <span data-ttu-id="dcbf8-243">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template you created.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-243">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template you created.</span></span> <span data-ttu-id="dcbf8-244">If your template requires any parameters, you must pass those parameters as well.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-244">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="dcbf8-245">In this case, the script action to install R on the cluster does not require any parameters.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-245">In this case, the script action to install R on the cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="dcbf8-246">You are prompted to provide values for the parameters defined in the template.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-246">You are prompted to provide values for the parameters defined in the template.</span></span>

1. <span data-ttu-id="dcbf8-247">When the resource group has been deployed, a summary of the deployment is displayed.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-247">When the resource group has been deployed, a summary of the deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/17/2015 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="dcbf8-248">If your deployment fails, you can use the following cmdlets to get information about the failures.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-248">If your deployment fails, you can use the following cmdlets to get information about the failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="dcbf8-249">Use a Script Action during cluster creation from Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcbf8-249">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="dcbf8-250">In this section, we use the [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet to invoke scripts by using Script Action to customize a cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-250">In this section, we use the [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet to invoke scripts by using Script Action to customize a cluster.</span></span> <span data-ttu-id="dcbf8-251">Before proceeding, make sure you have installed and configured Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-251">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="dcbf8-252">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-252">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="dcbf8-253">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-253">Perform the following steps:</span></span>

1. <span data-ttu-id="dcbf8-254">Open the Azure PowerShell console and use the following to log in to your Azure subscription and declare some PowerShell variables:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-254">Open the Azure PowerShell console and use the following to log in to your Azure subscription and declare some PowerShell variables:</span></span>

        # LOGIN TO ZURE
        Login-AzureRmAccount

        # PROVIDE VALUES FOR THESE VARIABLES
        $subscriptionId = "<SubscriptionId>"        # ID of the Azure subscription
        $clusterName = "<HDInsightClusterName>"            # HDInsight cluster name
        $storageAccountName = "<StorageAccountName>"    # Azure storage account that hosts the default container
        $storageAccountKey = "<StorageAccountKey>"      # Key for the storage account
        $containerName = $clusterName
        $location = "<MicrosoftDataCenter>"                # Location of the HDInsight cluster. It must be in the same data center as the storage account.
        $clusterNodes = <ClusterSizeInNumbers>            # The number of nodes in the HDInsight cluster.
        $resourceGroupName = "<ResourceGroupName>"      # The resource group that the HDInsight cluster is created in

2. <span data-ttu-id="dcbf8-255">Specify the configuration values (such as nodes in the cluster) and the default storage to be used.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-255">Specify the configuration values (such as nodes in the cluster) and the default storage to be used.</span></span>

        # SPECIFY THE CONFIGURATION OPTIONS
        Select-AzureRmSubscription -SubscriptionId $subscriptionId
        $config = New-AzureRmHDInsightClusterConfig
        $config.DefaultStorageAccountName="$storageAccountName.blob.core.windows.net"
        $config.DefaultStorageAccountKey=$storageAccountKey

3. <span data-ttu-id="dcbf8-256">Use **Add-AzureRmHDInsightScriptAction** cmdlet to invoke the script.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-256">Use **Add-AzureRmHDInsightScriptAction** cmdlet to invoke the script.</span></span> <span data-ttu-id="dcbf8-257">The following example uses a script that installs Giraph on the cluster:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-257">The following example uses a script that installs Giraph on the cluster:</span></span>

        # INVOKE THE SCRIPT USING THE SCRIPT ACTION FOR HEADNODE AND WORKERNODE
        $config = Add-AzureRmHDInsightScriptAction -Config $config -Name "Install Giraph"  -NodeType HeadNode -Uri https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
        $config = Add-AzureRmHDInsightScriptAction -Config $config -Name "Install Giraph"  -NodeType WorkerNode -Uri https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

    <span data-ttu-id="dcbf8-258">The **Add-AzureRmHDInsightScriptAction** cmdlet takes the following parameters:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-258">The **Add-AzureRmHDInsightScriptAction** cmdlet takes the following parameters:</span></span>

    | <span data-ttu-id="dcbf8-259">Parameter</span><span class="sxs-lookup"><span data-stu-id="dcbf8-259">Parameter</span></span> | <span data-ttu-id="dcbf8-260">Definition</span><span class="sxs-lookup"><span data-stu-id="dcbf8-260">Definition</span></span> |
    | --- | --- |
    | <span data-ttu-id="dcbf8-261">Config</span><span class="sxs-lookup"><span data-stu-id="dcbf8-261">Config</span></span> |<span data-ttu-id="dcbf8-262">Configuration object to which script action information is added.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-262">Configuration object to which script action information is added.</span></span> |
    | <span data-ttu-id="dcbf8-263">Name</span><span class="sxs-lookup"><span data-stu-id="dcbf8-263">Name</span></span> |<span data-ttu-id="dcbf8-264">Name of the script action.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-264">Name of the script action.</span></span> |
    | <span data-ttu-id="dcbf8-265">NodeType</span><span class="sxs-lookup"><span data-stu-id="dcbf8-265">NodeType</span></span> |<span data-ttu-id="dcbf8-266">Specifies the node on which the customization script is run.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-266">Specifies the node on which the customization script is run.</span></span> <span data-ttu-id="dcbf8-267">The valid values are **HeadNode** (to install on the head node), **WorkerNode** (to install on all the data nodes), or **ZookeeperNode** (to install on the zookeeper node).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-267">The valid values are **HeadNode** (to install on the head node), **WorkerNode** (to install on all the data nodes), or **ZookeeperNode** (to install on the zookeeper node).</span></span> |
    | <span data-ttu-id="dcbf8-268">Parameters</span><span class="sxs-lookup"><span data-stu-id="dcbf8-268">Parameters</span></span> |<span data-ttu-id="dcbf8-269">Parameters required by the script.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-269">Parameters required by the script.</span></span> |
    | <span data-ttu-id="dcbf8-270">Uri</span><span class="sxs-lookup"><span data-stu-id="dcbf8-270">Uri</span></span> |<span data-ttu-id="dcbf8-271">Specifies the URI to the script that is executed.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-271">Specifies the URI to the script that is executed.</span></span> |

4. <span data-ttu-id="dcbf8-272">Set the admin/HTTPS user for the cluster:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-272">Set the admin/HTTPS user for the cluster:</span></span>

        $httpCreds = get-credential

    <span data-ttu-id="dcbf8-273">When prompted, enter 'admin' as the name, and provide a password.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-273">When prompted, enter 'admin' as the name, and provide a password.</span></span>

5. <span data-ttu-id="dcbf8-274">Set the SSH credentials:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-274">Set the SSH credentials:</span></span>

        $sshCreds = get-credential

    <span data-ttu-id="dcbf8-275">When prompted, enter the SSH user name and password.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-275">When prompted, enter the SSH user name and password.</span></span> <span data-ttu-id="dcbf8-276">If you want to secure the SSH account with a certificate instead of a password, use a blank password and set `$sshPublicKey` to the contents of the certificate public key you wish to use.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-276">If you want to secure the SSH account with a certificate instead of a password, use a blank password and set `$sshPublicKey` to the contents of the certificate public key you wish to use.</span></span> <span data-ttu-id="dcbf8-277">For example:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-277">For example:</span></span>

        $sshPublicKey = Get-Content .\path\to\public.key -Raw

6. <span data-ttu-id="dcbf8-278">Finally, create the cluster:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-278">Finally, create the cluster:</span></span>

        New-AzureRmHDInsightCluster -config $config -clustername $clusterName -DefaultStorageContainer $containerName -Location $location -ResourceGroupName $resourceGroupName -ClusterSizeInNodes $clusterNodes -HttpCredential $httpCreds -SshCredential $sshCreds -OSType Linux

    <span data-ttu-id="dcbf8-279">If you are using a public key to secure your SSH account, you must also specify `-SshPublicKey $sshPublicKey` as a parameter.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-279">If you are using a public key to secure your SSH account, you must also specify `-SshPublicKey $sshPublicKey` as a parameter.</span></span>

<span data-ttu-id="dcbf8-280">It can take several minutes before the cluster is created.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-280">It can take several minutes before the cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a><span data-ttu-id="dcbf8-281">Use a Script Action during cluster creation from the HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="dcbf8-281">Use a Script Action during cluster creation from the HDInsight .NET SDK</span></span>

<span data-ttu-id="dcbf8-282">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-282">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span></span> <span data-ttu-id="dcbf8-283">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-283">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-to-a-running-cluster"></a><span data-ttu-id="dcbf8-284">Apply a Script Action to a running cluster</span><span class="sxs-lookup"><span data-stu-id="dcbf8-284">Apply a Script Action to a running cluster</span></span>

<span data-ttu-id="dcbf8-285">This section provides examples on the different ways you can apply script actions to a running HDInsight cluster; from the Azure portal, using PowerShell CMDlets, using the cross-platform Azure CLI, and using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-285">This section provides examples on the different ways you can apply script actions to a running HDInsight cluster; from the Azure portal, using PowerShell CMDlets, using the cross-platform Azure CLI, and using the .NET SDK.</span></span> <span data-ttu-id="dcbf8-286">The persisted script action used in this section adds an existing Azure storage account to a running cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-286">The persisted script action used in this section adds an existing Azure storage account to a running cluster.</span></span> <span data-ttu-id="dcbf8-287">You can also use other script actions, See [Example Script Action scripts](#example-script-action-scripts).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-287">You can also use other script actions, See [Example Script Action scripts](#example-script-action-scripts).</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a><span data-ttu-id="dcbf8-288">Apply a Script Action to a running cluster from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dcbf8-288">Apply a Script Action to a running cluster from the Azure portal</span></span>

1. <span data-ttu-id="dcbf8-289">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-289">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="dcbf8-290">From the HDInsight cluster blade, select the **Script Actions** tile.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-290">From the HDInsight cluster blade, select the **Script Actions** tile.</span></span>

    ![Script actions tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="dcbf8-292">You can also select **All settings** and then select **Script Actions** from the Settings blade.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-292">You can also select **All settings** and then select **Script Actions** from the Settings blade.</span></span>

3. <span data-ttu-id="dcbf8-293">From the top of the Script Actions blade, select **Submit new**.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-293">From the top of the Script Actions blade, select **Submit new**.</span></span>

    ![Submit new icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/newscriptaction.png)

4. <span data-ttu-id="dcbf8-295">From the Add Script Action blade, enter the following information.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-295">From the Add Script Action blade, enter the following information.</span></span>

   * <span data-ttu-id="dcbf8-296">**Name**: The friendly name to use for this Script Action.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-296">**Name**: The friendly name to use for this Script Action.</span></span> <span data-ttu-id="dcbf8-297">In this example, `Add Storage account`.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-297">In this example, `Add Storage account`.</span></span>

   * <span data-ttu-id="dcbf8-298">**SCRIPT URI**: The URI to the script.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-298">**SCRIPT URI**: The URI to the script.</span></span> <span data-ttu-id="dcbf8-299">In this example, `https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh`</span><span class="sxs-lookup"><span data-stu-id="dcbf8-299">In this example, `https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh`</span></span>

   * <span data-ttu-id="dcbf8-300">**Head**, **Worker**, and **Zookeeper**: Check the nodes that this script should be applied to.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-300">**Head**, **Worker**, and **Zookeeper**: Check the nodes that this script should be applied to.</span></span> <span data-ttu-id="dcbf8-301">In this example, Head, Worker and Zookeeper are checked.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-301">In this example, Head, Worker and Zookeeper are checked.</span></span>

   * <span data-ttu-id="dcbf8-302">**PARAMETERS**: If the script accepts parameters, enter them here.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-302">**PARAMETERS**: If the script accepts parameters, enter them here.</span></span> <span data-ttu-id="dcbf8-303">In this example, enter the storage account name, and the storage account key:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-303">In this example, enter the storage account name, and the storage account key:</span></span>

       ![hdinsight persisted script action acc storage account to running clusters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/hdinsight-persisted-script-action-add-storage-account.png)

       <span data-ttu-id="dcbf8-305">On the screenshot, `contosodata` is an existing Azure Storage account, the second line is the Storage account key.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-305">On the screenshot, `contosodata` is an existing Azure Storage account, the second line is the Storage account key.</span></span>

   * <span data-ttu-id="dcbf8-306">**PERSISTED**: Check this entry if you want to persist the script so it is applied to new worker nodes when you scale up the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-306">**PERSISTED**: Check this entry if you want to persist the script so it is applied to new worker nodes when you scale up the cluster.</span></span>

5. <span data-ttu-id="dcbf8-307">Finally, use the **Create** button to apply the script to the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-307">Finally, use the **Create** button to apply the script to the cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a><span data-ttu-id="dcbf8-308">Apply a Script Action to a running cluster from Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcbf8-308">Apply a Script Action to a running cluster from Azure PowerShell</span></span>

<span data-ttu-id="dcbf8-309">Before proceeding, make sure you have installed and configured Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-309">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="dcbf8-310">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-310">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

1. <span data-ttu-id="dcbf8-311">Open the Azure PowerShell console and use the following to log in to your Azure subscription and declare some PowerShell variables:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-311">Open the Azure PowerShell console and use the following to log in to your Azure subscription and declare some PowerShell variables:</span></span>

        # LOGIN TO ZURE
        Login-AzureRmAccount

        # PROVIDE VALUES FOR THESE VARIABLES
        $clusterName = "<HDInsightClusterName>"            # HDInsight cluster name
        $saName = "<ScriptActionName>"                  # Name of the script action
        $saURI = "<URI to the script>"                  # The URI where the script is located
        $nodeTypes = "headnode", "workernode"

   > [!NOTE]
   > <span data-ttu-id="dcbf8-312">If using an HDInsight Premium cluster, you can use a nodetype of `"edgenode"` to run the script on the edge node.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-312">If using an HDInsight Premium cluster, you can use a nodetype of `"edgenode"` to run the script on the edge node.</span></span>

2. <span data-ttu-id="dcbf8-313">Use the following command to apply the script to the cluster:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-313">Use the following command to apply the script to the cluster:</span></span>

        Submit-AzureRmHDInsightScriptAction -ClusterName $clusterName -Name $saName -Uri $saURI -NodeTypes $nodeTypes -PersistOnSuccess

    <span data-ttu-id="dcbf8-314">Once the job completes, you should receive information similar to the following:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-314">Once the job completes, you should receive information similar to the following:</span></span>

        OperationState  : Succeeded
        ErrorMessage    :
        Name            : Giraph
        Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
        Parameters      :
        NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a><span data-ttu-id="dcbf8-315">Apply a Script Action to a running cluster from the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dcbf8-315">Apply a Script Action to a running cluster from the Azure CLI</span></span>

<span data-ttu-id="dcbf8-316">Before proceeding, make sure you have installed and configured the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-316">Before proceeding, make sure you have installed and configured the Azure CLI.</span></span> <span data-ttu-id="dcbf8-317">For more information, see [Install the Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-317">For more information, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="dcbf8-318">Open a shell session, terminal, command-prompt or other command line for your system and use the following command to switch to Azure Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-318">Open a shell session, terminal, command-prompt or other command line for your system and use the following command to switch to Azure Resource Manager mode.</span></span>

        azure config mode arm

2. <span data-ttu-id="dcbf8-319">Use the following to authenticate to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-319">Use the following to authenticate to your Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="dcbf8-320">Use the following command to apply a script action to a running cluster</span><span class="sxs-lookup"><span data-stu-id="dcbf8-320">Use the following command to apply a script action to a running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="dcbf8-321">If you omit parameters for this command, you are prompted for them.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-321">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="dcbf8-322">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-322">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span></span>

    <span data-ttu-id="dcbf8-323">Valid **nodetypes** are **headnode**, **workernode**, and **zookeeper**.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-323">Valid **nodetypes** are **headnode**, **workernode**, and **zookeeper**.</span></span> <span data-ttu-id="dcbf8-324">If the script should be applied to multiple node types, specify the types separated by a ';'.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-324">If the script should be applied to multiple node types, specify the types separated by a ';'.</span></span> <span data-ttu-id="dcbf8-325">For example, `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-325">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="dcbf8-326">To persist the script, add the `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-326">To persist the script, add the `--persistOnSuccess`.</span></span> <span data-ttu-id="dcbf8-327">You can also persist the script at a later date by using `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-327">You can also persist the script at a later date by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="dcbf8-328">Once the job completes, you receive output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-328">Once the job completes, you receive output similar to the following.</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a><span data-ttu-id="dcbf8-329">Apply a Script Action to a running cluster using REST API</span><span class="sxs-lookup"><span data-stu-id="dcbf8-329">Apply a Script Action to a running cluster using REST API</span></span>

<span data-ttu-id="dcbf8-330">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-330">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a><span data-ttu-id="dcbf8-331">Apply a Script Action to a running cluster from the HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="dcbf8-331">Apply a Script Action to a running cluster from the HDInsight .NET SDK</span></span>

<span data-ttu-id="dcbf8-332">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-332">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="dcbf8-333">View history, promote, and demote Script Actions</span><span class="sxs-lookup"><span data-stu-id="dcbf8-333">View history, promote, and demote Script Actions</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="dcbf8-334">Using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dcbf8-334">Using the Azure portal</span></span>

1. <span data-ttu-id="dcbf8-335">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-335">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="dcbf8-336">From the HDInsight cluster blade, select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-336">From the HDInsight cluster blade, select **Settings**.</span></span>

    ![Settings icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/settingsicon.png)

3. <span data-ttu-id="dcbf8-338">From the Settings blade, select **Script Actions**.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-338">From the Settings blade, select **Script Actions**.</span></span>

    ![Script Actions link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/settings.png)

4. <span data-ttu-id="dcbf8-340">A list of the persisted scripts, as well as a history of scripts applied to the cluster, is displayed on the Script Actions blade.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-340">A list of the persisted scripts, as well as a history of scripts applied to the cluster, is displayed on the Script Actions blade.</span></span> <span data-ttu-id="dcbf8-341">In the screenshot below, you can see that the Solr script has been ran on this cluster, but that no script actions have been persisted.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-341">In the screenshot below, you can see that the Solr script has been ran on this cluster, but that no script actions have been persisted.</span></span>

    ![Script Actions blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/scriptactionhistory.png)

5. <span data-ttu-id="dcbf8-343">Selecting a script from the history displays the Properties blade for this script.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-343">Selecting a script from the history displays the Properties blade for this script.</span></span> <span data-ttu-id="dcbf8-344">From the top of the blade, you can rerun the script or promote it.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-344">From the top of the blade, you can rerun the script or promote it.</span></span>

    ![Script actions properties blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/scriptactionproperties.png)

6. <span data-ttu-id="dcbf8-346">You can also use the **...** to the right of entries on the Script Actions blade to perform actions such as rerun, persist, or (for persisted actions,) delete.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-346">You can also use the **...** to the right of entries on the Script Actions blade to perform actions such as rerun, persist, or (for persisted actions,) delete.</span></span>

    ![Script actions ... usage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="dcbf8-348">Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcbf8-348">Using Azure PowerShell</span></span>

| <span data-ttu-id="dcbf8-349">Use the following...</span><span class="sxs-lookup"><span data-stu-id="dcbf8-349">Use the following...</span></span> | <span data-ttu-id="dcbf8-350">To ...</span><span class="sxs-lookup"><span data-stu-id="dcbf8-350">To ...</span></span> |
| --- | --- |
| <span data-ttu-id="dcbf8-351">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="dcbf8-351">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="dcbf8-352">Retrieve information on persisted script actions</span><span class="sxs-lookup"><span data-stu-id="dcbf8-352">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="dcbf8-353">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="dcbf8-353">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="dcbf8-354">Retrieve a history of script actions applied to the cluster, or details for a specific script</span><span class="sxs-lookup"><span data-stu-id="dcbf8-354">Retrieve a history of script actions applied to the cluster, or details for a specific script</span></span> |
| <span data-ttu-id="dcbf8-355">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="dcbf8-355">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="dcbf8-356">Promotes an ad hoc script action to a persisted script action</span><span class="sxs-lookup"><span data-stu-id="dcbf8-356">Promotes an ad hoc script action to a persisted script action</span></span> |
| <span data-ttu-id="dcbf8-357">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="dcbf8-357">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="dcbf8-358">Demotes a persisted script action to an ad hoc action</span><span class="sxs-lookup"><span data-stu-id="dcbf8-358">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="dcbf8-359">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script, it only removes the persisted flag so that the script is not ran on new worker nodes added to the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-359">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script, it only removes the persisted flag so that the script is not ran on new worker nodes added to the cluster.</span></span>

<span data-ttu-id="dcbf8-360">The following example script demonstrates using the cmdlets to promote, then demote a script.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-360">The following example script demonstrates using the cmdlets to promote, then demote a script.</span></span>

    # Get a history of scripts
    Get-AzureRmHDInsightScriptActionHistory -ClusterName mycluster

    # From the list, we want to get information on a specific script
    Get-AzureRmHDInsightScriptActionHistory -ClusterName mycluster -ScriptExecutionId 635920937765978529

    # Promote this to a persisted script
    # Note: the script must have a unique name to be promoted
    # if the name is not unique, you receive an error
    Set-AzureRmHDInsightPersistedScriptAction -ClusterName mycluster -ScriptExecutionId 635920937765978529

    # Demote the script back to ad hoc
    # Note that demotion uses the unique script name instead of
    # execution ID.
    Remove-AzureRmHDInsightPersistedScriptAction -ClusterName mycluster -Name "Install Giraph"

### <a name="using-the-azure-cli"></a><span data-ttu-id="dcbf8-361">Using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dcbf8-361">Using the Azure CLI</span></span>

| <span data-ttu-id="dcbf8-362">Use the following...</span><span class="sxs-lookup"><span data-stu-id="dcbf8-362">Use the following...</span></span> | <span data-ttu-id="dcbf8-363">To ...</span><span class="sxs-lookup"><span data-stu-id="dcbf8-363">To ...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="dcbf8-364">Retrieve a list of persisted script actions</span><span class="sxs-lookup"><span data-stu-id="dcbf8-364">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="dcbf8-365">Retrieve information on a specific persisted script action</span><span class="sxs-lookup"><span data-stu-id="dcbf8-365">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="dcbf8-366">Retrieve a history of script actions applied to the cluster</span><span class="sxs-lookup"><span data-stu-id="dcbf8-366">Retrieve a history of script actions applied to the cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="dcbf8-367">Retrieve information on a specific script action</span><span class="sxs-lookup"><span data-stu-id="dcbf8-367">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="dcbf8-368">Promotes an ad hoc script action to a persisted script action</span><span class="sxs-lookup"><span data-stu-id="dcbf8-368">Promotes an ad hoc script action to a persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="dcbf8-369">Demotes a persisted script action to an ad hoc action</span><span class="sxs-lookup"><span data-stu-id="dcbf8-369">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="dcbf8-370">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script, it only removes the persisted flag so that the script is not ran on new worker nodes added to the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-370">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script, it only removes the persisted flag so that the script is not ran on new worker nodes added to the cluster.</span></span>

### <a name="using-the-hdinsight-net-sdk"></a><span data-ttu-id="dcbf8-371">Using the HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="dcbf8-371">Using the HDInsight .NET SDK</span></span>

<span data-ttu-id="dcbf8-372">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-372">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="dcbf8-373">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-373">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="dcbf8-374">Support for open-source software used on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="dcbf8-374">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="dcbf8-375">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-375">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="dcbf8-376">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-376">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="dcbf8-377">The HDInsight service provides an additional level of support for some of the components, as described below.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-377">The HDInsight service provides an additional level of support for some of the components, as described below.</span></span>

<span data-ttu-id="dcbf8-378">There are two types of open-source components that are available in the HDInsight service:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-378">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="dcbf8-379">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-379">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="dcbf8-380">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-380">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="dcbf8-381">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-381">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="dcbf8-382">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-382">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="dcbf8-383">Components provided with the HDInsight cluster are fully supported and Microsoft Support helps to isolate and resolve issues related to these components.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-383">Components provided with the HDInsight cluster are fully supported and Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="dcbf8-384">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-384">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="dcbf8-385">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-385">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="dcbf8-386">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-386">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="dcbf8-387">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-387">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="dcbf8-388">The HDInsight service provides several ways to use custom components.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-388">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="dcbf8-389">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-389">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span></span> <span data-ttu-id="dcbf8-390">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-390">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="dcbf8-391">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-391">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>

2. <span data-ttu-id="dcbf8-392">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-392">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span></span>

3. <span data-ttu-id="dcbf8-393">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-393">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="dcbf8-394">These samples are provided without support.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-394">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dcbf8-395">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="dcbf8-395">Troubleshooting</span></span>

<span data-ttu-id="dcbf8-396">You can use Ambari web UI to view information logged by script actions.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-396">You can use Ambari web UI to view information logged by script actions.</span></span> <span data-ttu-id="dcbf8-397">If the script is used during cluster creation, and cluster creation failed due to an error in the script, the logs are also available in the default storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-397">If the script is used during cluster creation, and cluster creation failed due to an error in the script, the logs are also available in the default storage account associated with the cluster.</span></span> <span data-ttu-id="dcbf8-398">This section provides information on how to retrieve the logs using both these options.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-398">This section provides information on how to retrieve the logs using both these options.</span></span>

### <a name="using-the-ambari-web-ui"></a><span data-ttu-id="dcbf8-399">Using the Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="dcbf8-399">Using the Ambari Web UI</span></span>

1. <span data-ttu-id="dcbf8-400">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-400">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="dcbf8-401">Replace CLUSTERNAME with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-401">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="dcbf8-402">When prompted, enter the admin account name (admin) and password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-402">When prompted, enter the admin account name (admin) and password for the cluster.</span></span> <span data-ttu-id="dcbf8-403">You may have to re-enter the admin credentials in a web form.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-403">You may have to re-enter the admin credentials in a web form.</span></span>

2. <span data-ttu-id="dcbf8-404">From the bar at the top of the page, select the **ops** entry.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-404">From the bar at the top of the page, select the **ops** entry.</span></span> <span data-ttu-id="dcbf8-405">This shows a list of current and previous operations performed on the cluster through Ambari.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-405">This shows a list of current and previous operations performed on the cluster through Ambari.</span></span>

    ![Ambari web UI bar with ops selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="dcbf8-407">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-407">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span></span> <span data-ttu-id="dcbf8-408">These are created when the Script Actions are ran.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-408">These are created when the Script Actions are ran.</span></span>

    ![Screenshot of operations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="dcbf8-410">Select this run\customscriptaction entry and drill down through the links to view the STDOUT and STDERR output.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-410">Select this run\customscriptaction entry and drill down through the links to view the STDOUT and STDERR output.</span></span> <span data-ttu-id="dcbf8-411">This output is generated when the script runs, and may contain useful information.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-411">This output is generated when the script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-the-default-storage-account"></a><span data-ttu-id="dcbf8-412">Access logs from the default storage account</span><span class="sxs-lookup"><span data-stu-id="dcbf8-412">Access logs from the default storage account</span></span>

<span data-ttu-id="dcbf8-413">If the cluster creation failed due to an error in script action, the script action logs can still be accessed directly from the default storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-413">If the cluster creation failed due to an error in script action, the script action logs can still be accessed directly from the default storage account associated with the cluster.</span></span>

* <span data-ttu-id="dcbf8-414">The storage logs are available at `\STORAGE_ACOCUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-414">The storage logs are available at `\STORAGE_ACOCUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Screenshot of operations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="dcbf8-416">Under this, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-416">Under this, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="dcbf8-417">Some examples are:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-417">Some examples are:</span></span>

    * <span data-ttu-id="dcbf8-418">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="dcbf8-418">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="dcbf8-419">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="dcbf8-419">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="dcbf8-420">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="dcbf8-420">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="dcbf8-421">All stdout and stderr of the corresponding host is uploaded to the storage account.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-421">All stdout and stderr of the corresponding host is uploaded to the storage account.</span></span> <span data-ttu-id="dcbf8-422">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-422">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="dcbf8-423">The output-\*.txt file contains information about the URI of the script that got run on the host.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-423">The output-\*.txt file contains information about the URI of the script that got run on the host.</span></span> <span data-ttu-id="dcbf8-424">For example</span><span class="sxs-lookup"><span data-stu-id="dcbf8-424">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="dcbf8-425">It's possible that you repeatedly create a script action cluster with the same name.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-425">It's possible that you repeatedly create a script action cluster with the same name.</span></span> <span data-ttu-id="dcbf8-426">In such case, you can distinguish the relevant logs based on the DATE folder name.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-426">In such case, you can distinguish the relevant logs based on the DATE folder name.</span></span> <span data-ttu-id="dcbf8-427">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-427">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following:</span></span>

    * `\STORAGE_ACOCUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04`

    * `\STORAGE_ACOCUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* <span data-ttu-id="dcbf8-428">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-428">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span></span>

* <span data-ttu-id="dcbf8-429">If you create a cluster at the end of the day, it's possible that the log files span across two days.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-429">If you create a cluster at the end of the day, it's possible that the log files span across two days.</span></span> <span data-ttu-id="dcbf8-430">In such cases, you see two different date folders for the same cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-430">In such cases, you see two different date folders for the same cluster.</span></span>

* <span data-ttu-id="dcbf8-431">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-431">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span></span> <span data-ttu-id="dcbf8-432">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-432">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="dcbf8-433">Ambari watchdog</span><span class="sxs-lookup"><span data-stu-id="dcbf8-433">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="dcbf8-434">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-434">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="dcbf8-435">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-435">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span></span>

### <a name="cannot-import-name-blobservice"></a><span data-ttu-id="dcbf8-436">Cannot import name BlobService</span><span class="sxs-lookup"><span data-stu-id="dcbf8-436">Cannot import name BlobService</span></span>

<span data-ttu-id="dcbf8-437">__Symptoms__: The script action fails, and an error similar to the following is displayed when you view the operation in Ambari:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-437">__Symptoms__: The script action fails, and an error similar to the following is displayed when you view the operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="dcbf8-438">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-438">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span></span> <span data-ttu-id="dcbf8-439">HDInsight expects Azure Storage client 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-439">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="dcbf8-440">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-440">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="dcbf8-441">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf8-441">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="dcbf8-442">History doesn't show scripts used during cluster creation</span><span class="sxs-lookup"><span data-stu-id="dcbf8-442">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="dcbf8-443">If your cluster was created before March 15th, 2016, you may not see an entry in Script Action history for any scripts used during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-443">If your cluster was created before March 15th, 2016, you may not see an entry in Script Action history for any scripts used during cluster creation.</span></span> <span data-ttu-id="dcbf8-444">However, if you resize the cluster after March 15th, 2016, the scripts using during cluster creation appears in history as they are applied to new nodes in the cluster as part of the resize operation.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-444">However, if you resize the cluster after March 15th, 2016, the scripts using during cluster creation appears in history as they are applied to new nodes in the cluster as part of the resize operation.</span></span>

<span data-ttu-id="dcbf8-445">There are two exceptions:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-445">There are two exceptions:</span></span>

* <span data-ttu-id="dcbf8-446">If your cluster was created before September 1st, 2015.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-446">If your cluster was created before September 1st, 2015.</span></span> <span data-ttu-id="dcbf8-447">This is when Script Actions were introduced, so any cluster created before this date could not have used Script Actions for cluster creation.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-447">This is when Script Actions were introduced, so any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="dcbf8-448">If you used multiple Script Actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-448">If you used multiple Script Actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="dcbf8-449">In these cases, you receive the following error.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-449">In these cases, you receive the following error.</span></span>

    <span data-ttu-id="dcbf8-450">No new script actions can be executed on this cluster due to conflicting script names in existing scripts.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-450">No new script actions can be executed on this cluster due to conflicting script names in existing scripts.</span></span> <span data-ttu-id="dcbf8-451">Script names provided at cluster create must be all unique.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-451">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="dcbf8-452">Existing scripts will still be executed on resize.</span><span class="sxs-lookup"><span data-stu-id="dcbf8-452">Existing scripts will still be executed on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcbf8-453">Next steps</span><span class="sxs-lookup"><span data-stu-id="dcbf8-453">Next steps</span></span>

<span data-ttu-id="dcbf8-454">See the following for information and examples on creating and using scripts to customize a cluster:</span><span class="sxs-lookup"><span data-stu-id="dcbf8-454">See the following for information and examples on creating and using scripts to customize a cluster:</span></span>

* [<span data-ttu-id="dcbf8-455">Develop Script Action scripts for HDInsight</span><span class="sxs-lookup"><span data-stu-id="dcbf8-455">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="dcbf8-456">Install and use Solr on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="dcbf8-456">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="dcbf8-457">Install and use Giraph on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="dcbf8-457">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="dcbf8-458">Add additional storage to an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="dcbf8-458">Add additional storage to an HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Stages during cluster creation"













