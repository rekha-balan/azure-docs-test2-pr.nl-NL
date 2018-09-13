---
title: Use extended Spark History Server to debug and diagnose Spark applications - Azure HDInsight
description: Use extended Spark History Server to debug and diagnose Spark applications - Azure HDInsight.
services: hdinsight
ms.service: hdinsight
author: jejiang
ms.author: jejiang
ms.reviewer: jasonh
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 07/12/2018
ms.openlocfilehash: b514f23f2e8a43f99fd5bf5c3afb5ed625ad4472
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857750"
---
# <a name="use-extended-spark-history-server-to-debug-and-diagnose-spark-applications"></a><span data-ttu-id="7b415-103">Use extended Spark History Server to debug and diagnose Spark applications</span><span class="sxs-lookup"><span data-stu-id="7b415-103">Use extended Spark History Server to debug and diagnose Spark applications</span></span>

<span data-ttu-id="7b415-104">This article provides guidance on how to use extended Spark History Server to debug and diagnose completed and running Spark applications.</span><span class="sxs-lookup"><span data-stu-id="7b415-104">This article provides guidance on how to use extended Spark History Server to debug and diagnose completed and running Spark applications.</span></span> <span data-ttu-id="7b415-105">The extension currently includes data tab and graph tab. In data tab, users can check the input and output data of the Spark job.</span><span class="sxs-lookup"><span data-stu-id="7b415-105">The extension currently includes data tab and graph tab. In data tab, users can check the input and output data of the Spark job.</span></span> <span data-ttu-id="7b415-106">In graph tab, users can check the data flow and replay the job graph.</span><span class="sxs-lookup"><span data-stu-id="7b415-106">In graph tab, users can check the data flow and replay the job graph.</span></span>

## <a name="open-the-spark-history-server"></a><span data-ttu-id="7b415-107">Open the Spark History Server</span><span class="sxs-lookup"><span data-stu-id="7b415-107">Open the Spark History Server</span></span>

<span data-ttu-id="7b415-108">Spark History Server is the web UI for completed and running Spark applications.</span><span class="sxs-lookup"><span data-stu-id="7b415-108">Spark History Server is the web UI for completed and running Spark applications.</span></span> 

### <a name="to-open-the-spark-history-server-web-ui-from-azure-portal"></a><span data-ttu-id="7b415-109">To open the Spark History Server Web UI from Azure portal</span><span class="sxs-lookup"><span data-stu-id="7b415-109">To open the Spark History Server Web UI from Azure portal</span></span>

