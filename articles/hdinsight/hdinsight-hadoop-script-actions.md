---
title: Script Action development with HDInsight | Microsoft Docs
description: Learn how to customize Hadoop clusters with Script Action. Script Action can be used to install additional software running on a Hadoop cluster or to change the configuration of applications installed on a cluster.
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 989f45eed033409b1ade183827719acdd9a4b0b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669770"
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a><span data-ttu-id="9c0f5-104">Develop Script Action scripts for HDInsight Windows-based clusters</span><span class="sxs-lookup"><span data-stu-id="9c0f5-104">Develop Script Action scripts for HDInsight Windows-based clusters</span></span>
<span data-ttu-id="9c0f5-105">Learn how to write Script Action scripts for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-105">Learn how to write Script Action scripts for HDInsight.</span></span> <span data-ttu-id="9c0f5-106">For information on using Script Action scripts, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-106">For information on using Script Action scripts, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="9c0f5-107">For the same article written for Linux-based HDInsight clusters, see [Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-107">For the same article written for Linux-based HDInsight clusters, see [Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>



> [!IMPORTANT]
> <span data-ttu-id="9c0f5-108">The steps in this document only work for Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="9c0f5-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="9c0f5-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9c0f5-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span> <span data-ttu-id="9c0f5-112">For information on using script actions with Linux-based clusters, see [Script action development with HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-112">For information on using script actions with Linux-based clusters, see [Script action development with HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).</span></span>
>
>



<span data-ttu-id="9c0f5-113">Script Action can be used to install additional software running on a Hadoop cluster or to change the configuration of applications installed on a cluster.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-113">Script Action can be used to install additional software running on a Hadoop cluster or to change the configuration of applications installed on a cluster.</span></span> <span data-ttu-id="9c0f5-114">Script actions are scripts that run on the cluster nodes when HDInsight clusters are deployed, and they are executed once nodes in the cluster complete HDInsight configuration.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-114">Script actions are scripts that run on the cluster nodes when HDInsight clusters are deployed, and they are executed once nodes in the cluster complete HDInsight configuration.</span></span> <span data-ttu-id="9c0f5-115">A script action is executed under system admin account privileges and provides full access rights to the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-115">A script action is executed under system admin account privileges and provides full access rights to the cluster nodes.</span></span> <span data-ttu-id="9c0f5-116">Each cluster can be provided with a list of script actions to be executed in the order in which they are specified.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-116">Each cluster can be provided with a list of script actions to be executed in the order in which they are specified.</span></span>

> [!NOTE]
> <span data-ttu-id="9c0f5-117">If you experience the following error message:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-117">If you experience the following error message:</span></span>
>
> <span data-ttu-id="9c0f5-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage : The term 'Save-HDIFile' is not recognized as the name of a cmdlet, function, script file, or operable program.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage : The term 'Save-HDIFile' is not recognized as the name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="9c0f5-119">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-119">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span></span>
> <span data-ttu-id="9c0f5-120">It is because you didn't include the helper methods.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-120">It is because you didn't include the helper methods.</span></span>  <span data-ttu-id="9c0f5-121">See [Helper methods for custom scripts](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-121">See [Helper methods for custom scripts](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span></span>
>
>

## <a name="sample-scripts"></a><span data-ttu-id="9c0f5-122">Sample scripts</span><span class="sxs-lookup"><span data-stu-id="9c0f5-122">Sample scripts</span></span>
<span data-ttu-id="9c0f5-123">For creating HDInsight clusters on Windows operating system, the Script Action is Azure PowerShell script.The following is a sample script for configure the site configuration files:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-123">For creating HDInsight clusters on Windows operating system, the Script Action is Azure PowerShell script.The following is a sample script for configure the site configuration files:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable to configure $ConfigFileName because it is not part of the HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

<span data-ttu-id="9c0f5-124">The script takes four parameters, the configuration file name, the property you want to modify, the value you want to set, and a description.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-124">The script takes four parameters, the configuration file name, the property you want to modify, the value you want to set, and a description.</span></span> <span data-ttu-id="9c0f5-125">For example:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-125">For example:</span></span>

    hive-site.xml hive.metastore.client.socket.timeout 90

<span data-ttu-id="9c0f5-126">These parameters will set the hive.metastore.client.socket.timeout value to 90 in the hive-site.xml file.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-126">These parameters will set the hive.metastore.client.socket.timeout value to 90 in the hive-site.xml file.</span></span>  <span data-ttu-id="9c0f5-127">The default value is 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-127">The default value is 60 seconds.</span></span>

<span data-ttu-id="9c0f5-128">This sample script can also be found at [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-128">This sample script can also be found at [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span></span>

<span data-ttu-id="9c0f5-129">HDInsight provides several scripts to install additional components on HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-129">HDInsight provides several scripts to install additional components on HDInsight clusters:</span></span>

| <span data-ttu-id="9c0f5-130">Name</span><span class="sxs-lookup"><span data-stu-id="9c0f5-130">Name</span></span> | <span data-ttu-id="9c0f5-131">Script</span><span class="sxs-lookup"><span data-stu-id="9c0f5-131">Script</span></span> |
| --- | --- |
| <span data-ttu-id="9c0f5-132">**Install Spark**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-132">**Install Spark**</span></span> |<span data-ttu-id="9c0f5-133">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-133">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="9c0f5-134">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="9c0f5-134">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="9c0f5-135">**Install R**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-135">**Install R**</span></span> |<span data-ttu-id="9c0f5-136">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-136">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="9c0f5-137">See [Install and use R on HDInsight clusters][hdinsight-r-scripts].</span><span class="sxs-lookup"><span data-stu-id="9c0f5-137">See [Install and use R on HDInsight clusters][hdinsight-r-scripts].</span></span> |
| <span data-ttu-id="9c0f5-138">**Install Solr**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-138">**Install Solr**</span></span> |<span data-ttu-id="9c0f5-139">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-139">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="9c0f5-140">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-140">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="9c0f5-141">- **Install Giraph**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-141">- **Install Giraph**</span></span> |<span data-ttu-id="9c0f5-142">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-142">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="9c0f5-143">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-143">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |

<span data-ttu-id="9c0f5-144">Script Action can be deployed from the Azure portal, Azure PowerShell or by using the HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-144">Script Action can be deployed from the Azure portal, Azure PowerShell or by using the HDInsight .NET SDK.</span></span>  <span data-ttu-id="9c0f5-145">For more information, see [Customize HDInsight clusters using Script Action][hdinsight-cluster-customize].</span><span class="sxs-lookup"><span data-stu-id="9c0f5-145">For more information, see [Customize HDInsight clusters using Script Action][hdinsight-cluster-customize].</span></span>

> [!NOTE]
> <span data-ttu-id="9c0f5-146">The sample scripts work only with HDInsight cluster version 3.1 or above.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-146">The sample scripts work only with HDInsight cluster version 3.1 or above.</span></span> <span data-ttu-id="9c0f5-147">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-147">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="helper-methods-for-custom-scripts"></a><span data-ttu-id="9c0f5-148">Helper methods for custom scripts</span><span class="sxs-lookup"><span data-stu-id="9c0f5-148">Helper methods for custom scripts</span></span>
<span data-ttu-id="9c0f5-149">Script Action helper methods are utilities that you can use while writing custom scripts.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-149">Script Action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="9c0f5-150">These are defined in [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), and can be included in your scripts using the following:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-150">These are defined in [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), and can be included in your scripts using the following:</span></span>

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module to make writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed to load HDInsightUtilities module, exiting ...";
        exit;
    }

<span data-ttu-id="9c0f5-151">Here are the helper methods that are provided by this script:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-151">Here are the helper methods that are provided by this script:</span></span>

| <span data-ttu-id="9c0f5-152">Helper method</span><span class="sxs-lookup"><span data-stu-id="9c0f5-152">Helper method</span></span> | <span data-ttu-id="9c0f5-153">Description</span><span class="sxs-lookup"><span data-stu-id="9c0f5-153">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9c0f5-154">**Save-HDIFile**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-154">**Save-HDIFile**</span></span> |<span data-ttu-id="9c0f5-155">Download a file from the specified Uniform Resource Identifier (URI) to a location on the local disk that is associated with the Azure VM node assigned to the cluster.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-155">Download a file from the specified Uniform Resource Identifier (URI) to a location on the local disk that is associated with the Azure VM node assigned to the cluster.</span></span> |
| <span data-ttu-id="9c0f5-156">**Expand-HDIZippedFile**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-156">**Expand-HDIZippedFile**</span></span> |<span data-ttu-id="9c0f5-157">Unzip a zipped file.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-157">Unzip a zipped file.</span></span> |
| <span data-ttu-id="9c0f5-158">**Invoke-HDICmdScript**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-158">**Invoke-HDICmdScript**</span></span> |<span data-ttu-id="9c0f5-159">Run a script from cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-159">Run a script from cmd.exe.</span></span> |
| <span data-ttu-id="9c0f5-160">**Write-HDILog**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-160">**Write-HDILog**</span></span> |<span data-ttu-id="9c0f5-161">Write output from the custom script used for a script action.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-161">Write output from the custom script used for a script action.</span></span> |
| <span data-ttu-id="9c0f5-162">**Get-Services**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-162">**Get-Services**</span></span> |<span data-ttu-id="9c0f5-163">Get a list of services running on the machine where the script executes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-163">Get a list of services running on the machine where the script executes.</span></span> |
| <span data-ttu-id="9c0f5-164">**Get-Service**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-164">**Get-Service**</span></span> |<span data-ttu-id="9c0f5-165">With the specific service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on the machine where the script executes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-165">With the specific service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on the machine where the script executes.</span></span> |
| <span data-ttu-id="9c0f5-166">**Get-HDIServices**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-166">**Get-HDIServices**</span></span> |<span data-ttu-id="9c0f5-167">Get a list of HDInsight services running on the computer where the script executes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-167">Get a list of HDInsight services running on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c0f5-168">**Get-HDIService**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-168">**Get-HDIService**</span></span> |<span data-ttu-id="9c0f5-169">With the specific HDInsight service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on the machine where the script executes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-169">With the specific HDInsight service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on the machine where the script executes.</span></span> |
| <span data-ttu-id="9c0f5-170">**Get-ServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-170">**Get-ServicesRunning**</span></span> |<span data-ttu-id="9c0f5-171">Get a list of services that are running on the computer where the script executes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-171">Get a list of services that are running on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c0f5-172">**Get-ServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-172">**Get-ServiceRunning**</span></span> |<span data-ttu-id="9c0f5-173">Check if a specific service (by name) is running on the computer where the script executes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-173">Check if a specific service (by name) is running on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c0f5-174">**Get-HDIServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-174">**Get-HDIServicesRunning**</span></span> |<span data-ttu-id="9c0f5-175">Get a list of HDInsight services running on the computer where the script executes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-175">Get a list of HDInsight services running on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c0f5-176">**Get-HDIServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-176">**Get-HDIServiceRunning**</span></span> |<span data-ttu-id="9c0f5-177">Check if a specific HDInsight service (by name) is running on the computer where the script executes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-177">Check if a specific HDInsight service (by name) is running on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c0f5-178">**Get-HDIHadoopVersion**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-178">**Get-HDIHadoopVersion**</span></span> |<span data-ttu-id="9c0f5-179">Get the version of Hadoop installed on the computer where the script executes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-179">Get the version of Hadoop installed on the computer where the script executes.</span></span> |
| <span data-ttu-id="9c0f5-180">**Test-IsHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-180">**Test-IsHDIHeadNode**</span></span> |<span data-ttu-id="9c0f5-181">Check if the computer where the script executes is a head node.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-181">Check if the computer where the script executes is a head node.</span></span> |
| <span data-ttu-id="9c0f5-182">**Test-IsActiveHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-182">**Test-IsActiveHDIHeadNode**</span></span> |<span data-ttu-id="9c0f5-183">Check if the computer where the script executes is an active head node.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-183">Check if the computer where the script executes is an active head node.</span></span> |
| <span data-ttu-id="9c0f5-184">**Test-IsHDIDataNode**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-184">**Test-IsHDIDataNode**</span></span> |<span data-ttu-id="9c0f5-185">Check if the computer where the script executes is a data node.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-185">Check if the computer where the script executes is a data node.</span></span> |
| <span data-ttu-id="9c0f5-186">**Edit-HDIConfigFile**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-186">**Edit-HDIConfigFile**</span></span> |<span data-ttu-id="9c0f5-187">Edit the config files hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml, or yarn-site.xml.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-187">Edit the config files hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml, or yarn-site.xml.</span></span> |

## <a name="best-practices-for-script-development"></a><span data-ttu-id="9c0f5-188">Best practices for script development</span><span class="sxs-lookup"><span data-stu-id="9c0f5-188">Best practices for script development</span></span>
<span data-ttu-id="9c0f5-189">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-189">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* <span data-ttu-id="9c0f5-190">Check for the Hadoop version</span><span class="sxs-lookup"><span data-stu-id="9c0f5-190">Check for the Hadoop version</span></span>

    <span data-ttu-id="9c0f5-191">Only HDInsight version 3.1 (Hadoop 2.4) and above support using Script Action to install custom components on a cluster.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-191">Only HDInsight version 3.1 (Hadoop 2.4) and above support using Script Action to install custom components on a cluster.</span></span> <span data-ttu-id="9c0f5-192">In your custom script, you must use the **Get-HDIHadoopVersion** helper method to check the Hadoop version before proceeding with performing other tasks in the script.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-192">In your custom script, you must use the **Get-HDIHadoopVersion** helper method to check the Hadoop version before proceeding with performing other tasks in the script.</span></span>
* <span data-ttu-id="9c0f5-193">Provide stable links to script resources</span><span class="sxs-lookup"><span data-stu-id="9c0f5-193">Provide stable links to script resources</span></span>

    <span data-ttu-id="9c0f5-194">Users should make sure that all of the scripts and other artifacts used in the customization of a cluster remain available throughout the lifetime of the cluster and that the versions of these files do not change for the duration.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-194">Users should make sure that all of the scripts and other artifacts used in the customization of a cluster remain available throughout the lifetime of the cluster and that the versions of these files do not change for the duration.</span></span> <span data-ttu-id="9c0f5-195">These resources are required if the re-imaging of nodes in the cluster is required.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-195">These resources are required if the re-imaging of nodes in the cluster is required.</span></span> <span data-ttu-id="9c0f5-196">The best practice is to download and archive everything in a Storage account that the user controls.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-196">The best practice is to download and archive everything in a Storage account that the user controls.</span></span> <span data-ttu-id="9c0f5-197">This can be the default Storage account or any of the additional Storage accounts specified at the time of deployment for a customized cluster.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-197">This can be the default Storage account or any of the additional Storage accounts specified at the time of deployment for a customized cluster.</span></span>
    <span data-ttu-id="9c0f5-198">In the Spark and R customized cluster samples provided in the documentation, for example, we have made a local copy of the resources in this Storage account: https://hdiconfigactions.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-198">In the Spark and R customized cluster samples provided in the documentation, for example, we have made a local copy of the resources in this Storage account: https://hdiconfigactions.blob.core.windows.net/.</span></span>
* <span data-ttu-id="9c0f5-199">Ensure that the cluster customization script is idempotent</span><span class="sxs-lookup"><span data-stu-id="9c0f5-199">Ensure that the cluster customization script is idempotent</span></span>

    <span data-ttu-id="9c0f5-200">You must expect that the nodes of an HDInsight cluster will be re-imaged during the cluster lifetime.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-200">You must expect that the nodes of an HDInsight cluster will be re-imaged during the cluster lifetime.</span></span> <span data-ttu-id="9c0f5-201">The cluster customization script is run whenever a cluster is re-imaged.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-201">The cluster customization script is run whenever a cluster is re-imaged.</span></span> <span data-ttu-id="9c0f5-202">This script must be designed to be idempotent in the sense that upon re-imaging, the script should ensure that the cluster is returned to the same customized state that it was in just after the script ran for the first time when the cluster was initially created.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-202">This script must be designed to be idempotent in the sense that upon re-imaging, the script should ensure that the cluster is returned to the same customized state that it was in just after the script ran for the first time when the cluster was initially created.</span></span> <span data-ttu-id="9c0f5-203">For example, if a custom script installed an application at D:\AppLocation on its first run, then on each subsequent run, upon re-imaging, the script should check whether the application exists at the D:\AppLocation location before proceeding with other steps in the script.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-203">For example, if a custom script installed an application at D:\AppLocation on its first run, then on each subsequent run, upon re-imaging, the script should check whether the application exists at the D:\AppLocation location before proceeding with other steps in the script.</span></span>
* <span data-ttu-id="9c0f5-204">Install custom components in the optimal location</span><span class="sxs-lookup"><span data-stu-id="9c0f5-204">Install custom components in the optimal location</span></span>

    <span data-ttu-id="9c0f5-205">When cluster nodes are re-imaged, the C:\ resource drive and D:\ system drive can be re-formatted, resulting in the loss of data and applications that had been installed on those drives.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-205">When cluster nodes are re-imaged, the C:\ resource drive and D:\ system drive can be re-formatted, resulting in the loss of data and applications that had been installed on those drives.</span></span> <span data-ttu-id="9c0f5-206">This could also happen if an Azure virtual machine (VM) node that is part of the cluster goes down and is replaced by a new node.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-206">This could also happen if an Azure virtual machine (VM) node that is part of the cluster goes down and is replaced by a new node.</span></span> <span data-ttu-id="9c0f5-207">You can install components on the D:\ drive or in the C:\apps location on the cluster.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-207">You can install components on the D:\ drive or in the C:\apps location on the cluster.</span></span> <span data-ttu-id="9c0f5-208">All other locations on the C:\ drive are reserved.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-208">All other locations on the C:\ drive are reserved.</span></span> <span data-ttu-id="9c0f5-209">Specify the location where applications or libraries are to be installed in the cluster customization script.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-209">Specify the location where applications or libraries are to be installed in the cluster customization script.</span></span>
* <span data-ttu-id="9c0f5-210">Ensure high availability of the cluster architecture</span><span class="sxs-lookup"><span data-stu-id="9c0f5-210">Ensure high availability of the cluster architecture</span></span>

    <span data-ttu-id="9c0f5-211">HDInsight has an active-passive architecture for high availability, in which one head node is in active mode (where the HDInsight services are running) and the other head node is in standby mode (in which HDInsight services are not running).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-211">HDInsight has an active-passive architecture for high availability, in which one head node is in active mode (where the HDInsight services are running) and the other head node is in standby mode (in which HDInsight services are not running).</span></span> <span data-ttu-id="9c0f5-212">The nodes switch active and passive modes if HDInsight services are interrupted.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-212">The nodes switch active and passive modes if HDInsight services are interrupted.</span></span> <span data-ttu-id="9c0f5-213">If a script action is used to install services on both head nodes for high availability, note that the HDInsight failover mechanism will not be able to automatically fail over these user-installed services.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-213">If a script action is used to install services on both head nodes for high availability, note that the HDInsight failover mechanism will not be able to automatically fail over these user-installed services.</span></span> <span data-ttu-id="9c0f5-214">So user-installed services on HDInsight head nodes that are expected to be highly available must either have their own failover mechanism if in active-passive mode or be in active-active mode.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-214">So user-installed services on HDInsight head nodes that are expected to be highly available must either have their own failover mechanism if in active-passive mode or be in active-active mode.</span></span>

    <span data-ttu-id="9c0f5-215">An HDInsight Script Action command runs on both head nodes when the head-node role is specified as a value in the *ClusterRoleCollection* parameter.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-215">An HDInsight Script Action command runs on both head nodes when the head-node role is specified as a value in the *ClusterRoleCollection* parameter.</span></span> <span data-ttu-id="9c0f5-216">So when you design a custom script, make sure that your script is aware of this setup.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-216">So when you design a custom script, make sure that your script is aware of this setup.</span></span> <span data-ttu-id="9c0f5-217">You should not run into problems where the same services are installed and started on both of the head nodes and they end up competing with each other.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-217">You should not run into problems where the same services are installed and started on both of the head nodes and they end up competing with each other.</span></span> <span data-ttu-id="9c0f5-218">Also, be aware that data will be lost during re-imaging, so software installed via Script Action has to be resilient to such events.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-218">Also, be aware that data will be lost during re-imaging, so software installed via Script Action has to be resilient to such events.</span></span> <span data-ttu-id="9c0f5-219">Applications should be designed to work with highly available data that is distributed across many nodes.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-219">Applications should be designed to work with highly available data that is distributed across many nodes.</span></span> <span data-ttu-id="9c0f5-220">Note that as many as 1/5 of the nodes in a cluster can be re-imaged at the same time.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-220">Note that as many as 1/5 of the nodes in a cluster can be re-imaged at the same time.</span></span>
* <span data-ttu-id="9c0f5-221">Configure the custom components to use Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="9c0f5-221">Configure the custom components to use Azure Blob storage</span></span>

    <span data-ttu-id="9c0f5-222">The custom components that you install on the cluster nodes might have a default configuration to use Hadoop Distributed File System (HDFS) storage.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-222">The custom components that you install on the cluster nodes might have a default configuration to use Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="9c0f5-223">You should change the configuration to use Azure Blob storage instead.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-223">You should change the configuration to use Azure Blob storage instead.</span></span> <span data-ttu-id="9c0f5-224">On a cluster re-image, the HDFS file system gets formatted and you would lose any data that is stored there.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-224">On a cluster re-image, the HDFS file system gets formatted and you would lose any data that is stored there.</span></span> <span data-ttu-id="9c0f5-225">Using Azure Blob storage instead ensures that your data will be retained.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-225">Using Azure Blob storage instead ensures that your data will be retained.</span></span>

## <a name="common-usage-patterns"></a><span data-ttu-id="9c0f5-226">Common usage patterns</span><span class="sxs-lookup"><span data-stu-id="9c0f5-226">Common usage patterns</span></span>
<span data-ttu-id="9c0f5-227">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-227">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="configure-environment-variables"></a><span data-ttu-id="9c0f5-228">Configure environment variables</span><span class="sxs-lookup"><span data-stu-id="9c0f5-228">Configure environment variables</span></span>
<span data-ttu-id="9c0f5-229">Often in script action development, you will feel the need to set environment variables.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-229">Often in script action development, you will feel the need to set environment variables.</span></span> <span data-ttu-id="9c0f5-230">For instance, a most likely scenario is when you download a binary from an external site, install it on the cluster, and add the location of where it is installed to your ‘PATH’ environment variable.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-230">For instance, a most likely scenario is when you download a binary from an external site, install it on the cluster, and add the location of where it is installed to your ‘PATH’ environment variable.</span></span> <span data-ttu-id="9c0f5-231">The following snippet shows you how to set environment variables in the custom script.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-231">The following snippet shows you how to set environment variables in the custom script.</span></span>

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

<span data-ttu-id="9c0f5-232">This statement sets the environment variable **MDS_RUNNER_CUSTOM_CLUSTER** to the value 'true' and also sets the scope of this variable to be machine-wide.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-232">This statement sets the environment variable **MDS_RUNNER_CUSTOM_CLUSTER** to the value 'true' and also sets the scope of this variable to be machine-wide.</span></span> <span data-ttu-id="9c0f5-233">At times it is important that environment variables are set at the appropriate scope – machine or user.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-233">At times it is important that environment variables are set at the appropriate scope – machine or user.</span></span> <span data-ttu-id="9c0f5-234">Refer [here][1] for more information on setting environment variables.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-234">Refer [here][1] for more information on setting environment variables.</span></span>

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="9c0f5-235">Access to locations where the custom scripts are stored</span><span class="sxs-lookup"><span data-stu-id="9c0f5-235">Access to locations where the custom scripts are stored</span></span>
<span data-ttu-id="9c0f5-236">Scripts used to customize a cluster needs to either be in the default storage account for the cluster or in a public read-only container on any other storage account.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-236">Scripts used to customize a cluster needs to either be in the default storage account for the cluster or in a public read-only container on any other storage account.</span></span> <span data-ttu-id="9c0f5-237">If your script accesses resources located elsewhere these need to be in a publicly accessible (at least public read-only).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-237">If your script accesses resources located elsewhere these need to be in a publicly accessible (at least public read-only).</span></span> <span data-ttu-id="9c0f5-238">For instance you might want to access a file and save it using the SaveFile-HDI command.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-238">For instance you might want to access a file and save it using the SaveFile-HDI command.</span></span>

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

<span data-ttu-id="9c0f5-239">In this example, you must ensure that the container 'somecontainer' in storage account 'somestorageaccount' is publicly accessible.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-239">In this example, you must ensure that the container 'somecontainer' in storage account 'somestorageaccount' is publicly accessible.</span></span> <span data-ttu-id="9c0f5-240">Otherwise, the script will throw a ‘Not Found’ exception and fail.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-240">Otherwise, the script will throw a ‘Not Found’ exception and fail.</span></span>

### <a name="pass-parameters-to-the-add-azurermhdinsightscriptaction-cmdlet"></a><span data-ttu-id="9c0f5-241">Pass parameters to the Add-AzureRmHDInsightScriptAction cmdlet</span><span class="sxs-lookup"><span data-stu-id="9c0f5-241">Pass parameters to the Add-AzureRmHDInsightScriptAction cmdlet</span></span>
<span data-ttu-id="9c0f5-242">To pass multiple parameters to the Add-AzureRmHDInsightScriptAction cmdlet, you need to format the string value to contain all parameters for the script.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-242">To pass multiple parameters to the Add-AzureRmHDInsightScriptAction cmdlet, you need to format the string value to contain all parameters for the script.</span></span> <span data-ttu-id="9c0f5-243">For example:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-243">For example:</span></span>

    "-CertifcateUri wasbs:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

<span data-ttu-id="9c0f5-244">or</span><span class="sxs-lookup"><span data-stu-id="9c0f5-244">or</span></span>

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a><span data-ttu-id="9c0f5-245">Throw exception for failed cluster deployment</span><span class="sxs-lookup"><span data-stu-id="9c0f5-245">Throw exception for failed cluster deployment</span></span>
<span data-ttu-id="9c0f5-246">If you want to get accurately notified of the fact that cluster customization did not succeed as expected, it is important to throw an exception and fail the cluster creation.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-246">If you want to get accurately notified of the fact that cluster customization did not succeed as expected, it is important to throw an exception and fail the cluster creation.</span></span> <span data-ttu-id="9c0f5-247">For instance, you might want to process a file if it exists and handle the error case where the file does not exist.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-247">For instance, you might want to process a file if it exists and handle the error case where the file does not exist.</span></span> <span data-ttu-id="9c0f5-248">This would ensure that the script exits gracefully and the state of the cluster is correctly known.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-248">This would ensure that the script exits gracefully and the state of the cluster is correctly known.</span></span> <span data-ttu-id="9c0f5-249">The following snippet gives an example of how to achieve this:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-249">The following snippet gives an example of how to achieve this:</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

<span data-ttu-id="9c0f5-250">In this snippet, if the file did not exist, it would lead to a state where the script actually exits gracefully after printing the error message, and the cluster reaches running state assuming it "successfully" completed cluster customization process.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-250">In this snippet, if the file did not exist, it would lead to a state where the script actually exits gracefully after printing the error message, and the cluster reaches running state assuming it "successfully" completed cluster customization process.</span></span> <span data-ttu-id="9c0f5-251">If you want to be accurately notified of the fact that cluster customization essentially did not succeed as expected because of a missing file, it is more appropriate to throw an exception and fail the cluster customization step.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-251">If you want to be accurately notified of the fact that cluster customization essentially did not succeed as expected because of a missing file, it is more appropriate to throw an exception and fail the cluster customization step.</span></span> <span data-ttu-id="9c0f5-252">To achieve this you must use the following sample code snippet instead.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-252">To achieve this you must use the following sample code snippet instead.</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a><span data-ttu-id="9c0f5-253">Checklist for deploying a script action</span><span class="sxs-lookup"><span data-stu-id="9c0f5-253">Checklist for deploying a script action</span></span>
<span data-ttu-id="9c0f5-254">Here are the steps we took when preparing to deploy these scripts:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-254">Here are the steps we took when preparing to deploy these scripts:</span></span>

1. <span data-ttu-id="9c0f5-255">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-255">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="9c0f5-256">This can be any of the default or additional Storage accounts specified at the time of cluster deployment, or any other publicly accessible storage container.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-256">This can be any of the default or additional Storage accounts specified at the time of cluster deployment, or any other publicly accessible storage container.</span></span>
2. <span data-ttu-id="9c0f5-257">Add checks into scripts to make sure that they execute idempotently, so that the script can be executed multiple times on the same node.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-257">Add checks into scripts to make sure that they execute idempotently, so that the script can be executed multiple times on the same node.</span></span>
3. <span data-ttu-id="9c0f5-258">Use the **Write-Output** Azure PowerShell cmdlet to print to STDOUT as well as STDERR.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-258">Use the **Write-Output** Azure PowerShell cmdlet to print to STDOUT as well as STDERR.</span></span> <span data-ttu-id="9c0f5-259">Do not use **Write-Host**.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-259">Do not use **Write-Host**.</span></span>
4. <span data-ttu-id="9c0f5-260">Use a temporary file folder, such as $env:TEMP, to keep the downloaded file used by the scripts and then clean them up after scripts have executed.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-260">Use a temporary file folder, such as $env:TEMP, to keep the downloaded file used by the scripts and then clean them up after scripts have executed.</span></span>
5. <span data-ttu-id="9c0f5-261">Install custom software only at D:\ or C:\apps.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-261">Install custom software only at D:\ or C:\apps.</span></span> <span data-ttu-id="9c0f5-262">Other locations on the C: drive should not be used as they are reserved.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-262">Other locations on the C: drive should not be used as they are reserved.</span></span> <span data-ttu-id="9c0f5-263">Note that installing files on the C: drive outside of the C:\apps folder may result in setup failures during re-images of the node.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-263">Note that installing files on the C: drive outside of the C:\apps folder may result in setup failures during re-images of the node.</span></span>
6. <span data-ttu-id="9c0f5-264">In the event that OS-level settings or Hadoop service configuration files were changed, you may want to restart HDInsight services so that they can pick up any OS-level settings, such as the environment variables set in the scripts.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-264">In the event that OS-level settings or Hadoop service configuration files were changed, you may want to restart HDInsight services so that they can pick up any OS-level settings, such as the environment variables set in the scripts.</span></span>

## <a name="debug-custom-scripts"></a><span data-ttu-id="9c0f5-265">Debug custom scripts</span><span class="sxs-lookup"><span data-stu-id="9c0f5-265">Debug custom scripts</span></span>
<span data-ttu-id="9c0f5-266">The script error logs are stored, along with other output, in the default Storage account that you specified for the cluster at its creation.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-266">The script error logs are stored, along with other output, in the default Storage account that you specified for the cluster at its creation.</span></span> <span data-ttu-id="9c0f5-267">The logs are stored in a table with the name *u<\cluster-name-fragment><\time-stamp>setuplog*.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-267">The logs are stored in a table with the name *u<\cluster-name-fragment><\time-stamp>setuplog*.</span></span> <span data-ttu-id="9c0f5-268">These are aggregated logs that have records from all of the nodes (head node and worker nodes) on which the script runs in the cluster.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-268">These are aggregated logs that have records from all of the nodes (head node and worker nodes) on which the script runs in the cluster.</span></span>
<span data-ttu-id="9c0f5-269">An easy way to check the logs is to use HDInsight Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-269">An easy way to check the logs is to use HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="9c0f5-270">For installing the tools, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="9c0f5-270">For installing the tools, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span></span>

<span data-ttu-id="9c0f5-271">**To check the log using Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="9c0f5-271">**To check the log using Visual Studio**</span></span>

1. <span data-ttu-id="9c0f5-272">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-272">Open Visual Studio.</span></span>
2. <span data-ttu-id="9c0f5-273">Click **View**, and then click **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-273">Click **View**, and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="9c0f5-274">Right-click "Azure", click Connect to **Microsoft Azure Subscriptions**, and then enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-274">Right-click "Azure", click Connect to **Microsoft Azure Subscriptions**, and then enter your credentials.</span></span>
4. <span data-ttu-id="9c0f5-275">Expand **Storage**, expand the Azure storage account used as the default file system, expand **Tables**, and then double-click the table name.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-275">Expand **Storage**, expand the Azure storage account used as the default file system, expand **Tables**, and then double-click the table name.</span></span>

<span data-ttu-id="9c0f5-276">You can also remote into the cluster nodes to see the both STDOUT and STDERR for custom scripts.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-276">You can also remote into the cluster nodes to see the both STDOUT and STDERR for custom scripts.</span></span> <span data-ttu-id="9c0f5-277">The logs on each node are specific only to that node and are logged into **C:\HDInsightLogs\DeploymentAgent.log**.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-277">The logs on each node are specific only to that node and are logged into **C:\HDInsightLogs\DeploymentAgent.log**.</span></span> <span data-ttu-id="9c0f5-278">These log files record all outputs from the custom script.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-278">These log files record all outputs from the custom script.</span></span> <span data-ttu-id="9c0f5-279">An example log snippet for a Spark script action looks like this:</span><span class="sxs-lookup"><span data-stu-id="9c0f5-279">An example log snippet for a Spark script action looks like this:</span></span>

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


<span data-ttu-id="9c0f5-280">In this log, it is clear that the Spark script action has been executed on the VM named HEADNODE0 and that no exceptions were thrown during the execution.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-280">In this log, it is clear that the Spark script action has been executed on the VM named HEADNODE0 and that no exceptions were thrown during the execution.</span></span>

<span data-ttu-id="9c0f5-281">In the event that an execution failure occurs, the output describing it will also be contained in this log file.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-281">In the event that an execution failure occurs, the output describing it will also be contained in this log file.</span></span> <span data-ttu-id="9c0f5-282">The information provided in these logs should be helpful in debugging script problems that may arise.</span><span class="sxs-lookup"><span data-stu-id="9c0f5-282">The information provided in these logs should be helpful in debugging script problems that may arise.</span></span>

## <a name="see-also"></a><span data-ttu-id="9c0f5-283">See also</span><span class="sxs-lookup"><span data-stu-id="9c0f5-283">See also</span></span>
* <span data-ttu-id="9c0f5-284">[Customize HDInsight clusters using Script Action][hdinsight-cluster-customize]</span><span class="sxs-lookup"><span data-stu-id="9c0f5-284">[Customize HDInsight clusters using Script Action][hdinsight-cluster-customize]</span></span>
* <span data-ttu-id="9c0f5-285">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="9c0f5-285">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="9c0f5-286">[Install and use R on HDInsight clusters][hdinsight-r-scripts]</span><span class="sxs-lookup"><span data-stu-id="9c0f5-286">[Install and use R on HDInsight clusters][hdinsight-r-scripts]</span></span>
* <span data-ttu-id="9c0f5-287">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-287">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="9c0f5-288">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="9c0f5-288">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
