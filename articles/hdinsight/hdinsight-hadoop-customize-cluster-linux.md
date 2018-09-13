---
title: Customize HDInsight clusters using script actions - Azure
description: Add custom components to Linux-based HDInsight clusters using script actions. Script actions are Bash scripts  that can be used to customize the cluster configuration or add additional services and utilities like Hue, Solr, or R.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/01/2018
ms.author: jasonh
ms.openlocfilehash: 3c0af8f46f4ffde34d664229821d84161622b315
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800259"
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-actions"></a><span data-ttu-id="15df8-104">Customize Linux-based HDInsight clusters using script actions</span><span class="sxs-lookup"><span data-stu-id="15df8-104">Customize Linux-based HDInsight clusters using script actions</span></span>

<span data-ttu-id="15df8-105">HDInsight provides a configuration method called **script actions** that invokes custom scripts to customize the cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-105">HDInsight provides a configuration method called **script actions** that invokes custom scripts to customize the cluster.</span></span> <span data-ttu-id="15df8-106">These scripts are used to install additional components and change configuration settings.</span><span class="sxs-lookup"><span data-stu-id="15df8-106">These scripts are used to install additional components and change configuration settings.</span></span> <span data-ttu-id="15df8-107">Script actions can be used during or after cluster creation.</span><span class="sxs-lookup"><span data-stu-id="15df8-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15df8-108">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="15df8-108">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="15df8-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="15df8-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="15df8-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="15df8-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="15df8-111">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span><span class="sxs-lookup"><span data-stu-id="15df8-111">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="15df8-112">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-112">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="15df8-113">Permissions</span><span class="sxs-lookup"><span data-stu-id="15df8-113">Permissions</span></span>

<span data-ttu-id="15df8-114">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span><span class="sxs-lookup"><span data-stu-id="15df8-114">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span></span>

