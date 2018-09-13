---
title: Publish HDInsight applications | Microsoft Docs
description: Learn how to create and publish HDInsight applications.
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: fd287c1ec9123b065bdadcfb4ff95dd93cbb02a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550014"
---
# <a name="publish-hdinsight-applications-into-the-azure-marketplace"></a><span data-ttu-id="6e664-103">Publish HDInsight applications into the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6e664-103">Publish HDInsight applications into the Azure Marketplace</span></span>
<span data-ttu-id="6e664-104">An HDInsight application is an application that users can install on a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6e664-104">An HDInsight application is an application that users can install on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6e664-105">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span><span class="sxs-lookup"><span data-stu-id="6e664-105">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span></span> <span data-ttu-id="6e664-106">In this article, you will learn how to publish an HDInsight application into the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6e664-106">In this article, you will learn how to publish an HDInsight application into the Azure Marketplace.</span></span>  <span data-ttu-id="6e664-107">For general information about publishing into the Azure Marketplace, see [publish an offer to the Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e664-107">For general information about publishing into the Azure Marketplace, see [publish an offer to the Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="6e664-108">HDInsight applications use the *Bring Your Own License (BYOL)* model, where application provider is responsible for licensing the application to end-users, and end-users are only charged by Azure for the resources they create, such as the HDInsight cluster and its VMs/nodes.</span><span class="sxs-lookup"><span data-stu-id="6e664-108">HDInsight applications use the *Bring Your Own License (BYOL)* model, where application provider is responsible for licensing the application to end-users, and end-users are only charged by Azure for the resources they create, such as the HDInsight cluster and its VMs/nodes.</span></span> <span data-ttu-id="6e664-109">At this time, billing for the application itself is not done through Azure.</span><span class="sxs-lookup"><span data-stu-id="6e664-109">At this time, billing for the application itself is not done through Azure.</span></span>

<span data-ttu-id="6e664-110">Other HDInsight application related article:</span><span class="sxs-lookup"><span data-stu-id="6e664-110">Other HDInsight application related article:</span></span>

* <span data-ttu-id="6e664-111">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span><span class="sxs-lookup"><span data-stu-id="6e664-111">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="6e664-112">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to install and test custom HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="6e664-112">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to install and test custom HDInsight applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e664-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6e664-113">Prerequisites</span></span>
<span data-ttu-id="6e664-114">In order to submit your custom application to the marketplace, you must have created and tested your custom application.</span><span class="sxs-lookup"><span data-stu-id="6e664-114">In order to submit your custom application to the marketplace, you must have created and tested your custom application.</span></span> <span data-ttu-id="6e664-115">See the following articles:</span><span class="sxs-lookup"><span data-stu-id="6e664-115">See the following articles:</span></span>

* <span data-ttu-id="6e664-116">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to install and test custom HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="6e664-116">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): Learn how to install and test custom HDInsight applications.</span></span>

