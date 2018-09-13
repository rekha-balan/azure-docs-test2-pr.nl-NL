---
title: Known issues for Apache Spark cluster in Azure HDInsight | Microsoft Docs
description: Known issues of Apache Spark clusters in Azure HDInsight.
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: nitinme
ms.openlocfilehash: 2ba5f280b38622b6a0c966d76617cd5698420b92
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662135"
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Known issues for Apache Spark cluster on HDInsight

This document keeps track of all the known issues for the HDInsight Spark public preview.  

## <a name="livy-leaks-interactive-session"></a>Livy leaks interactive session
When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked. Because of this, new jobs can stuck in the Accepted state, and cannot be started.

**Mitigation:**

Use the following procedure to workaround the issue:

1. Ssh into headnode. For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Run the following command to find the application IDs of the interactive jobs started through Livy. 
   
        yarn application –list
   
    The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*. 
3. Run the following command to kill those jobs. 
   
        yarn application –kill <Application ID>

New jobs will start running. 

## <a name="spark-history-server-not-started"></a>Spark History Server not started
Spark History Server is not started automatically after a cluster is created.  

**Mitigation:** 

Manually start the history server from Ambari.

## <a name="permission-issue-in-spark-log-directory"></a>Permission issue in Spark log directory
When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written. 

**Mitigation:**

1. Add hdiuser to the Hadoop group. 
2. Provide 777 permissions on /var/log/spark after cluster creation. 
3. Update the spark log location using Ambari to be a directory with 777 permissions.  
4. Run spark-submit as sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>Spark-Phoenix connector is not supported

Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.

**Mitigation:**

You must use the Spark-HBase connector instead. For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-to-jupyter-notebooks"></a>Issues related to Jupyter notebooks
Following are some known issues related to Jupyter notebooks.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Notebooks with non-ASCII characters in filenames
Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames. If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Error while loading notebooks of larger sizes
You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.  

**Mitigation:**

If you get this error, it does not mean your data is corrupt or lost.  Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them. For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook. You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.  From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.

To prevent this error from happening in the future, you must follow some best practices:

* It is important to keep the notebook size small. Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.  It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.
* Also, when you save a notebook, clear all output cells to reduce the size.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>Notebook initial startup takes longer than expected
First code statement in Jupyter notebook using Spark magic could take more than a minute.  

**Explanation:**

This happens because when the first code cell is run. In the background this initiates session configuration and Spark, SQL, and Hive contexts are set. After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a>Jupyter notebook timeout in creating the session
When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session. 

**Mitigations:** 

1. Free up some resources in your Spark cluster by:
   
   * Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.
   * Stopping other Spark applications from YARN.
2. Restart the notebook you were trying to start up. Enough resources should be available for you to create a session now.

## <a name="see-also"></a>See also
* [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenarios
* [Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark Streaming: Use Spark in HDInsight for building real-time streaming applications](hdinsight-apache-spark-eventhub-streaming.md)
* [Website log analysis using Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Create and run applications
* [Create a standalone application using Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Run jobs remotely on a Spark cluster using Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools and extensions
* [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Use Zeppelin notebooks with a Spark cluster on HDInsight](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [Kernels available for Jupyter notebook in Spark cluster for HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Use external packages with Jupyter notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Install Jupyter on your computer and connect to an HDInsight Spark cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Manage resources
* [Manage resources for the Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight](hdinsight-apache-spark-job-debugging.md)