* <span data-ttu-id="15df8-115">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span><span class="sxs-lookup"><span data-stu-id="15df8-115">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="15df8-116">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span><span class="sxs-lookup"><span data-stu-id="15df8-116">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="15df8-117">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](./domain-joined/apache-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-117">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](./domain-joined/apache-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="15df8-118">Access control</span><span class="sxs-lookup"><span data-stu-id="15df8-118">Access control</span></span>

<span data-ttu-id="15df8-119">If you are not the administrator/owner of your Azure subscription, your account must have at least **Contributor** access to the resource group that contains the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-119">If you are not the administrator/owner of your Azure subscription, your account must have at least **Contributor** access to the resource group that contains the HDInsight cluster.</span></span>

<span data-ttu-id="15df8-120">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="15df8-120">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span></span> <span data-ttu-id="15df8-121">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span><span class="sxs-lookup"><span data-stu-id="15df8-121">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span></span> <span data-ttu-id="15df8-122">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="15df8-122">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="15df8-123">For more information on working with access management, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="15df8-123">For more information on working with access management, see the following documents:</span></span>

* [<span data-ttu-id="15df8-124">Get started with access management in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="15df8-124">Get started with access management in the Azure portal</span></span>](../role-based-access-control/overview.md)
* [<span data-ttu-id="15df8-125">Use role assignments to manage access to your Azure subscription resources</span><span class="sxs-lookup"><span data-stu-id="15df8-125">Use role assignments to manage access to your Azure subscription resources</span></span>](../role-based-access-control/role-assignments-portal.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="15df8-126">Understanding script actions</span><span class="sxs-lookup"><span data-stu-id="15df8-126">Understanding script actions</span></span>

<span data-ttu-id="15df8-127">A script action is Bash script that runs on the nodes in an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-127">A script action is Bash script that runs on the nodes in an HDInsight cluster.</span></span> <span data-ttu-id="15df8-128">The following are characteristics and features of script actions.</span><span class="sxs-lookup"><span data-stu-id="15df8-128">The following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="15df8-129">Must be stored on a URI that is accessible from the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-129">Must be stored on a URI that is accessible from the HDInsight cluster.</span></span> <span data-ttu-id="15df8-130">The following are possible storage locations:</span><span class="sxs-lookup"><span data-stu-id="15df8-130">The following are possible storage locations:</span></span>

    * <span data-ttu-id="15df8-131">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-131">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span></span> <span data-ttu-id="15df8-132">For information on using Azure Data Lake Store with HDInsight, see [Quickstart: Set up clusters in HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-132">For information on using Azure Data Lake Store with HDInsight, see [Quickstart: Set up clusters in HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span></span>

        <span data-ttu-id="15df8-133">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="15df8-133">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="15df8-134">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span><span class="sxs-lookup"><span data-stu-id="15df8-134">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

    * <span data-ttu-id="15df8-135">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-135">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span></span> <span data-ttu-id="15df8-136">HDInsight is granted access to both of these types of storage accounts during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="15df8-136">HDInsight is granted access to both of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="15df8-137">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span><span class="sxs-lookup"><span data-stu-id="15df8-137">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="15df8-138">For example URIs, see the [Example script action scripts](#example-script-action-scripts) section.</span><span class="sxs-lookup"><span data-stu-id="15df8-138">For example URIs, see the [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="15df8-139">HDInsight only supports __General-purpose__ Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="15df8-139">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="15df8-140">It does not currently support the __Blob storage__ account type.</span><span class="sxs-lookup"><span data-stu-id="15df8-140">It does not currently support the __Blob storage__ account type.</span></span>

* <span data-ttu-id="15df8-141">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span><span class="sxs-lookup"><span data-stu-id="15df8-141">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span></span>

* <span data-ttu-id="15df8-142">Can be **persisted** or **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="15df8-142">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="15df8-143">**Persisted** scripts are used to customize new worker nodes added to the cluster through scaling operations.</span><span class="sxs-lookup"><span data-stu-id="15df8-143">**Persisted** scripts are used to customize new worker nodes added to the cluster through scaling operations.</span></span> <span data-ttu-id="15df8-144">A persisted script might also apply changes to another node type, such as a head node, when scaling operations occur.</span><span class="sxs-lookup"><span data-stu-id="15df8-144">A persisted script might also apply changes to another node type, such as a head node, when scaling operations occur.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="15df8-145">Persisted script actions must have a unique name.</span><span class="sxs-lookup"><span data-stu-id="15df8-145">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="15df8-146">**Ad hoc** scripts are not persisted.</span><span class="sxs-lookup"><span data-stu-id="15df8-146">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="15df8-147">They are not applied to worker nodes added to the cluster after the script has ran.</span><span class="sxs-lookup"><span data-stu-id="15df8-147">They are not applied to worker nodes added to the cluster after the script has ran.</span></span> <span data-ttu-id="15df8-148">You can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span><span class="sxs-lookup"><span data-stu-id="15df8-148">You can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="15df8-149">Script actions used during cluster creation are automatically persisted.</span><span class="sxs-lookup"><span data-stu-id="15df8-149">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="15df8-150">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span><span class="sxs-lookup"><span data-stu-id="15df8-150">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="15df8-151">Can accept **parameters** that are used by the script during execution.</span><span class="sxs-lookup"><span data-stu-id="15df8-151">Can accept **parameters** that are used by the script during execution.</span></span>

* <span data-ttu-id="15df8-152">Run with **root level privileges** on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="15df8-152">Run with **root level privileges** on the cluster nodes.</span></span>

* <span data-ttu-id="15df8-153">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI v1.0**, or **HDInsight .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="15df8-153">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI v1.0**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="15df8-154">The cluster keeps a history of all scripts that have been ran.</span><span class="sxs-lookup"><span data-stu-id="15df8-154">The cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="15df8-155">The history is useful when you need to find the ID of a script for promotion or demotion operations.</span><span class="sxs-lookup"><span data-stu-id="15df8-155">The history is useful when you need to find the ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15df8-156">There is no automatic way to undo the changes made by a script action.</span><span class="sxs-lookup"><span data-stu-id="15df8-156">There is no automatic way to undo the changes made by a script action.</span></span> <span data-ttu-id="15df8-157">Either manually reverse the changes or provide a script that reverses them.</span><span class="sxs-lookup"><span data-stu-id="15df8-157">Either manually reverse the changes or provide a script that reverses them.</span></span>

### <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="15df8-158">Script action in the cluster creation process</span><span class="sxs-lookup"><span data-stu-id="15df8-158">Script action in the cluster creation process</span></span>

<span data-ttu-id="15df8-159">Script actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span><span class="sxs-lookup"><span data-stu-id="15df8-159">Script actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="15df8-160">The script is **automatically persisted**.</span><span class="sxs-lookup"><span data-stu-id="15df8-160">The script is **automatically persisted**.</span></span>

* <span data-ttu-id="15df8-161">A **failure** in the script can cause the cluster creation process to fail.</span><span class="sxs-lookup"><span data-stu-id="15df8-161">A **failure** in the script can cause the cluster creation process to fail.</span></span>

<span data-ttu-id="15df8-162">The following diagram illustrates when script action is executed during the creation process:</span><span class="sxs-lookup"><span data-stu-id="15df8-162">The following diagram illustrates when script action is executed during the creation process:</span></span>

<span data-ttu-id="15df8-163">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="15df8-163">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="15df8-164">The script runs while HDInsight is being configured.</span><span class="sxs-lookup"><span data-stu-id="15df8-164">The script runs while HDInsight is being configured.</span></span> <span data-ttu-id="15df8-165">The script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span><span class="sxs-lookup"><span data-stu-id="15df8-165">The script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="15df8-166">You can perform operations like stopping and starting services, including Hadoop-related services.</span><span class="sxs-lookup"><span data-stu-id="15df8-166">You can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="15df8-167">If you stop services, you must ensure that the Ambari service and other Hadoop-related services running before the script completes.</span><span class="sxs-lookup"><span data-stu-id="15df8-167">If you stop services, you must ensure that the Ambari service and other Hadoop-related services running before the script completes.</span></span> <span data-ttu-id="15df8-168">These services are required to successfully determine the health and state of the cluster while it is being created.</span><span class="sxs-lookup"><span data-stu-id="15df8-168">These services are required to successfully determine the health and state of the cluster while it is being created.</span></span>


<span data-ttu-id="15df8-169">During cluster creation, you can use multiple script actions at once.</span><span class="sxs-lookup"><span data-stu-id="15df8-169">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="15df8-170">These scripts are invoked in the order in which they were specified.</span><span class="sxs-lookup"><span data-stu-id="15df8-170">These scripts are invoked in the order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15df8-171">Script actions must complete within 60 minutes, or timeout.</span><span class="sxs-lookup"><span data-stu-id="15df8-171">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="15df8-172">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span><span class="sxs-lookup"><span data-stu-id="15df8-172">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="15df8-173">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span><span class="sxs-lookup"><span data-stu-id="15df8-173">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>
>
> <span data-ttu-id="15df8-174">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span><span class="sxs-lookup"><span data-stu-id="15df8-174">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="15df8-175">Pre-compile applications and store the binary in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="15df8-175">Pre-compile applications and store the binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="15df8-176">Script action on a running cluster</span><span class="sxs-lookup"><span data-stu-id="15df8-176">Script action on a running cluster</span></span>

<span data-ttu-id="15df8-177">A failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span><span class="sxs-lookup"><span data-stu-id="15df8-177">A failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span></span> <span data-ttu-id="15df8-178">Once a script completes, the cluster should return to a "running" state.</span><span class="sxs-lookup"><span data-stu-id="15df8-178">Once a script completes, the cluster should return to a "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15df8-179">Even if the cluster has a 'running' state, the failed script may have broken things.</span><span class="sxs-lookup"><span data-stu-id="15df8-179">Even if the cluster has a 'running' state, the failed script may have broken things.</span></span> <span data-ttu-id="15df8-180">For example, a script could delete files needed by the cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-180">For example, a script could delete files needed by the cluster.</span></span>
>
> <span data-ttu-id="15df8-181">Scripts actions run with root privileges.</span><span class="sxs-lookup"><span data-stu-id="15df8-181">Scripts actions run with root privileges.</span></span> <span data-ttu-id="15df8-182">Make sure that you understand what a script does before applying it to your cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-182">Make sure that you understand what a script does before applying it to your cluster.</span></span>

<span data-ttu-id="15df8-183">When applying a script to a cluster, the cluster state changes from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span><span class="sxs-lookup"><span data-stu-id="15df8-183">When applying a script to a cluster, the cluster state changes from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span></span> <span data-ttu-id="15df8-184">The script status is logged in the script action history, and you can use this information to determine whether the script succeeded or failed.</span><span class="sxs-lookup"><span data-stu-id="15df8-184">The script status is logged in the script action history, and you can use this information to determine whether the script succeeded or failed.</span></span> <span data-ttu-id="15df8-185">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span><span class="sxs-lookup"><span data-stu-id="15df8-185">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span></span> <span data-ttu-id="15df8-186">It returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="15df8-186">It returns information similar to the following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!IMPORTANT]
> <span data-ttu-id="15df8-187">If you have changed the cluster user (admin) password after the cluster was created, script actions ran against this cluster may fail.</span><span class="sxs-lookup"><span data-stu-id="15df8-187">If you have changed the cluster user (admin) password after the cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="15df8-188">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale the cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-188">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale the cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="15df8-189">Example script action scripts</span><span class="sxs-lookup"><span data-stu-id="15df8-189">Example script action scripts</span></span>

<span data-ttu-id="15df8-190">Script action scripts can be used through the following utilities:</span><span class="sxs-lookup"><span data-stu-id="15df8-190">Script action scripts can be used through the following utilities:</span></span>

* <span data-ttu-id="15df8-191">Azure portal</span><span class="sxs-lookup"><span data-stu-id="15df8-191">Azure portal</span></span>
* <span data-ttu-id="15df8-192">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="15df8-192">Azure PowerShell</span></span>
* <span data-ttu-id="15df8-193">Azure CLI v1.0</span><span class="sxs-lookup"><span data-stu-id="15df8-193">Azure CLI v1.0</span></span>
* <span data-ttu-id="15df8-194">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="15df8-194">HDInsight .NET SDK</span></span>

<span data-ttu-id="15df8-195">HDInsight provides scripts to install the following components on HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="15df8-195">HDInsight provides scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="15df8-196">Name</span><span class="sxs-lookup"><span data-stu-id="15df8-196">Name</span></span> | <span data-ttu-id="15df8-197">Script</span><span class="sxs-lookup"><span data-stu-id="15df8-197">Script</span></span> |
| --- | --- |
| <span data-ttu-id="15df8-198">**Add an Azure Storage account**</span><span class="sxs-lookup"><span data-stu-id="15df8-198">**Add an Azure Storage account**</span></span> |<span data-ttu-id="15df8-199">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-199">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="15df8-200">**Install Hue**</span><span class="sxs-lookup"><span data-stu-id="15df8-200">**Install Hue**</span></span> |<span data-ttu-id="15df8-201">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-201">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="15df8-202">**Install Presto**</span><span class="sxs-lookup"><span data-stu-id="15df8-202">**Install Presto**</span></span> |<span data-ttu-id="15df8-203">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-203">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="15df8-204">**Install Solr**</span><span class="sxs-lookup"><span data-stu-id="15df8-204">**Install Solr**</span></span> |<span data-ttu-id="15df8-205">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-205">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="15df8-206">**Install Giraph**</span><span class="sxs-lookup"><span data-stu-id="15df8-206">**Install Giraph**</span></span> |<span data-ttu-id="15df8-207">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-207">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="15df8-208">**Pre-load Hive libraries**</span><span class="sxs-lookup"><span data-stu-id="15df8-208">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="15df8-209">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-209">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="15df8-210">**Install or update Mono**</span><span class="sxs-lookup"><span data-stu-id="15df8-210">**Install or update Mono**</span></span> | <span data-ttu-id="15df8-211">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="15df8-211">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="15df8-212">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-212">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="15df8-213">Use a script action during cluster creation</span><span class="sxs-lookup"><span data-stu-id="15df8-213">Use a script action during cluster creation</span></span>

<span data-ttu-id="15df8-214">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-214">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a><span data-ttu-id="15df8-215">Use a script action during cluster creation from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="15df8-215">Use a script action during cluster creation from the Azure portal</span></span>

1. <span data-ttu-id="15df8-216">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-216">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="15df8-217">During cluster creation, you will arrive at a __Cluster summary__ page.</span><span class="sxs-lookup"><span data-stu-id="15df8-217">During cluster creation, you will arrive at a __Cluster summary__ page.</span></span> <span data-ttu-id="15df8-218">From the __Cluster summary__ page, select the __edit__ link for __Advanced settings__.</span><span class="sxs-lookup"><span data-stu-id="15df8-218">From the __Cluster summary__ page, select the __edit__ link for __Advanced settings__.</span></span>

    ![Advanced settings link](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="15df8-220">From the __Advanced settings__ section, select __Script actions__.</span><span class="sxs-lookup"><span data-stu-id="15df8-220">From the __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="15df8-221">From the __Script actions__ section, select __+ Submit new__</span><span class="sxs-lookup"><span data-stu-id="15df8-221">From the __Script actions__ section, select __+ Submit new__</span></span>

    ![Submit a new script action](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="15df8-223">Use the __Select a script__ entry to select a pre-made script.</span><span class="sxs-lookup"><span data-stu-id="15df8-223">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="15df8-224">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span><span class="sxs-lookup"><span data-stu-id="15df8-224">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Add a script in the select script form](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="15df8-226">The following table describes the elements on the form:</span><span class="sxs-lookup"><span data-stu-id="15df8-226">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="15df8-227">Property</span><span class="sxs-lookup"><span data-stu-id="15df8-227">Property</span></span> | <span data-ttu-id="15df8-228">Value</span><span class="sxs-lookup"><span data-stu-id="15df8-228">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="15df8-229">Select a script</span><span class="sxs-lookup"><span data-stu-id="15df8-229">Select a script</span></span> | <span data-ttu-id="15df8-230">To use your own script, select __Custom__.</span><span class="sxs-lookup"><span data-stu-id="15df8-230">To use your own script, select __Custom__.</span></span> <span data-ttu-id="15df8-231">Otherwise, select one of the provided scripts.</span><span class="sxs-lookup"><span data-stu-id="15df8-231">Otherwise, select one of the provided scripts.</span></span> |
    | <span data-ttu-id="15df8-232">Name</span><span class="sxs-lookup"><span data-stu-id="15df8-232">Name</span></span> |<span data-ttu-id="15df8-233">Specify a name for the script action.</span><span class="sxs-lookup"><span data-stu-id="15df8-233">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="15df8-234">Bash script URI</span><span class="sxs-lookup"><span data-stu-id="15df8-234">Bash script URI</span></span> |<span data-ttu-id="15df8-235">Specify the URI of the script.</span><span class="sxs-lookup"><span data-stu-id="15df8-235">Specify the URI of the script.</span></span> |
    | <span data-ttu-id="15df8-236">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="15df8-236">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="15df8-237">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the script is run.</span><span class="sxs-lookup"><span data-stu-id="15df8-237">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the script is run.</span></span> |
    | <span data-ttu-id="15df8-238">Parameters</span><span class="sxs-lookup"><span data-stu-id="15df8-238">Parameters</span></span> |<span data-ttu-id="15df8-239">Specify the parameters, if required by the script.</span><span class="sxs-lookup"><span data-stu-id="15df8-239">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="15df8-240">Use the __Persist this script action__ entry to ensure that the script is applied during scaling operations.</span><span class="sxs-lookup"><span data-stu-id="15df8-240">Use the __Persist this script action__ entry to ensure that the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="15df8-241">Select __Create__ to save the script.</span><span class="sxs-lookup"><span data-stu-id="15df8-241">Select __Create__ to save the script.</span></span> <span data-ttu-id="15df8-242">You can then use __+ Submit new__ to add another script.</span><span class="sxs-lookup"><span data-stu-id="15df8-242">You can then use __+ Submit new__ to add another script.</span></span>

    ![Multiple script actions](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="15df8-244">When you are done adding scripts, use the __Select__ button, and then the __Next__ button to return to the __Cluster summary__ section.</span><span class="sxs-lookup"><span data-stu-id="15df8-244">When you are done adding scripts, use the __Select__ button, and then the __Next__ button to return to the __Cluster summary__ section.</span></span>

3. <span data-ttu-id="15df8-245">To create the cluster, select __Create__ from the __Cluster summary__ selection.</span><span class="sxs-lookup"><span data-stu-id="15df8-245">To create the cluster, select __Create__ from the __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="15df8-246">Use a script action from Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="15df8-246">Use a script action from Azure Resource Manager templates</span></span>

<span data-ttu-id="15df8-247">Script actions can be used with Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="15df8-247">Script actions can be used with Azure Resource Manager templates.</span></span> <span data-ttu-id="15df8-248">For an example, see [https://azure.microsoft.com/resources/templates/hdinsight-linux-run-script-action/](https://azure.microsoft.com/resources/templates/hdinsight-linux-run-script-action/).</span><span class="sxs-lookup"><span data-stu-id="15df8-248">For an example, see [https://azure.microsoft.com/resources/templates/hdinsight-linux-run-script-action/](https://azure.microsoft.com/resources/templates/hdinsight-linux-run-script-action/).</span></span>

<span data-ttu-id="15df8-249">In this example, the script action is added using the following code:</span><span class="sxs-lookup"><span data-stu-id="15df8-249">In this example, the script action is added using the following code:</span></span>

```json
"scriptActions": [
    {
        "name": "setenvironmentvariable",
        "uri": "[parameters('scriptActionUri')]",
        "parameters": "headnode"
    }
]
```

<span data-ttu-id="15df8-250">For information on how to deploy a template, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="15df8-250">For information on how to deploy a template, see the following documents:</span></span>

* [<span data-ttu-id="15df8-251">Deploy resources with templates and Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="15df8-251">Deploy resources with templates and Azure PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)

* [<span data-ttu-id="15df8-252">Deploy resources with templates and Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15df8-252">Deploy resources with templates and Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli)

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="15df8-253">Use a script action during cluster creation from Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="15df8-253">Use a script action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="15df8-254">In this section, you use the [Add-AzureRmHDInsightScriptAction](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/add-azurermhdinsightscriptaction) cmdlet to invoke scripts to customize a cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-254">In this section, you use the [Add-AzureRmHDInsightScriptAction](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/add-azurermhdinsightscriptaction) cmdlet to invoke scripts to customize a cluster.</span></span> <span data-ttu-id="15df8-255">Before proceeding, make sure you have installed and configured Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15df8-255">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="15df8-256">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="15df8-256">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="15df8-257">The following script demonstrates how to apply a script action when creating a cluster using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="15df8-257">The following script demonstrates how to apply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="15df8-258">It can take several minutes before the cluster is created.</span><span class="sxs-lookup"><span data-stu-id="15df8-258">It can take several minutes before the cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a><span data-ttu-id="15df8-259">Use a script action during cluster creation from the HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="15df8-259">Use a script action during cluster creation from the HDInsight .NET SDK</span></span>

<span data-ttu-id="15df8-260">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span><span class="sxs-lookup"><span data-stu-id="15df8-260">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span></span> <span data-ttu-id="15df8-261">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="15df8-261">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-to-a-running-cluster"></a><span data-ttu-id="15df8-262">Apply a script action to a running cluster</span><span class="sxs-lookup"><span data-stu-id="15df8-262">Apply a script action to a running cluster</span></span>

<span data-ttu-id="15df8-263">In this section, learn how to apply script actions to a running cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-263">In this section, learn how to apply script actions to a running cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a><span data-ttu-id="15df8-264">Apply a script action to a running cluster from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="15df8-264">Apply a script action to a running cluster from the Azure portal</span></span>

1. <span data-ttu-id="15df8-265">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-265">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="15df8-266">From the HDInsight cluster overview, select the **Script Actions** tile.</span><span class="sxs-lookup"><span data-stu-id="15df8-266">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Script actions tile](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="15df8-268">You can also select **All settings** and then select **Script Actions** from the Settings section.</span><span class="sxs-lookup"><span data-stu-id="15df8-268">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

3. <span data-ttu-id="15df8-269">From the top of the script actions section, select **Submit new**.</span><span class="sxs-lookup"><span data-stu-id="15df8-269">From the top of the script actions section, select **Submit new**.</span></span>

    ![Add a script to a running cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="15df8-271">Use the __Select a script__ entry to select a pre-made script.</span><span class="sxs-lookup"><span data-stu-id="15df8-271">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="15df8-272">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span><span class="sxs-lookup"><span data-stu-id="15df8-272">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Add a script in the select script form](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="15df8-274">The following table describes the elements on the form:</span><span class="sxs-lookup"><span data-stu-id="15df8-274">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="15df8-275">Property</span><span class="sxs-lookup"><span data-stu-id="15df8-275">Property</span></span> | <span data-ttu-id="15df8-276">Value</span><span class="sxs-lookup"><span data-stu-id="15df8-276">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="15df8-277">Select a script</span><span class="sxs-lookup"><span data-stu-id="15df8-277">Select a script</span></span> | <span data-ttu-id="15df8-278">To use your own script, select __custom__.</span><span class="sxs-lookup"><span data-stu-id="15df8-278">To use your own script, select __custom__.</span></span> <span data-ttu-id="15df8-279">Otherwise, select a provided script.</span><span class="sxs-lookup"><span data-stu-id="15df8-279">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="15df8-280">Name</span><span class="sxs-lookup"><span data-stu-id="15df8-280">Name</span></span> |<span data-ttu-id="15df8-281">Specify a name for the script action.</span><span class="sxs-lookup"><span data-stu-id="15df8-281">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="15df8-282">Bash script URI</span><span class="sxs-lookup"><span data-stu-id="15df8-282">Bash script URI</span></span> |<span data-ttu-id="15df8-283">Specify the URI of the script.</span><span class="sxs-lookup"><span data-stu-id="15df8-283">Specify the URI of the script.</span></span> |
    | <span data-ttu-id="15df8-284">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="15df8-284">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="15df8-285">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the script is run.</span><span class="sxs-lookup"><span data-stu-id="15df8-285">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the script is run.</span></span> |
    | <span data-ttu-id="15df8-286">Parameters</span><span class="sxs-lookup"><span data-stu-id="15df8-286">Parameters</span></span> |<span data-ttu-id="15df8-287">Specify the parameters, if required by the script.</span><span class="sxs-lookup"><span data-stu-id="15df8-287">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="15df8-288">Use the __Persist this script action__ entry to make sure the script is applied during scaling operations.</span><span class="sxs-lookup"><span data-stu-id="15df8-288">Use the __Persist this script action__ entry to make sure the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="15df8-289">Finally, use the **Create** button to apply the script to the cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-289">Finally, use the **Create** button to apply the script to the cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a><span data-ttu-id="15df8-290">Apply a script action to a running cluster from Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="15df8-290">Apply a script action to a running cluster from Azure PowerShell</span></span>

<span data-ttu-id="15df8-291">Before proceeding, make sure you have installed and configured Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15df8-291">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="15df8-292">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="15df8-292">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="15df8-293">The following example demonstrates how to apply a script action to a running cluster:</span><span class="sxs-lookup"><span data-stu-id="15df8-293">The following example demonstrates how to apply a script action to a running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="15df8-294">Once the operation completes, you receive information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="15df8-294">Once the operation completes, you receive information similar to the following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a><span data-ttu-id="15df8-295">Apply a script action to a running cluster from the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15df8-295">Apply a script action to a running cluster from the Azure CLI</span></span>

<span data-ttu-id="15df8-296">Before proceeding, make sure you have installed and configured the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="15df8-296">Before proceeding, make sure you have installed and configured the Azure CLI.</span></span> <span data-ttu-id="15df8-297">For more information, see [Install the Azure CLI 1.0](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-297">For more information, see [Install the Azure CLI 1.0](../cli-install-nodejs.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15df8-298">HDInsight requires Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="15df8-298">HDInsight requires Azure CLI 1.0.</span></span> <span data-ttu-id="15df8-299">Currently Azure CLI 2.0 does not provide commands for working with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="15df8-299">Currently Azure CLI 2.0 does not provide commands for working with HDInsight.</span></span>

1. <span data-ttu-id="15df8-300">To switch to Azure Resource Manager mode, use the following command at the command line:</span><span class="sxs-lookup"><span data-stu-id="15df8-300">To switch to Azure Resource Manager mode, use the following command at the command line:</span></span>

    ```bash
    azure config mode arm
    ```

2. <span data-ttu-id="15df8-301">Use the following to authenticate to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="15df8-301">Use the following to authenticate to your Azure subscription.</span></span>

    ```bash
    azure login
    ```

3. <span data-ttu-id="15df8-302">Use the following command to apply a script action to a running cluster</span><span class="sxs-lookup"><span data-stu-id="15df8-302">Use the following command to apply a script action to a running cluster</span></span>

    ```bash
    azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>
    ```

    <span data-ttu-id="15df8-303">If you omit parameters for this command, you are prompted for them.</span><span class="sxs-lookup"><span data-stu-id="15df8-303">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="15df8-304">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span><span class="sxs-lookup"><span data-stu-id="15df8-304">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span></span>

    <span data-ttu-id="15df8-305">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="15df8-305">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="15df8-306">If the script should be applied to multiple node types, specify the types separated by a ';'.</span><span class="sxs-lookup"><span data-stu-id="15df8-306">If the script should be applied to multiple node types, specify the types separated by a ';'.</span></span> <span data-ttu-id="15df8-307">For example, `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="15df8-307">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="15df8-308">To persist the script, add the `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="15df8-308">To persist the script, add the `--persistOnSuccess`.</span></span> <span data-ttu-id="15df8-309">You can also persist the script later by using `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="15df8-309">You can also persist the script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="15df8-310">Once the job completes, you receive output similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="15df8-310">Once the job completes, you receive output similar to the following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a><span data-ttu-id="15df8-311">Apply a script action to a running cluster using REST API</span><span class="sxs-lookup"><span data-stu-id="15df8-311">Apply a script action to a running cluster using REST API</span></span>

<span data-ttu-id="15df8-312">See [Run script actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="15df8-312">See [Run script actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a><span data-ttu-id="15df8-313">Apply a script action to a running cluster from the HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="15df8-313">Apply a script action to a running cluster from the HDInsight .NET SDK</span></span>

<span data-ttu-id="15df8-314">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="15df8-314">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="15df8-315">View history, promote, and demote script actions</span><span class="sxs-lookup"><span data-stu-id="15df8-315">View history, promote, and demote script actions</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="15df8-316">Using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="15df8-316">Using the Azure portal</span></span>

1. <span data-ttu-id="15df8-317">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-317">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="15df8-318">From the HDInsight cluster overview, select the **Script Actions** tile.</span><span class="sxs-lookup"><span data-stu-id="15df8-318">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Script actions tile](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="15df8-320">You can also select **All settings** and then select **Script Actions** from the Settings section.</span><span class="sxs-lookup"><span data-stu-id="15df8-320">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

4. <span data-ttu-id="15df8-321">A history of scripts for this cluster is displayed on the script actions section.</span><span class="sxs-lookup"><span data-stu-id="15df8-321">A history of scripts for this cluster is displayed on the script actions section.</span></span> <span data-ttu-id="15df8-322">This information includes a list of persisted scripts.</span><span class="sxs-lookup"><span data-stu-id="15df8-322">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="15df8-323">In the screenshot below, you can see that the Solr script has been ran on this cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-323">In the screenshot below, you can see that the Solr script has been ran on this cluster.</span></span> <span data-ttu-id="15df8-324">The screenshot does not show any persisted scripts.</span><span class="sxs-lookup"><span data-stu-id="15df8-324">The screenshot does not show any persisted scripts.</span></span>

    ![Script actions section](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="15df8-326">Selecting a script from the history displays the Properties section for this script.</span><span class="sxs-lookup"><span data-stu-id="15df8-326">Selecting a script from the history displays the Properties section for this script.</span></span> <span data-ttu-id="15df8-327">From the top of the screen, you can rerun the script or promote it.</span><span class="sxs-lookup"><span data-stu-id="15df8-327">From the top of the screen, you can rerun the script or promote it.</span></span>

    ![Script actions properties](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="15df8-329">You can also use the **...** to the right of entries on the script actions section to perform actions.</span><span class="sxs-lookup"><span data-stu-id="15df8-329">You can also use the **...** to the right of entries on the script actions section to perform actions.</span></span>

    ![Script actions ... usage](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="15df8-331">Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="15df8-331">Using Azure PowerShell</span></span>

| <span data-ttu-id="15df8-332">Use the following...</span><span class="sxs-lookup"><span data-stu-id="15df8-332">Use the following...</span></span> | <span data-ttu-id="15df8-333">To ...</span><span class="sxs-lookup"><span data-stu-id="15df8-333">To ...</span></span> |
| --- | --- |
| <span data-ttu-id="15df8-334">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="15df8-334">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="15df8-335">Retrieve information on persisted script actions</span><span class="sxs-lookup"><span data-stu-id="15df8-335">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="15df8-336">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="15df8-336">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="15df8-337">Retrieve a history of script actions applied to the cluster, or details for a specific script</span><span class="sxs-lookup"><span data-stu-id="15df8-337">Retrieve a history of script actions applied to the cluster, or details for a specific script</span></span> |
| <span data-ttu-id="15df8-338">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="15df8-338">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="15df8-339">Promotes an ad hoc script action to a persisted script action</span><span class="sxs-lookup"><span data-stu-id="15df8-339">Promotes an ad hoc script action to a persisted script action</span></span> |
| <span data-ttu-id="15df8-340">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="15df8-340">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="15df8-341">Demotes a persisted script action to an ad hoc action</span><span class="sxs-lookup"><span data-stu-id="15df8-341">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="15df8-342">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script.</span><span class="sxs-lookup"><span data-stu-id="15df8-342">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script.</span></span> <span data-ttu-id="15df8-343">This cmdlet only removes the persisted flag.</span><span class="sxs-lookup"><span data-stu-id="15df8-343">This cmdlet only removes the persisted flag.</span></span>

<span data-ttu-id="15df8-344">The following example script demonstrates using the cmdlets to promote, then demote a script.</span><span class="sxs-lookup"><span data-stu-id="15df8-344">The following example script demonstrates using the cmdlets to promote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-the-azure-cli"></a><span data-ttu-id="15df8-345">Using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15df8-345">Using the Azure CLI</span></span>

| <span data-ttu-id="15df8-346">Use the following...</span><span class="sxs-lookup"><span data-stu-id="15df8-346">Use the following...</span></span> | <span data-ttu-id="15df8-347">To ...</span><span class="sxs-lookup"><span data-stu-id="15df8-347">To ...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="15df8-348">Retrieve a list of persisted script actions</span><span class="sxs-lookup"><span data-stu-id="15df8-348">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="15df8-349">Retrieve information on a specific persisted script action</span><span class="sxs-lookup"><span data-stu-id="15df8-349">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="15df8-350">Retrieve a history of script actions applied to the cluster</span><span class="sxs-lookup"><span data-stu-id="15df8-350">Retrieve a history of script actions applied to the cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="15df8-351">Retrieve information on a specific script action</span><span class="sxs-lookup"><span data-stu-id="15df8-351">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="15df8-352">Promotes an ad hoc script action to a persisted script action</span><span class="sxs-lookup"><span data-stu-id="15df8-352">Promotes an ad hoc script action to a persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="15df8-353">Demotes a persisted script action to an ad hoc action</span><span class="sxs-lookup"><span data-stu-id="15df8-353">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="15df8-354">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script.</span><span class="sxs-lookup"><span data-stu-id="15df8-354">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script.</span></span> <span data-ttu-id="15df8-355">This cmdlet only removes the persisted flag.</span><span class="sxs-lookup"><span data-stu-id="15df8-355">This cmdlet only removes the persisted flag.</span></span>

### <a name="using-the-hdinsight-net-sdk"></a><span data-ttu-id="15df8-356">Using the HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="15df8-356">Using the HDInsight .NET SDK</span></span>

<span data-ttu-id="15df8-357">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="15df8-357">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="15df8-358">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="15df8-358">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="15df8-359">Support for open-source software used on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="15df8-359">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="15df8-360">The Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span><span class="sxs-lookup"><span data-stu-id="15df8-360">The Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="15df8-361">Microsoft Azure provides a general level of support for open-source technologies.</span><span class="sxs-lookup"><span data-stu-id="15df8-361">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="15df8-362">For more information, see the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="15df8-362">For more information, see the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="15df8-363">The HDInsight service provides an additional level of support for built-in components.</span><span class="sxs-lookup"><span data-stu-id="15df8-363">The HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="15df8-364">There are two types of open-source components that are available in the HDInsight service:</span><span class="sxs-lookup"><span data-stu-id="15df8-364">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="15df8-365">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-365">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="15df8-366">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span><span class="sxs-lookup"><span data-stu-id="15df8-366">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="15df8-367">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-367">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="15df8-368">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span><span class="sxs-lookup"><span data-stu-id="15df8-368">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="15df8-369">Components provided with the HDInsight cluster are fully supported.</span><span class="sxs-lookup"><span data-stu-id="15df8-369">Components provided with the HDInsight cluster are fully supported.</span></span> <span data-ttu-id="15df8-370">Microsoft Support helps to isolate and resolve issues related to these components.</span><span class="sxs-lookup"><span data-stu-id="15df8-370">Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="15df8-371">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="15df8-371">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="15df8-372">Microsoft support may be able to resolve the issue OR they may ask you to engage available channels for the open source technologies where deep expertise for that technology is found.</span><span class="sxs-lookup"><span data-stu-id="15df8-372">Microsoft support may be able to resolve the issue OR they may ask you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="15df8-373">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="15df8-373">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="15df8-374">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="15df8-374">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="15df8-375">The HDInsight service provides several ways to use custom components.</span><span class="sxs-lookup"><span data-stu-id="15df8-375">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="15df8-376">The same level of support applies, regardless of how a component is used or installed on the cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-376">The same level of support applies, regardless of how a component is used or installed on the cluster.</span></span> <span data-ttu-id="15df8-377">The following list describes the most common ways that custom components can be used on HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="15df8-377">The following list describes the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="15df8-378">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-378">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>

2. <span data-ttu-id="15df8-379">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="15df8-379">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span></span>

3. <span data-ttu-id="15df8-380">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="15df8-380">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="15df8-381">These samples are provided without support.</span><span class="sxs-lookup"><span data-stu-id="15df8-381">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="15df8-382">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="15df8-382">Troubleshooting</span></span>

<span data-ttu-id="15df8-383">You can use Ambari web UI to view information logged by script actions.</span><span class="sxs-lookup"><span data-stu-id="15df8-383">You can use Ambari web UI to view information logged by script actions.</span></span> <span data-ttu-id="15df8-384">If the script fails during cluster creation, the logs are also available in the default storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-384">If the script fails during cluster creation, the logs are also available in the default storage account associated with the cluster.</span></span> <span data-ttu-id="15df8-385">This section provides information on how to retrieve the logs using both these options.</span><span class="sxs-lookup"><span data-stu-id="15df8-385">This section provides information on how to retrieve the logs using both these options.</span></span>

### <a name="using-the-ambari-web-ui"></a><span data-ttu-id="15df8-386">Using the Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="15df8-386">Using the Ambari Web UI</span></span>

1. <span data-ttu-id="15df8-387">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="15df8-387">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="15df8-388">Replace CLUSTERNAME with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-388">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="15df8-389">When prompted, enter the admin account name (admin) and password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-389">When prompted, enter the admin account name (admin) and password for the cluster.</span></span> <span data-ttu-id="15df8-390">You may have to reenter the admin credentials in a web form.</span><span class="sxs-lookup"><span data-stu-id="15df8-390">You may have to reenter the admin credentials in a web form.</span></span>

2. <span data-ttu-id="15df8-391">From the bar at the top of the page, select the **ops** entry.</span><span class="sxs-lookup"><span data-stu-id="15df8-391">From the bar at the top of the page, select the **ops** entry.</span></span> <span data-ttu-id="15df8-392">A list of current and previous operations performed on the cluster through Ambari is displayed.</span><span class="sxs-lookup"><span data-stu-id="15df8-392">A list of current and previous operations performed on the cluster through Ambari is displayed.</span></span>

    ![Ambari web UI bar with ops selected](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="15df8-394">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span><span class="sxs-lookup"><span data-stu-id="15df8-394">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span></span> <span data-ttu-id="15df8-395">These entries are created when the script actions run.</span><span class="sxs-lookup"><span data-stu-id="15df8-395">These entries are created when the script actions run.</span></span>

    ![Screenshot of operations](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="15df8-397">To view the STDOUT and STDERR output, select the run\customscriptaction entry and drill down through the links.</span><span class="sxs-lookup"><span data-stu-id="15df8-397">To view the STDOUT and STDERR output, select the run\customscriptaction entry and drill down through the links.</span></span> <span data-ttu-id="15df8-398">This output is generated when the script runs, and may contain useful information.</span><span class="sxs-lookup"><span data-stu-id="15df8-398">This output is generated when the script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-the-default-storage-account"></a><span data-ttu-id="15df8-399">Access logs from the default storage account</span><span class="sxs-lookup"><span data-stu-id="15df8-399">Access logs from the default storage account</span></span>

<span data-ttu-id="15df8-400">If cluster creation fails due to a script error, the logs are kept in the cluster storage account.</span><span class="sxs-lookup"><span data-stu-id="15df8-400">If cluster creation fails due to a script error, the logs are kept in the cluster storage account.</span></span>

* <span data-ttu-id="15df8-401">The storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="15df8-401">The storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Screenshot of operations](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="15df8-403">Under this directory, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span><span class="sxs-lookup"><span data-stu-id="15df8-403">Under this directory, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="15df8-404">Some examples are:</span><span class="sxs-lookup"><span data-stu-id="15df8-404">Some examples are:</span></span>

    * <span data-ttu-id="15df8-405">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="15df8-405">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="15df8-406">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="15df8-406">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="15df8-407">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="15df8-407">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="15df8-408">All stdout and stderr of the corresponding host is uploaded to the storage account.</span><span class="sxs-lookup"><span data-stu-id="15df8-408">All stdout and stderr of the corresponding host is uploaded to the storage account.</span></span> <span data-ttu-id="15df8-409">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span><span class="sxs-lookup"><span data-stu-id="15df8-409">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="15df8-410">The output-\*.txt file contains information about the URI of the script that got run on the host.</span><span class="sxs-lookup"><span data-stu-id="15df8-410">The output-\*.txt file contains information about the URI of the script that got run on the host.</span></span> <span data-ttu-id="15df8-411">The following text is an example of this information:</span><span class="sxs-lookup"><span data-stu-id="15df8-411">The following text is an example of this information:</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="15df8-412">It's possible that you repeatedly create a script action cluster with the same name.</span><span class="sxs-lookup"><span data-stu-id="15df8-412">It's possible that you repeatedly create a script action cluster with the same name.</span></span> <span data-ttu-id="15df8-413">In such case, you can distinguish the relevant logs based on the DATE folder name.</span><span class="sxs-lookup"><span data-stu-id="15df8-413">In such case, you can distinguish the relevant logs based on the DATE folder name.</span></span> <span data-ttu-id="15df8-414">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following log entries:</span><span class="sxs-lookup"><span data-stu-id="15df8-414">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following log entries:</span></span>

    <span data-ttu-id="15df8-415">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="15df8-415">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="15df8-416">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span><span class="sxs-lookup"><span data-stu-id="15df8-416">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span></span>

* <span data-ttu-id="15df8-417">If you create a cluster near 12:00AM (midnight), it's possible that the log files span across two days.</span><span class="sxs-lookup"><span data-stu-id="15df8-417">If you create a cluster near 12:00AM (midnight), it's possible that the log files span across two days.</span></span> <span data-ttu-id="15df8-418">In such cases, you see two different date folders for the same cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-418">In such cases, you see two different date folders for the same cluster.</span></span>

* <span data-ttu-id="15df8-419">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span><span class="sxs-lookup"><span data-stu-id="15df8-419">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span></span> <span data-ttu-id="15df8-420">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span><span class="sxs-lookup"><span data-stu-id="15df8-420">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="15df8-421">Ambari watchdog</span><span class="sxs-lookup"><span data-stu-id="15df8-421">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="15df8-422">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-422">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="15df8-423">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-423">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="15df8-424">Can't import name BlobService</span><span class="sxs-lookup"><span data-stu-id="15df8-424">Can't import name BlobService</span></span>

<span data-ttu-id="15df8-425">__Symptoms__: The script action fails.</span><span class="sxs-lookup"><span data-stu-id="15df8-425">__Symptoms__: The script action fails.</span></span> <span data-ttu-id="15df8-426">Text similar to the following error is displayed when you view the operation in Ambari:</span><span class="sxs-lookup"><span data-stu-id="15df8-426">Text similar to the following error is displayed when you view the operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="15df8-427">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15df8-427">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span></span> <span data-ttu-id="15df8-428">HDInsight expects Azure Storage client 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="15df8-428">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="15df8-429">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span><span class="sxs-lookup"><span data-stu-id="15df8-429">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span></span>

```bash
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="15df8-430">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="15df8-430">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="15df8-431">History doesn't show scripts used during cluster creation</span><span class="sxs-lookup"><span data-stu-id="15df8-431">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="15df8-432">If your cluster was created before March 15, 2016, you may not see an entry in script action history.</span><span class="sxs-lookup"><span data-stu-id="15df8-432">If your cluster was created before March 15, 2016, you may not see an entry in script action history.</span></span> <span data-ttu-id="15df8-433">Resizing the cluster causes the scripts to appear in script action history.</span><span class="sxs-lookup"><span data-stu-id="15df8-433">Resizing the cluster causes the scripts to appear in script action history.</span></span>

<span data-ttu-id="15df8-434">There are two exceptions:</span><span class="sxs-lookup"><span data-stu-id="15df8-434">There are two exceptions:</span></span>

* <span data-ttu-id="15df8-435">If your cluster was created before September 1, 2015.</span><span class="sxs-lookup"><span data-stu-id="15df8-435">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="15df8-436">This date is when script actions were introduced.</span><span class="sxs-lookup"><span data-stu-id="15df8-436">This date is when script actions were introduced.</span></span> <span data-ttu-id="15df8-437">Any cluster created before this date could not have used script actions for cluster creation.</span><span class="sxs-lookup"><span data-stu-id="15df8-437">Any cluster created before this date could not have used script actions for cluster creation.</span></span>

* <span data-ttu-id="15df8-438">If you used multiple script actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span><span class="sxs-lookup"><span data-stu-id="15df8-438">If you used multiple script actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="15df8-439">In these cases, you receive the following error:</span><span class="sxs-lookup"><span data-stu-id="15df8-439">In these cases, you receive the following error:</span></span>

    <span data-ttu-id="15df8-440">No new script actions can be ran on this cluster due to conflicting script names in existing scripts.</span><span class="sxs-lookup"><span data-stu-id="15df8-440">No new script actions can be ran on this cluster due to conflicting script names in existing scripts.</span></span> <span data-ttu-id="15df8-441">Script names provided at cluster create must be all unique.</span><span class="sxs-lookup"><span data-stu-id="15df8-441">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="15df8-442">Existing scripts are ran on resize.</span><span class="sxs-lookup"><span data-stu-id="15df8-442">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15df8-443">Next steps</span><span class="sxs-lookup"><span data-stu-id="15df8-443">Next steps</span></span>

* [<span data-ttu-id="15df8-444">Develop script action scripts for HDInsight</span><span class="sxs-lookup"><span data-stu-id="15df8-444">Develop script action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="15df8-445">Install and use Solr on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="15df8-445">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="15df8-446">Install and use Giraph on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="15df8-446">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="15df8-447">Add additional storage to an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="15df8-447">Add additional storage to an HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Stages during cluster creation"
