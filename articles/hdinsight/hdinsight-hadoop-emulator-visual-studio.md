---
title: Azure Data Lake Tools for Visual Studio with Hortonworks Sandbox | Microsoft Docs
description: Learn how to use the Azure Data Lake Tools for VIsual Studio with the Hortonworks sandbox (running in a local VM.) With these tools, you can create and run Hive and Pig jobs on the sandbox and view job output and history.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/28/2017
ms.author: larryfr
ms.openlocfilehash: 5674a2745b1fe746a5e8b59297b0f215546a83aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661815"
---
# <a name="use-the-azure-data-lake-tools-for-visual-studio-with-the-hortonworks-sandbox"></a><span data-ttu-id="33e14-103">Use the Azure Data Lake Tools for Visual Studio with the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="33e14-103">Use the Azure Data Lake Tools for Visual Studio with the Hortonworks Sandbox</span></span>

<span data-ttu-id="33e14-104">The Azure Data Lake tools for Visual Studio include tools for working with generic Hadoop clusters, in addition to tools for working with Azure Data Lake and HDInsight.</span><span class="sxs-lookup"><span data-stu-id="33e14-104">The Azure Data Lake tools for Visual Studio include tools for working with generic Hadoop clusters, in addition to tools for working with Azure Data Lake and HDInsight.</span></span> <span data-ttu-id="33e14-105">This document provides the steps needed to use the Azure Data Lake tools with the Hortonworks Sandbox running in a local virtual machine.</span><span class="sxs-lookup"><span data-stu-id="33e14-105">This document provides the steps needed to use the Azure Data Lake tools with the Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="33e14-106">Using the Hortonworks Sandbox allows you to work with Hadoop locally on your development environment.</span><span class="sxs-lookup"><span data-stu-id="33e14-106">Using the Hortonworks Sandbox allows you to work with Hadoop locally on your development environment.</span></span> <span data-ttu-id="33e14-107">Once you have developed a solution and want to deploy it at scale, you can then move to an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="33e14-107">Once you have developed a solution and want to deploy it at scale, you can then move to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33e14-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="33e14-108">Prerequisites</span></span>

