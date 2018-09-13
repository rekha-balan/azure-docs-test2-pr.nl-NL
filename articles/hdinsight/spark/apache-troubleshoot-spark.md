---
title: Troubleshoot Spark in Azure HDInsight
description: Get answers to common questions about working with Apache Spark and Azure HDInsight.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.topic: conceptual
ms.date: 11/2/2017
ms.openlocfilehash: 7c7f89864d9394ff4527f9a0354b9276f7c01c49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867680"
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="13679-103">Troubleshoot Spark by using Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="13679-103">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="13679-104">Learn about the top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="13679-104">Learn about the top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="13679-105">How do I configure a Spark application by using Ambari on clusters?</span><span class="sxs-lookup"><span data-stu-id="13679-105">How do I configure a Spark application by using Ambari on clusters?</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="13679-106">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="13679-106">Resolution steps</span></span>

<span data-ttu-id="13679-107">The configuration values for this procedure were previously set in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13679-107">The configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="13679-108">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="13679-108">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="13679-109">In the list of clusters, select **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="13679-109">In the list of clusters, select **Spark2**.</span></span>

    ![Select cluster from list](./media/apache-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="13679-111">Select the **Configs** tab.</span><span class="sxs-lookup"><span data-stu-id="13679-111">Select the **Configs** tab.</span></span>

    ![Select the Configs tab](./media/apache-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="13679-113">In the list of configurations, select **Custom-spark2-defaults**.</span><span class="sxs-lookup"><span data-stu-id="13679-113">In the list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Select custom-spark-defaults](./media/apache-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="13679-115">Look for the value setting that you need to adjust, such as **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="13679-115">Look for the value setting that you need to adjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="13679-116">In this case, the value of **4608m** is too high.</span><span class="sxs-lookup"><span data-stu-id="13679-116">In this case, the value of **4608m** is too high.</span></span>

    ![Select the spark.executor.memory field](./media/apache-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="13679-118">Set the value to the recommended setting.</span><span class="sxs-lookup"><span data-stu-id="13679-118">Set the value to the recommended setting.</span></span> <span data-ttu-id="13679-119">The value **2048m** is recommended for this setting.</span><span class="sxs-lookup"><span data-stu-id="13679-119">The value **2048m** is recommended for this setting.</span></span>

    ![Change value to 2048m](./media/apache-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="13679-121">Save the value, and then save the configuration.</span><span class="sxs-lookup"><span data-stu-id="13679-121">Save the value, and then save the configuration.</span></span> <span data-ttu-id="13679-122">On the toolbar, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="13679-122">On the toolbar, select **Save**.</span></span>

    ![Save the setting and configuration](./media/apache-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="13679-124">You are notified if any configurations need attention.</span><span class="sxs-lookup"><span data-stu-id="13679-124">You are notified if any configurations need attention.</span></span> <span data-ttu-id="13679-125">Note the items, and then select **Proceed Anyway**.</span><span class="sxs-lookup"><span data-stu-id="13679-125">Note the items, and then select **Proceed Anyway**.</span></span> 

    ![Select Proceed Anyway](./media/apache-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="13679-127">Write a note about the configuration changes, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="13679-127">Write a note about the configuration changes, and then select **Save**.</span></span>

    ![Enter a note about the changes you made](./media/apache-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="13679-129">Whenever a configuration is saved, you are prompted to restart the service.</span><span class="sxs-lookup"><span data-stu-id="13679-129">Whenever a configuration is saved, you are prompted to restart the service.</span></span> <span data-ttu-id="13679-130">Select **Restart**.</span><span class="sxs-lookup"><span data-stu-id="13679-130">Select **Restart**.</span></span>

    ![Select restart](./media/apache-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="13679-132">Confirm the restart.</span><span class="sxs-lookup"><span data-stu-id="13679-132">Confirm the restart.</span></span>

    ![Select Confirm Restart All](./media/apache-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="13679-134">You can review the processes that are running.</span><span class="sxs-lookup"><span data-stu-id="13679-134">You can review the processes that are running.</span></span>

    ![Review running processes](./media/apache-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="13679-136">You can add configurations.</span><span class="sxs-lookup"><span data-stu-id="13679-136">You can add configurations.</span></span> <span data-ttu-id="13679-137">In the list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span><span class="sxs-lookup"><span data-stu-id="13679-137">In the list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Select add property](./media/apache-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="13679-139">Define a new property.</span><span class="sxs-lookup"><span data-stu-id="13679-139">Define a new property.</span></span> <span data-ttu-id="13679-140">You can define a single property by using a dialog box for specific settings such as the data type.</span><span class="sxs-lookup"><span data-stu-id="13679-140">You can define a single property by using a dialog box for specific settings such as the data type.</span></span> <span data-ttu-id="13679-141">Or, you can define multiple properties by using one definition per line.</span><span class="sxs-lookup"><span data-stu-id="13679-141">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="13679-142">In this example, the **spark.driver.memory** property is defined with a value of **4g**.</span><span class="sxs-lookup"><span data-stu-id="13679-142">In this example, the **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Define new property](./media/apache-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="13679-144">Save the configuration, and then restart the service as described in steps 6 and 7.</span><span class="sxs-lookup"><span data-stu-id="13679-144">Save the configuration, and then restart the service as described in steps 6 and 7.</span></span>

<span data-ttu-id="13679-145">These changes are cluster-wide but can be overridden when you submit the Spark job.</span><span class="sxs-lookup"><span data-stu-id="13679-145">These changes are cluster-wide but can be overridden when you submit the Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="13679-146">Additional reading</span><span class="sxs-lookup"><span data-stu-id="13679-146">Additional reading</span></span>

[<span data-ttu-id="13679-147">Spark job submission on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="13679-147">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="13679-148">How do I configure a Spark application by using a Jupyter notebook on clusters?</span><span class="sxs-lookup"><span data-stu-id="13679-148">How do I configure a Spark application by using a Jupyter notebook on clusters?</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="13679-149">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="13679-149">Resolution steps</span></span>

1. <span data-ttu-id="13679-150">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="13679-150">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="13679-151">In the first cell of the Jupyter notebook, after the **%%configure** directive, specify the Spark configurations in valid JSON format.</span><span class="sxs-lookup"><span data-stu-id="13679-151">In the first cell of the Jupyter notebook, after the **%%configure** directive, specify the Spark configurations in valid JSON format.</span></span> <span data-ttu-id="13679-152">Change the actual values as necessary:</span><span class="sxs-lookup"><span data-stu-id="13679-152">Change the actual values as necessary:</span></span>

    ![Add a configuration](./media/apache-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="13679-154">Additional reading</span><span class="sxs-lookup"><span data-stu-id="13679-154">Additional reading</span></span>

[<span data-ttu-id="13679-155">Spark job submission on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="13679-155">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="13679-156">How do I configure a Spark application by using Livy on clusters?</span><span class="sxs-lookup"><span data-stu-id="13679-156">How do I configure a Spark application by using Livy on clusters?</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="13679-157">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="13679-157">Resolution steps</span></span>

1. <span data-ttu-id="13679-158">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="13679-158">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="13679-159">Submit the Spark application to Livy by using a REST client like cURL.</span><span class="sxs-lookup"><span data-stu-id="13679-159">Submit the Spark application to Livy by using a REST client like cURL.</span></span> <span data-ttu-id="13679-160">Use a command similar to the following.</span><span class="sxs-lookup"><span data-stu-id="13679-160">Use a command similar to the following.</span></span> <span data-ttu-id="13679-161">Change the actual values as necessary:</span><span class="sxs-lookup"><span data-stu-id="13679-161">Change the actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="13679-162">Additional reading</span><span class="sxs-lookup"><span data-stu-id="13679-162">Additional reading</span></span>

[<span data-ttu-id="13679-163">Spark job submission on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="13679-163">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="13679-164">How do I configure a Spark application by using spark-submit on clusters?</span><span class="sxs-lookup"><span data-stu-id="13679-164">How do I configure a Spark application by using spark-submit on clusters?</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="13679-165">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="13679-165">Resolution steps</span></span>

1. <span data-ttu-id="13679-166">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="13679-166">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="13679-167">Launch spark-shell by using a command similar to the following.</span><span class="sxs-lookup"><span data-stu-id="13679-167">Launch spark-shell by using a command similar to the following.</span></span> <span data-ttu-id="13679-168">Change the actual value of the configurations as necessary:</span><span class="sxs-lookup"><span data-stu-id="13679-168">Change the actual value of the configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="13679-169">Additional reading</span><span class="sxs-lookup"><span data-stu-id="13679-169">Additional reading</span></span>

[<span data-ttu-id="13679-170">Spark job submission on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="13679-170">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="13679-171">What causes a Spark application OutofMemoryError exception?</span><span class="sxs-lookup"><span data-stu-id="13679-171">What causes a Spark application OutofMemoryError exception?</span></span>

### <a name="detailed-description"></a><span data-ttu-id="13679-172">Detailed description</span><span class="sxs-lookup"><span data-stu-id="13679-172">Detailed description</span></span>

<span data-ttu-id="13679-173">The Spark application fails, with the following types of uncaught exceptions:</span><span class="sxs-lookup"><span data-stu-id="13679-173">The Spark application fails, with the following types of uncaught exceptions:</span></span>

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a><span data-ttu-id="13679-174">Probable cause</span><span class="sxs-lookup"><span data-stu-id="13679-174">Probable cause</span></span>

<span data-ttu-id="13679-175">The most likely cause of this exception is that not enough heap memory is allocated to the Java virtual machines (JVMs).</span><span class="sxs-lookup"><span data-stu-id="13679-175">The most likely cause of this exception is that not enough heap memory is allocated to the Java virtual machines (JVMs).</span></span> <span data-ttu-id="13679-176">These JVMs are launched as executors or drivers as part of the Spark application.</span><span class="sxs-lookup"><span data-stu-id="13679-176">These JVMs are launched as executors or drivers as part of the Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="13679-177">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="13679-177">Resolution steps</span></span>

1. <span data-ttu-id="13679-178">Determine the maximum size of the data the Spark application handles.</span><span class="sxs-lookup"><span data-stu-id="13679-178">Determine the maximum size of the data the Spark application handles.</span></span> <span data-ttu-id="13679-179">You can make a guess based on the maximum size of the input data, the intermediate data that's produced by transforming the input data, and the output data that's produced when the application is further transforming the intermediate data.</span><span class="sxs-lookup"><span data-stu-id="13679-179">You can make a guess based on the maximum size of the input data, the intermediate data that's produced by transforming the input data, and the output data that's produced when the application is further transforming the intermediate data.</span></span> <span data-ttu-id="13679-180">This process can be an iterative if you can't make an initial formal guess.</span><span class="sxs-lookup"><span data-stu-id="13679-180">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="13679-181">Make sure that the HDInsight cluster that you're going to use has enough resources in terms of memory and cores to accommodate the Spark application.</span><span class="sxs-lookup"><span data-stu-id="13679-181">Make sure that the HDInsight cluster that you're going to use has enough resources in terms of memory and cores to accommodate the Spark application.</span></span> <span data-ttu-id="13679-182">You can determine this by viewing the cluster metrics section of the YARN UI for the values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span><span class="sxs-lookup"><span data-stu-id="13679-182">You can determine this by viewing the cluster metrics section of the YARN UI for the values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="13679-183">Set the following Spark configurations to appropriate values, which should not exceed 90% of the available memory and cores.</span><span class="sxs-lookup"><span data-stu-id="13679-183">Set the following Spark configurations to appropriate values, which should not exceed 90% of the available memory and cores.</span></span> <span data-ttu-id="13679-184">The values should be well within the memory requirements of the Spark application:</span><span class="sxs-lookup"><span data-stu-id="13679-184">The values should be well within the memory requirements of the Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="13679-185">To calcuate the total memory used by all executors:</span><span class="sxs-lookup"><span data-stu-id="13679-185">To calcuate the total memory used by all executors:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
   <span data-ttu-id="13679-186">To calcuate the total memory used by the driver:</span><span class="sxs-lookup"><span data-stu-id="13679-186">To calcuate the total memory used by the driver:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="13679-187">Additional reading</span><span class="sxs-lookup"><span data-stu-id="13679-187">Additional reading</span></span>

- [<span data-ttu-id="13679-188">Spark memory management overview</span><span class="sxs-lookup"><span data-stu-id="13679-188">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [<span data-ttu-id="13679-189">Debug a Spark application on an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="13679-189">Debug a Spark application on an HDInsight cluster</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)


### <a name="see-also"></a><span data-ttu-id="13679-190">See Also</span><span class="sxs-lookup"><span data-stu-id="13679-190">See Also</span></span>
[<span data-ttu-id="13679-191">Troubleshoot by Using Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="13679-191">Troubleshoot by Using Azure HDInsight</span></span>](../../hdinsight/hdinsight-troubleshoot-guide.md)

