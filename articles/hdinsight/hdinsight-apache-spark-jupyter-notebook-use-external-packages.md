---
title: Use custom Maven packages with Jupyter notebooks in Spark on Azure | Microsoft Docs
description: Step-by-step instructions on how to configure Jupyter notebooks available with HDInsight Spark clusters to use external Spark packages.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: 0dbe32816d67f8977804f4744f0df7ccba59a737
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550727"
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight
> [!div class="op_single_selector"]
> * [Using cell magic](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Using Script Action](hdinsight-apache-spark-python-package-installation.md)
>
>

Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster. 

You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available. You can also get a list of available packages from other sources. For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).

In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.



## <a name="prerequisites"></a>Prerequisites
You must have the following:

* An Azure subscription. See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* An Apache Spark cluster on HDInsight. For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="use-external-packages-with-jupyter-notebooks"></a>Use external packages with Jupyter notebooks
1. From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard). You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.   
2. From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**. If prompted, enter the admin credentials for the cluster.

    > [!NOTE]
    > You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser. Replace **CLUSTERNAME** with the name of your cluster:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. Create a new notebook. Click **New**, and then click **Spark**.
   
    ![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")

4. A new notebook is created and opened with the name Untitled.pynb. Click the notebook name at the top, and enter a friendly name.
   
    ![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")

5. You will use the `%%configure` magic to configure the notebook to use an external package. In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell. This ensures that the kernel is configured to use the package before the session starts.

    >[!IMPORTANT] 
    >If you forget to configure the kernel in the first cell, you can use the `%%configure` with the `-f` parameter, but that will restart the session and all progress will be lost.

    | HDInsight version | Command |
    |-------------------|---------|
    |For HDInsight 3.3 and HDInsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | For HDInsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. The snippet above expects the maven coordinates for the external package in Maven Central Repository. In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package. Here's how you construct the coordinates for a package.
   
    a. Locate the package in the Maven Repository. For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**. Make sure that the values you gather match your cluster. In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster. You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit. You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.
   
    ![Use external packages with Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")
   
    c. Concatenate the three values, separated by a colon (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Run the code cell with the `%%configure` magic. This will configure the underlying Livy session to use the package you provided. In the subsequent cells in the notebook, you can now use the package, as shown below.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a>See also
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

* [Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux](hdinsight-apache-spark-python-package-installation.md)
* [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Use Zeppelin notebooks with a Spark cluster on HDInsight](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [Kernels available for Jupyter notebook in Spark cluster for HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Install Jupyter on your computer and connect to an HDInsight Spark cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Manage resources
* [Manage resources for the Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight](hdinsight-apache-spark-job-debugging.md)