* <span data-ttu-id="33e14-109">The Hortonworks Sandbox running in a virtual machine on your development environment.</span><span class="sxs-lookup"><span data-stu-id="33e14-109">The Hortonworks Sandbox running in a virtual machine on your development environment.</span></span> <span data-ttu-id="33e14-110">This document was written and tested with the sandbox running in Oracle VirtualBox, which was configured using the information in the [Get started in the Hadoop ecosystem](hdinsight-hadoop-emulator-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="33e14-110">This document was written and tested with the sandbox running in Oracle VirtualBox, which was configured using the information in the [Get started in the Hadoop ecosystem](hdinsight-hadoop-emulator-get-started.md) document.</span></span>

* <span data-ttu-id="33e14-111">Visual Studio 2013, 2015, or 2017 any edition.</span><span class="sxs-lookup"><span data-stu-id="33e14-111">Visual Studio 2013, 2015, or 2017 any edition.</span></span>

* <span data-ttu-id="33e14-112">The [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or higher.</span><span class="sxs-lookup"><span data-stu-id="33e14-112">The [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or higher.</span></span>

* <span data-ttu-id="33e14-113">[Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="33e14-113">[Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-the-sandbox"></a><span data-ttu-id="33e14-114">Configure passwords for the sandbox</span><span class="sxs-lookup"><span data-stu-id="33e14-114">Configure passwords for the sandbox</span></span>

<span data-ttu-id="33e14-115">Make sure that the Hortonworks Sandbox is running, then follow the steps in [Get started in the Hadoop ecosystem](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords).</span><span class="sxs-lookup"><span data-stu-id="33e14-115">Make sure that the Hortonworks Sandbox is running, then follow the steps in [Get started in the Hadoop ecosystem](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords).</span></span> <span data-ttu-id="33e14-116">These steps configure the password for the SSH `root` account, and the Ambari `admin` account.</span><span class="sxs-lookup"><span data-stu-id="33e14-116">These steps configure the password for the SSH `root` account, and the Ambari `admin` account.</span></span> <span data-ttu-id="33e14-117">These passwords are used when connecting to the sandbox from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33e14-117">These passwords are used when connecting to the sandbox from Visual Studio.</span></span>

## <a name="connect-the-tools-to-the-sandbox"></a><span data-ttu-id="33e14-118">Connect the tools to the sandbox</span><span class="sxs-lookup"><span data-stu-id="33e14-118">Connect the tools to the sandbox</span></span>

1. <span data-ttu-id="33e14-119">Open Visual Studio, and select **View**, then **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="33e14-119">Open Visual Studio, and select **View**, then **Server Explorer**.</span></span>

2. <span data-ttu-id="33e14-120">From **Server Explorer**, right-click the **HDInsight** entry, and then select **Connect to HDInsight Emulator**.</span><span class="sxs-lookup"><span data-stu-id="33e14-120">From **Server Explorer**, right-click the **HDInsight** entry, and then select **Connect to HDInsight Emulator**.</span></span>

    ![Connect to HDInsight Emulator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="33e14-122">From the **Connect to HDInsight Emulator** dialog, enter the password that you configured for Ambari.</span><span class="sxs-lookup"><span data-stu-id="33e14-122">From the **Connect to HDInsight Emulator** dialog, enter the password that you configured for Ambari.</span></span>

    ![Enter Ambari password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="33e14-124">Select **Next** to continue.</span><span class="sxs-lookup"><span data-stu-id="33e14-124">Select **Next** to continue.</span></span>

4. <span data-ttu-id="33e14-125">Use the **Password** field to enter the password you configured for the `root` account.</span><span class="sxs-lookup"><span data-stu-id="33e14-125">Use the **Password** field to enter the password you configured for the `root` account.</span></span> <span data-ttu-id="33e14-126">Leave the other fields at the default value.</span><span class="sxs-lookup"><span data-stu-id="33e14-126">Leave the other fields at the default value.</span></span>

    ![Enter root password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="33e14-128">Select **Next** to continue.</span><span class="sxs-lookup"><span data-stu-id="33e14-128">Select **Next** to continue.</span></span>

5. <span data-ttu-id="33e14-129">Wait for validation of the services to complete.</span><span class="sxs-lookup"><span data-stu-id="33e14-129">Wait for validation of the services to complete.</span></span> <span data-ttu-id="33e14-130">In some cases, validation may fail and prompt you to update the configuration.</span><span class="sxs-lookup"><span data-stu-id="33e14-130">In some cases, validation may fail and prompt you to update the configuration.</span></span> <span data-ttu-id="33e14-131">If validation fails, select the **update** button and wait for the configuration and verification for the service to complete.</span><span class="sxs-lookup"><span data-stu-id="33e14-131">If validation fails, select the **update** button and wait for the configuration and verification for the service to complete.</span></span>

    ![Errors and update button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="33e14-133">The update process uses Ambari to modify the Hortonworks Sandbox configuration to what is expected by the Azure Data Lake tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33e14-133">The update process uses Ambari to modify the Hortonworks Sandbox configuration to what is expected by the Azure Data Lake tools for Visual Studio.</span></span>

    <span data-ttu-id="33e14-134">Once validation has completed, select **Finish** to complete configuration.</span><span class="sxs-lookup"><span data-stu-id="33e14-134">Once validation has completed, select **Finish** to complete configuration.</span></span>

    ![Finish connecting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

    > [!NOTE]
    > <span data-ttu-id="33e14-136">Depending on the speed of your development environment, and the amount of memory allocated to the virtual machine, it can take several minutes to configure and validate the services.</span><span class="sxs-lookup"><span data-stu-id="33e14-136">Depending on the speed of your development environment, and the amount of memory allocated to the virtual machine, it can take several minutes to configure and validate the services.</span></span>

<span data-ttu-id="33e14-137">After following these steps, you now have an "HDInsight local cluster" entry in Server Explorer under the HDInsight section.</span><span class="sxs-lookup"><span data-stu-id="33e14-137">After following these steps, you now have an "HDInsight local cluster" entry in Server Explorer under the HDInsight section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="33e14-138">Write a Hive query</span><span class="sxs-lookup"><span data-stu-id="33e14-138">Write a Hive query</span></span>

<span data-ttu-id="33e14-139">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span><span class="sxs-lookup"><span data-stu-id="33e14-139">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="33e14-140">Use the following steps to learn how to run ad-hoc queries against the local cluster.</span><span class="sxs-lookup"><span data-stu-id="33e14-140">Use the following steps to learn how to run ad-hoc queries against the local cluster.</span></span>

1. <span data-ttu-id="33e14-141">In **Server Explorer**, right-click on the entry for the local cluster that you added previously, and then select **Write a Hive query**.</span><span class="sxs-lookup"><span data-stu-id="33e14-141">In **Server Explorer**, right-click on the entry for the local cluster that you added previously, and then select **Write a Hive query**.</span></span>

    ![Write a hive query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="33e14-143">This opens a new query window that allows you to quickly type up and submit a query to the local cluster.</span><span class="sxs-lookup"><span data-stu-id="33e14-143">This opens a new query window that allows you to quickly type up and submit a query to the local cluster.</span></span>

2. <span data-ttu-id="33e14-144">In the new query window, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="33e14-144">In the new query window, enter the following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="33e14-145">From the top of the query window, make sure that configuration for the local cluster is selected, and then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="33e14-145">From the top of the query window, make sure that configuration for the local cluster is selected, and then select **Submit**.</span></span> <span data-ttu-id="33e14-146">Leave the other values (**Batch** and server name) at the default values.</span><span class="sxs-lookup"><span data-stu-id="33e14-146">Leave the other values (**Batch** and server name) at the default values.</span></span>

    ![query window and submit button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="33e14-148">You can also use the drop-down menu next to **Submit** to select **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="33e14-148">You can also use the drop-down menu next to **Submit** to select **Advanced**.</span></span> <span data-ttu-id="33e14-149">Advanced options allow you to provide additional options when submitting the job.</span><span class="sxs-lookup"><span data-stu-id="33e14-149">Advanced options allow you to provide additional options when submitting the job.</span></span>

    ![advanced submit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="33e14-151">Once you submit the query, the job status appears.</span><span class="sxs-lookup"><span data-stu-id="33e14-151">Once you submit the query, the job status appears.</span></span> <span data-ttu-id="33e14-152">The job status displays information on the job as it is processed by Hadoop.</span><span class="sxs-lookup"><span data-stu-id="33e14-152">The job status displays information on the job as it is processed by Hadoop.</span></span> <span data-ttu-id="33e14-153">The **Job State** entry provides the status of the job.</span><span class="sxs-lookup"><span data-stu-id="33e14-153">The **Job State** entry provides the status of the job.</span></span> <span data-ttu-id="33e14-154">The state is updated periodically, or you can use the refresh icon to manually refresh the state.</span><span class="sxs-lookup"><span data-stu-id="33e14-154">The state is updated periodically, or you can use the refresh icon to manually refresh the state.</span></span>

    ![Job state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="33e14-156">Once the **Job Status** changes to **Finished**, a Directed Acyclic Graph (DAG) is displayed.</span><span class="sxs-lookup"><span data-stu-id="33e14-156">Once the **Job Status** changes to **Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="33e14-157">This diagram describes the execution path that was determined by Tez (the default execution engine for Hive on the local cluster.)</span><span class="sxs-lookup"><span data-stu-id="33e14-157">This diagram describes the execution path that was determined by Tez (the default execution engine for Hive on the local cluster.)</span></span>

    > [!NOTE]
    > <span data-ttu-id="33e14-158">Tez is also the default when using Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="33e14-158">Tez is also the default when using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="33e14-159">It is not the default on Windows-based HDInsight; to use it there, you must add the line `set hive.execution.engine = tez;` to the beginning of your Hive query.</span><span class="sxs-lookup"><span data-stu-id="33e14-159">It is not the default on Windows-based HDInsight; to use it there, you must add the line `set hive.execution.engine = tez;` to the beginning of your Hive query.</span></span>

    <span data-ttu-id="33e14-160">Use the **Job Output** link to view the output.</span><span class="sxs-lookup"><span data-stu-id="33e14-160">Use the **Job Output** link to view the output.</span></span> <span data-ttu-id="33e14-161">In this case, it is **823**; the number of rows in the sample_08 table.</span><span class="sxs-lookup"><span data-stu-id="33e14-161">In this case, it is **823**; the number of rows in the sample_08 table.</span></span> <span data-ttu-id="33e14-162">You can view diagnostics information about the job by using the **Job Log** and **Download YARN Log** links.</span><span class="sxs-lookup"><span data-stu-id="33e14-162">You can view diagnostics information about the job by using the **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="33e14-163">You can also run Hive jobs interactively by changing the **Batch** field to **Interactive**, and then select **Execute**.</span><span class="sxs-lookup"><span data-stu-id="33e14-163">You can also run Hive jobs interactively by changing the **Batch** field to **Interactive**, and then select **Execute**.</span></span>

    ![Interactive query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="33e14-165">An interactive query streams the output log generated during processing to the **HiveServer2 Output** window.</span><span class="sxs-lookup"><span data-stu-id="33e14-165">An interactive query streams the output log generated during processing to the **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="33e14-166">The information is the same that is available from the **Job Log** link after a job has completed.</span><span class="sxs-lookup"><span data-stu-id="33e14-166">The information is the same that is available from the **Job Log** link after a job has completed.</span></span>

    ![HiveServer2 output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="33e14-168">Create a Hive project</span><span class="sxs-lookup"><span data-stu-id="33e14-168">Create a Hive project</span></span>

<span data-ttu-id="33e14-169">You can also create a project that contains multiple Hive scripts.</span><span class="sxs-lookup"><span data-stu-id="33e14-169">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="33e14-170">A project is useful when you have related scripts that you need to keep together, or maintain using a version control systems.</span><span class="sxs-lookup"><span data-stu-id="33e14-170">A project is useful when you have related scripts that you need to keep together, or maintain using a version control systems.</span></span>

1. <span data-ttu-id="33e14-171">In Visual Studio, select **File**, **New**, and then__Project__.</span><span class="sxs-lookup"><span data-stu-id="33e14-171">In Visual Studio, select **File**, **New**, and then__Project__.</span></span>

2. <span data-ttu-id="33e14-172">From the list of projects, expand **Templates**, **Azure Data Lake** and then select **HIVE (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="33e14-172">From the list of projects, expand **Templates**, **Azure Data Lake** and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="33e14-173">From the list of templates, select **Hive Sample**.</span><span class="sxs-lookup"><span data-stu-id="33e14-173">From the list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="33e14-174">Enter a name and location, then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="33e14-174">Enter a name and location, then select **OK**.</span></span>

    ![HIVE (HDInsight) template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="33e14-176">The **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="33e14-176">The **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="33e14-177">You can submit these using the same **Submit** button at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="33e14-177">You can submit these using the same **Submit** button at the top of the window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="33e14-178">Create a Pig project</span><span class="sxs-lookup"><span data-stu-id="33e14-178">Create a Pig project</span></span>

<span data-ttu-id="33e14-179">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span><span class="sxs-lookup"><span data-stu-id="33e14-179">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="33e14-180">Pig provides a language (Pig Latin) that allows you to develop a pipeline of transformations.</span><span class="sxs-lookup"><span data-stu-id="33e14-180">Pig provides a language (Pig Latin) that allows you to develop a pipeline of transformations.</span></span> <span data-ttu-id="33e14-181">Use the following steps to use Pig with the local cluster:</span><span class="sxs-lookup"><span data-stu-id="33e14-181">Use the following steps to use Pig with the local cluster:</span></span>

1. <span data-ttu-id="33e14-182">Open Visual Studio and select **File**, **New**, and then **Project**.</span><span class="sxs-lookup"><span data-stu-id="33e14-182">Open Visual Studio and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="33e14-183">From the list of projects, expand **Templates**, **Azure Data Lake**, and then select **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="33e14-183">From the list of projects, expand **Templates**, **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="33e14-184">From the list of templates, select **Pig Application**.</span><span class="sxs-lookup"><span data-stu-id="33e14-184">From the list of templates, select **Pig Application**.</span></span> <span data-ttu-id="33e14-185">Enter a name, location, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="33e14-185">Enter a name, location, and then select **OK**.</span></span>

    ![Pig (HDInsight) project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="33e14-187">Enter the following text as the contents of the **script.pig** file that was created with this project.</span><span class="sxs-lookup"><span data-stu-id="33e14-187">Enter the following text as the contents of the **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="33e14-188">While Pig uses a different language than Hive, how you run the jobs is consistent between both languages through the **Submit** button.</span><span class="sxs-lookup"><span data-stu-id="33e14-188">While Pig uses a different language than Hive, how you run the jobs is consistent between both languages through the **Submit** button.</span></span> <span data-ttu-id="33e14-189">Selecting the drop-down beside **Submit** displays an advanced submit dialog for Pig.</span><span class="sxs-lookup"><span data-stu-id="33e14-189">Selecting the drop-down beside **Submit** displays an advanced submit dialog for Pig.</span></span>

    ![Pig advanced submit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="33e14-191">The job status and output is also displayed the same as a Hive query.</span><span class="sxs-lookup"><span data-stu-id="33e14-191">The job status and output is also displayed the same as a Hive query.</span></span>

    ![image of a completed pig job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="33e14-193">View jobs</span><span class="sxs-lookup"><span data-stu-id="33e14-193">View jobs</span></span>

<span data-ttu-id="33e14-194">Azure Data Lake Tools also allow you to easily view information about jobs that have been ran on Hadoop.</span><span class="sxs-lookup"><span data-stu-id="33e14-194">Azure Data Lake Tools also allow you to easily view information about jobs that have been ran on Hadoop.</span></span> <span data-ttu-id="33e14-195">Use the following steps to see the jobs that have been ran on the local cluster.</span><span class="sxs-lookup"><span data-stu-id="33e14-195">Use the following steps to see the jobs that have been ran on the local cluster.</span></span>

1. <span data-ttu-id="33e14-196">From **Server Explorer**, right-click on the local cluster, and then select **View Jobs**.</span><span class="sxs-lookup"><span data-stu-id="33e14-196">From **Server Explorer**, right-click on the local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="33e14-197">A list of jobs that have been submitted to the cluster is displayed.</span><span class="sxs-lookup"><span data-stu-id="33e14-197">A list of jobs that have been submitted to the cluster is displayed.</span></span>

    ![View jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="33e14-199">From the list of jobs, select one to view the job details.</span><span class="sxs-lookup"><span data-stu-id="33e14-199">From the list of jobs, select one to view the job details.</span></span>

    ![select a job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="33e14-201">The information displayed is similar to what you see after running a Hive or Pig query, complete with links to view the output and log information.</span><span class="sxs-lookup"><span data-stu-id="33e14-201">The information displayed is similar to what you see after running a Hive or Pig query, complete with links to view the output and log information.</span></span>

3. <span data-ttu-id="33e14-202">You can also modify and resubmit the job from here.</span><span class="sxs-lookup"><span data-stu-id="33e14-202">You can also modify and resubmit the job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="33e14-203">View Hive databases</span><span class="sxs-lookup"><span data-stu-id="33e14-203">View Hive databases</span></span>

1. <span data-ttu-id="33e14-204">In **Server Explorer**, expand the **HDInsight local cluster** entry, and then expand **Hive Databases**.</span><span class="sxs-lookup"><span data-stu-id="33e14-204">In **Server Explorer**, expand the **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="33e14-205">The **Default** and **xademo** databases on the local cluster are displayed.</span><span class="sxs-lookup"><span data-stu-id="33e14-205">The **Default** and **xademo** databases on the local cluster are displayed.</span></span> <span data-ttu-id="33e14-206">Expanding a database reveals the tables within the database.</span><span class="sxs-lookup"><span data-stu-id="33e14-206">Expanding a database reveals the tables within the database.</span></span>

    ![expanded databases](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="33e14-208">Expanding a table displays the columns for that table.</span><span class="sxs-lookup"><span data-stu-id="33e14-208">Expanding a table displays the columns for that table.</span></span> <span data-ttu-id="33e14-209">You can right-click a table and select **View Top 100 Rows** to quickly view the data.</span><span class="sxs-lookup"><span data-stu-id="33e14-209">You can right-click a table and select **View Top 100 Rows** to quickly view the data.</span></span>

    ![hive databases view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="33e14-211">Database and Table properties</span><span class="sxs-lookup"><span data-stu-id="33e14-211">Database and Table properties</span></span>

<span data-ttu-id="33e14-212">You may have noticed that you can select to view **Properties** on a database or table.</span><span class="sxs-lookup"><span data-stu-id="33e14-212">You may have noticed that you can select to view **Properties** on a database or table.</span></span> <span data-ttu-id="33e14-213">Selecting **Properties** displays details for the selected item in the properties window.</span><span class="sxs-lookup"><span data-stu-id="33e14-213">Selecting **Properties** displays details for the selected item in the properties window.</span></span>

![Properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="33e14-215">Create a table</span><span class="sxs-lookup"><span data-stu-id="33e14-215">Create a table</span></span>

<span data-ttu-id="33e14-216">To create a new table, right-click a database, and then select **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="33e14-216">To create a new table, right-click a database, and then select **Create Table**.</span></span>

![Create table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="33e14-218">You can then create the table using a form.</span><span class="sxs-lookup"><span data-stu-id="33e14-218">You can then create the table using a form.</span></span> <span data-ttu-id="33e14-219">You can see the raw HiveQL that will be used to create the table at the bottom of this page.</span><span class="sxs-lookup"><span data-stu-id="33e14-219">You can see the raw HiveQL that will be used to create the table at the bottom of this page.</span></span>

![create table form](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="33e14-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="33e14-221">Next steps</span></span>

* [<span data-ttu-id="33e14-222">Learning the ropes of the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="33e14-222">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="33e14-223">Hadoop tutorial - Getting started with HDP</span><span class="sxs-lookup"><span data-stu-id="33e14-223">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)






