<span data-ttu-id="6e664-117">You must also have register your developer account.</span><span class="sxs-lookup"><span data-stu-id="6e664-117">You must also have register your developer account.</span></span> <span data-ttu-id="6e664-118">See [publish an offer to the Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) and [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6e664-118">See [publish an offer to the Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) and [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span></span>

## <a name="define-application"></a><span data-ttu-id="6e664-119">Define application</span><span class="sxs-lookup"><span data-stu-id="6e664-119">Define application</span></span>
<span data-ttu-id="6e664-120">There are two steps involved for publishing applications to the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6e664-120">There are two steps involved for publishing applications to the Azure Marketplace.</span></span>  <span data-ttu-id="6e664-121">First you define a **createUiDef.json** file to indicate which clusters your application is compatible with; and then you publish the template from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6e664-121">First you define a **createUiDef.json** file to indicate which clusters your application is compatible with; and then you publish the template from the Azure portal.</span></span> <span data-ttu-id="6e664-122">The following is a sample createUiDef.json file.</span><span class="sxs-lookup"><span data-stu-id="6e664-122">The following is a sample createUiDef.json file.</span></span>

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| <span data-ttu-id="6e664-123">Field</span><span class="sxs-lookup"><span data-stu-id="6e664-123">Field</span></span> | <span data-ttu-id="6e664-124">Description</span><span class="sxs-lookup"><span data-stu-id="6e664-124">Description</span></span> | <span data-ttu-id="6e664-125">Possible values</span><span class="sxs-lookup"><span data-stu-id="6e664-125">Possible values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6e664-126">types</span><span class="sxs-lookup"><span data-stu-id="6e664-126">types</span></span> |<span data-ttu-id="6e664-127">The cluster types that the application is compatible with.</span><span class="sxs-lookup"><span data-stu-id="6e664-127">The cluster types that the application is compatible with.</span></span> |<span data-ttu-id="6e664-128">Hadoop, HBase, Storm, Spark, (or any combination of these)</span><span class="sxs-lookup"><span data-stu-id="6e664-128">Hadoop, HBase, Storm, Spark, (or any combination of these)</span></span> |
| <span data-ttu-id="6e664-129">tiers</span><span class="sxs-lookup"><span data-stu-id="6e664-129">tiers</span></span> |<span data-ttu-id="6e664-130">The cluster tiers that the application is compatible with.</span><span class="sxs-lookup"><span data-stu-id="6e664-130">The cluster tiers that the application is compatible with.</span></span> |<span data-ttu-id="6e664-131">Standard, Premium, (or both)</span><span class="sxs-lookup"><span data-stu-id="6e664-131">Standard, Premium, (or both)</span></span> |
| <span data-ttu-id="6e664-132">versions</span><span class="sxs-lookup"><span data-stu-id="6e664-132">versions</span></span> |<span data-ttu-id="6e664-133">The HDInsight cluster types that the application is compatible with.</span><span class="sxs-lookup"><span data-stu-id="6e664-133">The HDInsight cluster types that the application is compatible with.</span></span> |<span data-ttu-id="6e664-134">3.4</span><span class="sxs-lookup"><span data-stu-id="6e664-134">3.4</span></span> |

## <a name="package-application"></a><span data-ttu-id="6e664-135">Package application</span><span class="sxs-lookup"><span data-stu-id="6e664-135">Package application</span></span>
<span data-ttu-id="6e664-136">Create a zip file that contains all required files for installing your HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="6e664-136">Create a zip file that contains all required files for installing your HDInsight applications.</span></span> <span data-ttu-id="6e664-137">You will need the zip file in [Publish application](#publish-application).</span><span class="sxs-lookup"><span data-stu-id="6e664-137">You will need the zip file in [Publish application](#publish-application).</span></span>

* <span data-ttu-id="6e664-138">[createUiDefinition.json](#define-application).</span><span class="sxs-lookup"><span data-stu-id="6e664-138">[createUiDefinition.json](#define-application).</span></span>
* <span data-ttu-id="6e664-139">mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="6e664-139">mainTemplate.json.</span></span> <span data-ttu-id="6e664-140">See a sample at [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span><span class="sxs-lookup"><span data-stu-id="6e664-140">See a sample at [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="6e664-141">The name of the application install script names must be unique for a particular cluster with the format below.</span><span class="sxs-lookup"><span data-stu-id="6e664-141">The name of the application install script names must be unique for a particular cluster with the format below.</span></span> <span data-ttu-id="6e664-142">Additionally any install and uninstall script actions should be idempotent, meaning the scripts can be called repeatly while producing the same result.</span><span class="sxs-lookup"><span data-stu-id="6e664-142">Additionally any install and uninstall script actions should be idempotent, meaning the scripts can be called repeatly while producing the same result.</span></span>
  > 
  > <span data-ttu-id="6e664-143">name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"</span><span class="sxs-lookup"><span data-stu-id="6e664-143">name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"</span></span>
  > 
  > <span data-ttu-id="6e664-144">Note there are three parts to the script name:</span><span class="sxs-lookup"><span data-stu-id="6e664-144">Note there are three parts to the script name:</span></span>
  > 
  > 1. <span data-ttu-id="6e664-145">A script name prefix, which shall include either the application name or a name relevant to the application.</span><span class="sxs-lookup"><span data-stu-id="6e664-145">A script name prefix, which shall include either the application name or a name relevant to the application.</span></span>
  > 2. <span data-ttu-id="6e664-146">A "-" for readability.</span><span class="sxs-lookup"><span data-stu-id="6e664-146">A "-" for readability.</span></span>
  > 3. <span data-ttu-id="6e664-147">A unique string function with the application name as the parameter.</span><span class="sxs-lookup"><span data-stu-id="6e664-147">A unique string function with the application name as the parameter.</span></span>
  > 
  > <span data-ttu-id="6e664-148">An example is the above ends up becoming: hue-install-v0-4wkahss55hlas in the persisted script action list.</span><span class="sxs-lookup"><span data-stu-id="6e664-148">An example is the above ends up becoming: hue-install-v0-4wkahss55hlas in the persisted script action list.</span></span> <span data-ttu-id="6e664-149">For a sample JSON payload, see [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="6e664-149">For a sample JSON payload, see [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).</span></span>
  > 
  > 
* <span data-ttu-id="6e664-150">All required scripts.</span><span class="sxs-lookup"><span data-stu-id="6e664-150">All required scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="6e664-151">The application files (including web application files if there is any) can be located on any publicly accessible endpoint.</span><span class="sxs-lookup"><span data-stu-id="6e664-151">The application files (including web application files if there is any) can be located on any publicly accessible endpoint.</span></span>
> 
> 

## <a name="publish-application"></a><span data-ttu-id="6e664-152">Publish application</span><span class="sxs-lookup"><span data-stu-id="6e664-152">Publish application</span></span>
<span data-ttu-id="6e664-153">Follow the following steps to publish an HDInsight application:</span><span class="sxs-lookup"><span data-stu-id="6e664-153">Follow the following steps to publish an HDInsight application:</span></span>

1. <span data-ttu-id="6e664-154">Sign on to the [Azure Publishing portal](https://publish.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="6e664-154">Sign on to the [Azure Publishing portal](https://publish.windowsazure.com/).</span></span>
2. <span data-ttu-id="6e664-155">Click **Solution templates** from the left to create a new solution template.</span><span class="sxs-lookup"><span data-stu-id="6e664-155">Click **Solution templates** from the left to create a new solution template.</span></span>
3. <span data-ttu-id="6e664-156">Enter a title, and then click **Create a new solution template**.</span><span class="sxs-lookup"><span data-stu-id="6e664-156">Enter a title, and then click **Create a new solution template**.</span></span>
4. <span data-ttu-id="6e664-157">Click **Create Dev Center account and join the Azure program** to register your company if you haven't done so.</span><span class="sxs-lookup"><span data-stu-id="6e664-157">Click **Create Dev Center account and join the Azure program** to register your company if you haven't done so.</span></span>  <span data-ttu-id="6e664-158">See [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6e664-158">See [Create a Microsoft Developer account](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).</span></span>
5. <span data-ttu-id="6e664-159">Click **Define some Topologies to get Started**.</span><span class="sxs-lookup"><span data-stu-id="6e664-159">Click **Define some Topologies to get Started**.</span></span> <span data-ttu-id="6e664-160">A solution template is a "parent" to all of its topologies.</span><span class="sxs-lookup"><span data-stu-id="6e664-160">A solution template is a "parent" to all of its topologies.</span></span> <span data-ttu-id="6e664-161">You can define multiple topologies in one offer/solution template.</span><span class="sxs-lookup"><span data-stu-id="6e664-161">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="6e664-162">When an offer is pushed to staging, it is pushed with all of its topologies.</span><span class="sxs-lookup"><span data-stu-id="6e664-162">When an offer is pushed to staging, it is pushed with all of its topologies.</span></span> 
6. <span data-ttu-id="6e664-163">Enter a topology name, and then click the plus sign.</span><span class="sxs-lookup"><span data-stu-id="6e664-163">Enter a topology name, and then click the plus sign.</span></span>
7. <span data-ttu-id="6e664-164">Enter a new version, and then click the Plus sign.</span><span class="sxs-lookup"><span data-stu-id="6e664-164">Enter a new version, and then click the Plus sign.</span></span>
8. <span data-ttu-id="6e664-165">Upload the zip file prepared in [Package application](#package-application).</span><span class="sxs-lookup"><span data-stu-id="6e664-165">Upload the zip file prepared in [Package application](#package-application).</span></span>  
9. <span data-ttu-id="6e664-166">Click **Request Certification**.</span><span class="sxs-lookup"><span data-stu-id="6e664-166">Click **Request Certification**.</span></span> <span data-ttu-id="6e664-167">The Microsoft certification team will review the files and certify the topology.</span><span class="sxs-lookup"><span data-stu-id="6e664-167">The Microsoft certification team will review the files and certify the topology.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e664-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="6e664-168">Next steps</span></span>
* <span data-ttu-id="6e664-169">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span><span class="sxs-lookup"><span data-stu-id="6e664-169">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="6e664-170">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an un-published HDInsight application to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e664-170">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an un-published HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="6e664-171">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span><span class="sxs-lookup"><span data-stu-id="6e664-171">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="6e664-172">[Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="6e664-172">[Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>
* <span data-ttu-id="6e664-173">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): learn how to use an empty edge node for accessing HDInsight cluster, testing HDInsight applications, and hosting HDInsight applications.</span><span class="sxs-lookup"><span data-stu-id="6e664-173">[Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md): learn how to use an empty edge node for accessing HDInsight cluster, testing HDInsight applications, and hosting HDInsight applications.</span></span>

