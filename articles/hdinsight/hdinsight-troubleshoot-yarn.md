---
title: Troubleshoot YARN in Azure HDInsight
description: Get answers to common questions about working with Apache Hadoop YARN and Azure HDInsight.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.topic: conceptual
ms.date: 11/2/2017
ms.openlocfilehash: f1f332164b5e954b2576f9fbde519241c7288006
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856369"
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="3f796-103">Troubleshoot YARN by using Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3f796-103">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="3f796-104">Learn about the top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="3f796-104">Learn about the top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="3f796-105">How do I create a new YARN queue on a cluster?</span><span class="sxs-lookup"><span data-stu-id="3f796-105">How do I create a new YARN queue on a cluster?</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="3f796-106">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="3f796-106">Resolution steps</span></span> 

<span data-ttu-id="3f796-107">Use the following steps in Ambari to create a new YARN queue, and then balance the capacity allocation among all the queues.</span><span class="sxs-lookup"><span data-stu-id="3f796-107">Use the following steps in Ambari to create a new YARN queue, and then balance the capacity allocation among all the queues.</span></span> 

<span data-ttu-id="3f796-108">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity to 25% capacity, which gives the new queue (spark) 50% capacity.</span><span class="sxs-lookup"><span data-stu-id="3f796-108">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity to 25% capacity, which gives the new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="3f796-109">Queue</span><span class="sxs-lookup"><span data-stu-id="3f796-109">Queue</span></span> | <span data-ttu-id="3f796-110">Capacity</span><span class="sxs-lookup"><span data-stu-id="3f796-110">Capacity</span></span> | <span data-ttu-id="3f796-111">Maximum capacity</span><span class="sxs-lookup"><span data-stu-id="3f796-111">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3f796-112">default</span><span class="sxs-lookup"><span data-stu-id="3f796-112">default</span></span> | <span data-ttu-id="3f796-113">25%</span><span class="sxs-lookup"><span data-stu-id="3f796-113">25%</span></span> | <span data-ttu-id="3f796-114">50%</span><span class="sxs-lookup"><span data-stu-id="3f796-114">50%</span></span> |
| <span data-ttu-id="3f796-115">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="3f796-115">thrftsvr</span></span> | <span data-ttu-id="3f796-116">25%</span><span class="sxs-lookup"><span data-stu-id="3f796-116">25%</span></span> | <span data-ttu-id="3f796-117">50%</span><span class="sxs-lookup"><span data-stu-id="3f796-117">50%</span></span> |
| <span data-ttu-id="3f796-118">spark</span><span class="sxs-lookup"><span data-stu-id="3f796-118">spark</span></span> | <span data-ttu-id="3f796-119">50%</span><span class="sxs-lookup"><span data-stu-id="3f796-119">50%</span></span> | <span data-ttu-id="3f796-120">50%</span><span class="sxs-lookup"><span data-stu-id="3f796-120">50%</span></span> |