1. <span data-ttu-id="7b415-110">From the [Azure portal](https://portal.azure.com/), open the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="7b415-110">From the [Azure portal](https://portal.azure.com/), open the Spark cluster.</span></span> <span data-ttu-id="7b415-111">For more information, see [List and show clusters](../hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="7b415-111">For more information, see [List and show clusters](../hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
2. <span data-ttu-id="7b415-112">From **Quick Links**, click **Cluster Dashboard**, and then click **Spark History Server**.</span><span class="sxs-lookup"><span data-stu-id="7b415-112">From **Quick Links**, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span> <span data-ttu-id="7b415-113">When prompted, enter the admin credentials for the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="7b415-113">When prompted, enter the admin credentials for the Spark cluster.</span></span> 

    <span data-ttu-id="7b415-114">![Spark History Server](./media/apache-azure-spark-history-server/launch-history-server.png "Spark History Server")</span><span class="sxs-lookup"><span data-stu-id="7b415-114">![Spark History Server](./media/apache-azure-spark-history-server/launch-history-server.png "Spark History Server")</span></span>

### <a name="to-open-the-spark-history-server-web-ui-by-url"></a><span data-ttu-id="7b415-115">To open the Spark History Server Web UI by URL</span><span class="sxs-lookup"><span data-stu-id="7b415-115">To open the Spark History Server Web UI by URL</span></span>
<span data-ttu-id="7b415-116">Open the Spark History Server by browsing to the following URL, replace <ClusterName> with Spark cluster name of customer.</span><span class="sxs-lookup"><span data-stu-id="7b415-116">Open the Spark History Server by browsing to the following URL, replace <ClusterName> with Spark cluster name of customer.</span></span>

   ```
   https://<ClusterName>.azurehdinsight.net/sparkhistory
   ```

<span data-ttu-id="7b415-117">The Spark History Server web UI looks like:</span><span class="sxs-lookup"><span data-stu-id="7b415-117">The Spark History Server web UI looks like:</span></span>

![HDInsight Spark History Server](./media/apache-azure-spark-history-server/hdinsight-spark-history-server.png)


## <a name="open-the-data-tab-from-spark-history-server"></a><span data-ttu-id="7b415-119">Open the Data tab from Spark History Server</span><span class="sxs-lookup"><span data-stu-id="7b415-119">Open the Data tab from Spark History Server</span></span>
<span data-ttu-id="7b415-120">Select job ID then click **Data** on the tool menu to get the data view.</span><span class="sxs-lookup"><span data-stu-id="7b415-120">Select job ID then click **Data** on the tool menu to get the data view.</span></span>

+ <span data-ttu-id="7b415-121">Check the **Inputs**, **Outputs**, and **Table Operations** by selecting the tabs separately.</span><span class="sxs-lookup"><span data-stu-id="7b415-121">Check the **Inputs**, **Outputs**, and **Table Operations** by selecting the tabs separately.</span></span>

    ![Data tabs](./media/apache-azure-spark-history-server/sparkui-data-tabs.png)

+ <span data-ttu-id="7b415-123">Copy all rows by clicking button **Copy**.</span><span class="sxs-lookup"><span data-stu-id="7b415-123">Copy all rows by clicking button **Copy**.</span></span>

    ![Data copy](./media/apache-azure-spark-history-server/sparkui-data-copy.png)

+ <span data-ttu-id="7b415-125">Save all data as CSV file by clicking button **csv**.</span><span class="sxs-lookup"><span data-stu-id="7b415-125">Save all data as CSV file by clicking button **csv**.</span></span>

    ![Data save](./media/apache-azure-spark-history-server/sparkui-data-save.png)

+ <span data-ttu-id="7b415-127">Search by entering keywords in field **Search**, the search result will display immediately.</span><span class="sxs-lookup"><span data-stu-id="7b415-127">Search by entering keywords in field **Search**, the search result will display immediately.</span></span>

    ![Data search](./media/apache-azure-spark-history-server/sparkui-data-search.png)

+ <span data-ttu-id="7b415-129">Click the column header to sort table, click the plus sign to expand a row to show more details, or click the minus sign to collapse a row.</span><span class="sxs-lookup"><span data-stu-id="7b415-129">Click the column header to sort table, click the plus sign to expand a row to show more details, or click the minus sign to collapse a row.</span></span>

    ![Data table](./media/apache-azure-spark-history-server/sparkui-data-table.png)

+ <span data-ttu-id="7b415-131">Download single file by clicking button **Partial Download** that place at the right, then the selected file will be downloaded to local, if the file does not exist any more, it will open a new tab to show the error messages.</span><span class="sxs-lookup"><span data-stu-id="7b415-131">Download single file by clicking button **Partial Download** that place at the right, then the selected file will be downloaded to local, if the file does not exist any more, it will open a new tab to show the error messages.</span></span>

    ![Data download row](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ <span data-ttu-id="7b415-133">Copy full path or relative path by selecting the **Copy Full Path**, **Copy Relative Path** that expands from download menu.</span><span class="sxs-lookup"><span data-stu-id="7b415-133">Copy full path or relative path by selecting the **Copy Full Path**, **Copy Relative Path** that expands from download menu.</span></span> <span data-ttu-id="7b415-134">For azure data lake storage files, **Open in Azure Storage Explorer** will launch Azure Storage Explorer, and locate to the folder when sign-in.</span><span class="sxs-lookup"><span data-stu-id="7b415-134">For azure data lake storage files, **Open in Azure Storage Explorer** will launch Azure Storage Explorer, and locate to the folder when sign-in.</span></span>

    ![Data copy path](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ <span data-ttu-id="7b415-136">Click the number below the table to navigate pages when too many rows to display in one page.</span><span class="sxs-lookup"><span data-stu-id="7b415-136">Click the number below the table to navigate pages when too many rows to display in one page.</span></span> 

    ![Data page](./media/apache-azure-spark-history-server/sparkui-data-page.png)

+ <span data-ttu-id="7b415-138">Hover on the question mark beside Data to show the tooltip, or click the question mark to get more information.</span><span class="sxs-lookup"><span data-stu-id="7b415-138">Hover on the question mark beside Data to show the tooltip, or click the question mark to get more information.</span></span>

    ![Data more info](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+ <span data-ttu-id="7b415-140">Send feedback with issues by clicking **Provide us feedback**.</span><span class="sxs-lookup"><span data-stu-id="7b415-140">Send feedback with issues by clicking **Provide us feedback**.</span></span>

    ![graph feedback](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="open-the-graph-tab-from-spark-history-server"></a><span data-ttu-id="7b415-142">Open the Graph tab from Spark History Server</span><span class="sxs-lookup"><span data-stu-id="7b415-142">Open the Graph tab from Spark History Server</span></span>
<span data-ttu-id="7b415-143">Select job ID then click **Graph** on the tool menu to get the job graph view.</span><span class="sxs-lookup"><span data-stu-id="7b415-143">Select job ID then click **Graph** on the tool menu to get the job graph view.</span></span>

+ <span data-ttu-id="7b415-144">Check overview of your job by the generated job graph.</span><span class="sxs-lookup"><span data-stu-id="7b415-144">Check overview of your job by the generated job graph.</span></span> 

+ <span data-ttu-id="7b415-145">By default, it will show all jobs, and it could be filtered by **Job ID**.</span><span class="sxs-lookup"><span data-stu-id="7b415-145">By default, it will show all jobs, and it could be filtered by **Job ID**.</span></span>

    ![graph job ID](./media/apache-azure-spark-history-server/sparkui-graph-jobid.png)

+ <span data-ttu-id="7b415-147">By default, **Progress** is selected, user could check the data flow by selecting **Read/Written** in the dropdown list of **Display**.</span><span class="sxs-lookup"><span data-stu-id="7b415-147">By default, **Progress** is selected, user could check the data flow by selecting **Read/Written** in the dropdown list of **Display**.</span></span>

    ![graph display](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

    <span data-ttu-id="7b415-149">The graph node display in color that shows the heatmap.</span><span class="sxs-lookup"><span data-stu-id="7b415-149">The graph node display in color that shows the heatmap.</span></span>

    ![graph heatmap](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)

+ <span data-ttu-id="7b415-151">Play back the job by clicking the **Playback** button and stop anytime by clicking the stop button.</span><span class="sxs-lookup"><span data-stu-id="7b415-151">Play back the job by clicking the **Playback** button and stop anytime by clicking the stop button.</span></span> <span data-ttu-id="7b415-152">The task display in color to show different status when playback:</span><span class="sxs-lookup"><span data-stu-id="7b415-152">The task display in color to show different status when playback:</span></span>

    + <span data-ttu-id="7b415-153">Green for succeeded: The job has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="7b415-153">Green for succeeded: The job has completed successfully.</span></span>
    + <span data-ttu-id="7b415-154">Orange for retried: Instances of tasks that failed but do not affect the final result of the job.</span><span class="sxs-lookup"><span data-stu-id="7b415-154">Orange for retried: Instances of tasks that failed but do not affect the final result of the job.</span></span> <span data-ttu-id="7b415-155">These tasks had duplicate or retry instances that may succeed later.</span><span class="sxs-lookup"><span data-stu-id="7b415-155">These tasks had duplicate or retry instances that may succeed later.</span></span>
    + <span data-ttu-id="7b415-156">Red for failed: The task has failed.</span><span class="sxs-lookup"><span data-stu-id="7b415-156">Red for failed: The task has failed.</span></span>
    + <span data-ttu-id="7b415-157">Blue for running: The task is running.</span><span class="sxs-lookup"><span data-stu-id="7b415-157">Blue for running: The task is running.</span></span>
    + <span data-ttu-id="7b415-158">White for skipped or waiting: The task is waiting to run, or the stage has skipped.</span><span class="sxs-lookup"><span data-stu-id="7b415-158">White for skipped or waiting: The task is waiting to run, or the stage has skipped.</span></span>

    ![graph color sample, running](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)
 
    ![graph color sample, failed](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)
 
    > [!NOTE]
    > <span data-ttu-id="7b415-161">Playback for each job is allowed.</span><span class="sxs-lookup"><span data-stu-id="7b415-161">Playback for each job is allowed.</span></span> <span data-ttu-id="7b415-162">When a job does not have any stage or haven’t complete, playback is not supported.</span><span class="sxs-lookup"><span data-stu-id="7b415-162">When a job does not have any stage or haven’t complete, playback is not supported.</span></span>


+ <span data-ttu-id="7b415-163">Mouse scrolls to zoom in/out the job graph, or click **Zoom to fit** to make it fit to screen.</span><span class="sxs-lookup"><span data-stu-id="7b415-163">Mouse scrolls to zoom in/out the job graph, or click **Zoom to fit** to make it fit to screen.</span></span>
 
    ![graph zoom to fit](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ <span data-ttu-id="7b415-165">Hover on graph node to see the tooltip when there are failed tasks, and click on stage to open stage page.</span><span class="sxs-lookup"><span data-stu-id="7b415-165">Hover on graph node to see the tooltip when there are failed tasks, and click on stage to open stage page.</span></span>

    ![graph tooltip](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ <span data-ttu-id="7b415-167">The job graph node will display the following information of each stage:</span><span class="sxs-lookup"><span data-stu-id="7b415-167">The job graph node will display the following information of each stage:</span></span>
    + <span data-ttu-id="7b415-168">ID.</span><span class="sxs-lookup"><span data-stu-id="7b415-168">ID.</span></span>
    + <span data-ttu-id="7b415-169">Name or description.</span><span class="sxs-lookup"><span data-stu-id="7b415-169">Name or description.</span></span>
    + <span data-ttu-id="7b415-170">Total task number.</span><span class="sxs-lookup"><span data-stu-id="7b415-170">Total task number.</span></span>
    + <span data-ttu-id="7b415-171">Data read: the sum of input size and shuffle read size.</span><span class="sxs-lookup"><span data-stu-id="7b415-171">Data read: the sum of input size and shuffle read size.</span></span>
    + <span data-ttu-id="7b415-172">Data write: the sum of output size and shuffle write size.</span><span class="sxs-lookup"><span data-stu-id="7b415-172">Data write: the sum of output size and shuffle write size.</span></span>
    + <span data-ttu-id="7b415-173">Execution time: the time between start time of the first attempt and completion time of the last attempt.</span><span class="sxs-lookup"><span data-stu-id="7b415-173">Execution time: the time between start time of the first attempt and completion time of the last attempt.</span></span>
    + <span data-ttu-id="7b415-174">Row count: the sum of input records, output records, shuffle read records and shuffle write records.</span><span class="sxs-lookup"><span data-stu-id="7b415-174">Row count: the sum of input records, output records, shuffle read records and shuffle write records.</span></span>
    + <span data-ttu-id="7b415-175">Progress.</span><span class="sxs-lookup"><span data-stu-id="7b415-175">Progress.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7b415-176">By default, the job graph node will display information from last attempt of each stage (except for stage execution time), but during playback graph node will show information of each attempt.</span><span class="sxs-lookup"><span data-stu-id="7b415-176">By default, the job graph node will display information from last attempt of each stage (except for stage execution time), but during playback graph node will show information of each attempt.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7b415-177">For data size of read and write we use 1MB = 1000 KB = 1000 \* 1000 Bytes.</span><span class="sxs-lookup"><span data-stu-id="7b415-177">For data size of read and write we use 1MB = 1000 KB = 1000 \* 1000 Bytes.</span></span>

+ <span data-ttu-id="7b415-178">Send feedback with issues by clicking **Provide us feedback**.</span><span class="sxs-lookup"><span data-stu-id="7b415-178">Send feedback with issues by clicking **Provide us feedback**.</span></span>

    ![graph feedback](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="faq"></a><span data-ttu-id="7b415-180">FAQ</span><span class="sxs-lookup"><span data-stu-id="7b415-180">FAQ</span></span>

### <a name="1-revert-to-community-version"></a><span data-ttu-id="7b415-181">1. Revert to community version</span><span class="sxs-lookup"><span data-stu-id="7b415-181">1. Revert to community version</span></span>

<span data-ttu-id="7b415-182">To revert to community version, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="7b415-182">To revert to community version, do the following steps:</span></span>

1. <span data-ttu-id="7b415-183">Open cluster in Ambari.</span><span class="sxs-lookup"><span data-stu-id="7b415-183">Open cluster in Ambari.</span></span> <span data-ttu-id="7b415-184">Click **Spark2** in left panel.</span><span class="sxs-lookup"><span data-stu-id="7b415-184">Click **Spark2** in left panel.</span></span>
2. <span data-ttu-id="7b415-185">Click **Configs** tab.</span><span class="sxs-lookup"><span data-stu-id="7b415-185">Click **Configs** tab.</span></span>
3. <span data-ttu-id="7b415-186">Expand the group **Custom spark2-defaults**.</span><span class="sxs-lookup"><span data-stu-id="7b415-186">Expand the group **Custom spark2-defaults**.</span></span>
4. <span data-ttu-id="7b415-187">Click **Add Property**, add **spark.ui.enhancement.enabled=false**, save.</span><span class="sxs-lookup"><span data-stu-id="7b415-187">Click **Add Property**, add **spark.ui.enhancement.enabled=false**, save.</span></span>
5. <span data-ttu-id="7b415-188">The property sets to **false** now.</span><span class="sxs-lookup"><span data-stu-id="7b415-188">The property sets to **false** now.</span></span>
6. <span data-ttu-id="7b415-189">Click **Save** to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="7b415-189">Click **Save** to save the configuration.</span></span>

    ![feature turns off](./media/apache-azure-spark-history-server/sparkui-turn-off.png)

7. <span data-ttu-id="7b415-191">Click **Spark2** in left panel, under **Summary** tab, click **Spark2 History Server**.</span><span class="sxs-lookup"><span data-stu-id="7b415-191">Click **Spark2** in left panel, under **Summary** tab, click **Spark2 History Server**.</span></span>

    ![restart server1](./media/apache-azure-spark-history-server/sparkui-restart-1.png) 

8. <span data-ttu-id="7b415-193">Restart history server by clicking **Restart** of **Spark2 History Server**.</span><span class="sxs-lookup"><span data-stu-id="7b415-193">Restart history server by clicking **Restart** of **Spark2 History Server**.</span></span>

    ![restart server2](./media/apache-azure-spark-history-server/sparkui-restart-2.png)  

9. <span data-ttu-id="7b415-195">Refresh the Spark history server web UI, it will be reverted to community version.</span><span class="sxs-lookup"><span data-stu-id="7b415-195">Refresh the Spark history server web UI, it will be reverted to community version.</span></span>

### <a name="2-upload-history-server-event"></a><span data-ttu-id="7b415-196">2. Upload history server event</span><span class="sxs-lookup"><span data-stu-id="7b415-196">2. Upload history server event</span></span>

<span data-ttu-id="7b415-197">If you run into history server error, follow the steps to provide the event:</span><span class="sxs-lookup"><span data-stu-id="7b415-197">If you run into history server error, follow the steps to provide the event:</span></span>
1. <span data-ttu-id="7b415-198">Download event by clicking **Download** in history server web UI.</span><span class="sxs-lookup"><span data-stu-id="7b415-198">Download event by clicking **Download** in history server web UI.</span></span>

    ![download event](./media/apache-azure-spark-history-server/sparkui-download-event.png)

2. <span data-ttu-id="7b415-200">Click **Provide us feedback** from data/graph tab.</span><span class="sxs-lookup"><span data-stu-id="7b415-200">Click **Provide us feedback** from data/graph tab.</span></span>

    ![graph feedback](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

3. <span data-ttu-id="7b415-202">Provide the title and description of error, drag the zip file to the edit field, then click **Submit new issue**.</span><span class="sxs-lookup"><span data-stu-id="7b415-202">Provide the title and description of error, drag the zip file to the edit field, then click **Submit new issue**.</span></span>

    ![file issue](./media/apache-azure-spark-history-server/sparkui-file-issue.png)


### <a name="3-upgrade-jar-file-for-hotfix-scenario"></a><span data-ttu-id="7b415-204">3. Upgrade jar file for hotfix scenario</span><span class="sxs-lookup"><span data-stu-id="7b415-204">3. Upgrade jar file for hotfix scenario</span></span>

<span data-ttu-id="7b415-205">If you want to upgrade with hotfix, use the script below which will upgrade spark-enhancement.jar\*.</span><span class="sxs-lookup"><span data-stu-id="7b415-205">If you want to upgrade with hotfix, use the script below which will upgrade spark-enhancement.jar\*.</span></span>

<span data-ttu-id="7b415-206">**upgrade_spark_enhancement.sh**:</span><span class="sxs-lookup"><span data-stu-id="7b415-206">**upgrade_spark_enhancement.sh**:</span></span>

   ```bash
    #!/usr/bin/env bash

    # Copyright (C) Microsoft Corporation. All rights reserved.

    # Arguments:
    # $1 Enhancement jar path

    if [ "$#" -ne 1 ]; then
        >&2 echo "Please provide the upgrade jar path."
        exit 1
    fi

    install_jar() {
        tmp_jar_path="/tmp/spark-enhancement-hotfix-$( date +%s )"

        if wget -O "$tmp_jar_path" "$2"; then
            for FILE in "$1"/spark-enhancement*.jar
            do
                back_up_path="$FILE.original.$( date +%s )"
                echo "Back up $FILE to $back_up_path"
                mv "$FILE" "$back_up_path"
                echo "Copy the hotfix jar file from $tmp_jar_path   to $FILE"
                cp "$tmp_jar_path" "$FILE"

                "Hotfix done."
                break
            done
        else    
            >&2 echo "Download jar file failed."
            exit 1
        fi
    }

    jars_folder="/usr/hdp/current/spark2-client/jars"
    jar_path=$1

    if ls ${jars_folder}/spark-enhancement*.jar 1>/dev/null 2>&1;   then
        install_jar "$jars_folder" "$jar_path"
    else
        >&2 echo "There is no target jar on this node. Exit with no action."
        exit 0
    fi
   ```

<span data-ttu-id="7b415-207">**Usage**:</span><span class="sxs-lookup"><span data-stu-id="7b415-207">**Usage**:</span></span> 

`upgrade_spark_enhancement.sh https://${jar_path}`

<span data-ttu-id="7b415-208">**Example**:</span><span class="sxs-lookup"><span data-stu-id="7b415-208">**Example**:</span></span>

`upgrade_spark_enhancement.sh https://${account_name}.blob.core.windows.net/packages/jars/spark-enhancement-${version}.tgz` 

<span data-ttu-id="7b415-209">**To use the bash file from Azure portal**</span><span class="sxs-lookup"><span data-stu-id="7b415-209">**To use the bash file from Azure portal**</span></span>

1. <span data-ttu-id="7b415-210">Launch [Azure Portal](https://ms.portal.azure.com), and select your cluster.</span><span class="sxs-lookup"><span data-stu-id="7b415-210">Launch [Azure Portal](https://ms.portal.azure.com), and select your cluster.</span></span>
2. <span data-ttu-id="7b415-211">Click **Script actions**, then **Submit new**.</span><span class="sxs-lookup"><span data-stu-id="7b415-211">Click **Script actions**, then **Submit new**.</span></span> <span data-ttu-id="7b415-212">Complete the **Submit script action** form, then click **Create** button.</span><span class="sxs-lookup"><span data-stu-id="7b415-212">Complete the **Submit script action** form, then click **Create** button.</span></span>
    
    + <span data-ttu-id="7b415-213">**Script type**: select **Custom**.</span><span class="sxs-lookup"><span data-stu-id="7b415-213">**Script type**: select **Custom**.</span></span>
    + <span data-ttu-id="7b415-214">**Name**: specify a script name.</span><span class="sxs-lookup"><span data-stu-id="7b415-214">**Name**: specify a script name.</span></span>
    + <span data-ttu-id="7b415-215">**Bash script URI**: upload the bash file to private cluster then copy URL here.</span><span class="sxs-lookup"><span data-stu-id="7b415-215">**Bash script URI**: upload the bash file to private cluster then copy URL here.</span></span> <span data-ttu-id="7b415-216">Alternatively, use the URI provided.</span><span class="sxs-lookup"><span data-stu-id="7b415-216">Alternatively, use the URI provided.</span></span>
    
   ```upgrade_spark_enhancement
    https://hdinsighttoolingstorage.blob.core.windows.net/shsscriptactions/upgrade_spark_enhancement.sh
   ```

    + <span data-ttu-id="7b415-217">Check on **Head** and **Worker**.</span><span class="sxs-lookup"><span data-stu-id="7b415-217">Check on **Head** and **Worker**.</span></span>
    + <span data-ttu-id="7b415-218">**Parameters**: set the parameters follow the bash usage.</span><span class="sxs-lookup"><span data-stu-id="7b415-218">**Parameters**: set the parameters follow the bash usage.</span></span>

    ![upload log or upgrade hotfix](./media/apache-azure-spark-history-server/sparkui-upload2.png)


## <a name="known-issue"></a><span data-ttu-id="7b415-220">Known issue</span><span class="sxs-lookup"><span data-stu-id="7b415-220">Known issue</span></span>

1.  <span data-ttu-id="7b415-221">Currently, it only works for Spark 2.3 cluster.</span><span class="sxs-lookup"><span data-stu-id="7b415-221">Currently, it only works for Spark 2.3 cluster.</span></span>

2.  <span data-ttu-id="7b415-222">Input/output data using RDD will not show in data tab.</span><span class="sxs-lookup"><span data-stu-id="7b415-222">Input/output data using RDD will not show in data tab.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b415-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b415-223">Next steps</span></span>

* [<span data-ttu-id="7b415-224">Manage resources for a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b415-224">Manage resources for a Spark cluster on HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="7b415-225">Configure Spark settings</span><span class="sxs-lookup"><span data-stu-id="7b415-225">Configure Spark settings</span></span>](apache-spark-settings.md)


## <a name="contact-us"></a><span data-ttu-id="7b415-226">Contact us</span><span class="sxs-lookup"><span data-stu-id="7b415-226">Contact us</span></span>

<span data-ttu-id="7b415-227">If you have any feedback, or if you encounter any other problems when using this tool, send an email at ([hdivstool@microsoft.com](mailto:hdivstool@microsoft.com)).</span><span class="sxs-lookup"><span data-stu-id="7b415-227">If you have any feedback, or if you encounter any other problems when using this tool, send an email at ([hdivstool@microsoft.com](mailto:hdivstool@microsoft.com)).</span></span>