1. <span data-ttu-id="3f796-121">Select the **Ambari Views** icon, and then select the grid pattern.</span><span class="sxs-lookup"><span data-stu-id="3f796-121">Select the **Ambari Views** icon, and then select the grid pattern.</span></span> <span data-ttu-id="3f796-122">Next, select **YARN Queue Manager**.</span><span class="sxs-lookup"><span data-stu-id="3f796-122">Next, select **YARN Queue Manager**.</span></span>

    ![Select the Ambari Views icon](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="3f796-124">Select the **default** queue.</span><span class="sxs-lookup"><span data-stu-id="3f796-124">Select the **default** queue.</span></span>

    ![Select the default queue](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="3f796-126">For the **default** queue, change the **capacity** from 50% to 25%.</span><span class="sxs-lookup"><span data-stu-id="3f796-126">For the **default** queue, change the **capacity** from 50% to 25%.</span></span> <span data-ttu-id="3f796-127">For the **thriftsvr** queue, change the **capacity** to 25%.</span><span class="sxs-lookup"><span data-stu-id="3f796-127">For the **thriftsvr** queue, change the **capacity** to 25%.</span></span>

    ![Change the capacity to 25% for the default and thriftsvr queues](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="3f796-129">To create a new queue, select **Add Queue**.</span><span class="sxs-lookup"><span data-stu-id="3f796-129">To create a new queue, select **Add Queue**.</span></span>

    ![Select Add Queue](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="3f796-131">Name the new queue.</span><span class="sxs-lookup"><span data-stu-id="3f796-131">Name the new queue.</span></span>

    ![Name the queue Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="3f796-133">Leave the **capacity** values at 50%, and then select the **Actions** button.</span><span class="sxs-lookup"><span data-stu-id="3f796-133">Leave the **capacity** values at 50%, and then select the **Actions** button.</span></span>

    ![Select the Actions button](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="3f796-135">Select **Save and Refresh Queues**.</span><span class="sxs-lookup"><span data-stu-id="3f796-135">Select **Save and Refresh Queues**.</span></span>

    ![Select Save and Refresh Queues](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="3f796-137">These changes are visible immediately on the YARN Scheduler UI.</span><span class="sxs-lookup"><span data-stu-id="3f796-137">These changes are visible immediately on the YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="3f796-138">Additional reading</span><span class="sxs-lookup"><span data-stu-id="3f796-138">Additional reading</span></span>

- [<span data-ttu-id="3f796-139">YARN CapacityScheduler</span><span class="sxs-lookup"><span data-stu-id="3f796-139">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="3f796-140">How do I download YARN logs from a cluster?</span><span class="sxs-lookup"><span data-stu-id="3f796-140">How do I download YARN logs from a cluster?</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="3f796-141">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="3f796-141">Resolution steps</span></span> 

1. <span data-ttu-id="3f796-142">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span><span class="sxs-lookup"><span data-stu-id="3f796-142">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="3f796-143">For more information, see [Additional reading](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="3f796-143">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="3f796-144">To list all the application IDs of the YARN applications that are currently running, run the following command:</span><span class="sxs-lookup"><span data-stu-id="3f796-144">To list all the application IDs of the YARN applications that are currently running, run the following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="3f796-145">The IDs are listed in the **APPLICATIONID** column.</span><span class="sxs-lookup"><span data-stu-id="3f796-145">The IDs are listed in the **APPLICATIONID** column.</span></span> <span data-ttu-id="3f796-146">You can download logs from the **APPLICATIONID** column.</span><span class="sxs-lookup"><span data-stu-id="3f796-146">You can download logs from the **APPLICATIONID** column.</span></span>

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. <span data-ttu-id="3f796-147">To download YARN container logs for all application masters, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3f796-147">To download YARN container logs for all application masters, use the following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="3f796-148">This command creates a log file named amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="3f796-148">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="3f796-149">To download YARN container logs for only the latest application master, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3f796-149">To download YARN container logs for only the latest application master, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="3f796-150">This command creates a log file named latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="3f796-150">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="3f796-151">To download YARN container logs for the first two application masters, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3f796-151">To download YARN container logs for the first two application masters, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="3f796-152">This command creates a log file named first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="3f796-152">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="3f796-153">To download all YARN container logs, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3f796-153">To download all YARN container logs, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="3f796-154">This command creates a log file named logs.txt.</span><span class="sxs-lookup"><span data-stu-id="3f796-154">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="3f796-155">To download the YARN container log for a specific container, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3f796-155">To download the YARN container log for a specific container, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="3f796-156">This command creates a log file named containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="3f796-156">This command creates a log file named containerlogs.txt.</span></span>

### <a name="additional-reading-2"></a><span data-ttu-id="3f796-157">Additional reading</span><span class="sxs-lookup"><span data-stu-id="3f796-157">Additional reading</span></span>

- [<span data-ttu-id="3f796-158">Connect to HDInsight (Hadoop) by using SSH</span><span class="sxs-lookup"><span data-stu-id="3f796-158">Connect to HDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [<span data-ttu-id="3f796-159">Apache Hadoop YARN concepts and applications</span><span class="sxs-lookup"><span data-stu-id="3f796-159">Apache Hadoop YARN concepts and applications</span></span>](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)


### <a name="see-also"></a><span data-ttu-id="3f796-160">See Also</span><span class="sxs-lookup"><span data-stu-id="3f796-160">See Also</span></span>
[<span data-ttu-id="3f796-161">Troubleshoot by Using Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3f796-161">Troubleshoot by Using Azure HDInsight</span></span>](hdinsight-troubleshoot-guide.md)







