---
title: MapReduce and SSH connection with Hadoop in HDInsight | Microsoft Docs
description: Learn how to use SSH to run MapReduce jobs using Hadoop on HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/08/2017
ms.author: larryfr
ms.openlocfilehash: fbf33ea6a6362857bf4bc92055cabd9b099a6d0c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550615"
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>Use MapReduce with Hadoop on HDInsight with SSH

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

In this article, you learn how to use Secure Shell (SSH) to connect to a Hadoop on HDInsight cluster and then submit MapReduce jobs by using Hadoop commands.

> [!NOTE]
> If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Prerequisites

To complete the steps in this article, you need the following:

* A Linux-based HDInsight (Hadoop on HDInsight) cluster

  > [!IMPORTANT]
  > Linux is the only operating system used on HDInsight version 3.4 or greater. For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).

* An SSH client. Linux, Unix, and Mac operating systems should come with an SSH client. Windows users must download a client, such as [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

## <a id="ssh"></a>Connect with SSH

Connect to the fully qualified domain name (FQDN) of your HDInsight cluster by using the SSH command. The FQDN is the name you gave the cluster, followed by **.azurehdinsight.net**. For example, the following would connect to a cluster named **myhdinsight**:

    ssh admin@myhdinsight-ssh.azurehdinsight.net

**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system, for example:

    ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net

**If you provided a password for SSH authentication** when you created the HDInsight cluster, you need to provide the password when prompted.

For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="hadoop"></a>Use Hadoop commands

1. After you are connected to the HDInsight cluster, use the following **Hadoop** command to start a MapReduce job:

    ```
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file. As input, it uses the **/example/data/gutenberg/davinci.txt** document, and output is stored at **/example/data/WordCountOutput**.

    > [!NOTE]
    > For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).

2. The job emits details as it processes, and it returns information similar to the following when the job completes:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. When the job completes, use the following command to list the output files that are stored at **wasbs://example/data/WordCountOutput**:

    ```
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    This should display two files, **_SUCCESS** and **part-r-00000**. The **part-r-00000** file contains the output for this job.

    > [!NOTE]
    > Some MapReduce jobs may split the results across multiple **part-r-#####** files. If so, use the ##### suffix to indicate the order of the files.

4. To view the output, use the following command:

    ```
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    This displays a list of the words that are contained in the **wasbs://example/data/gutenberg/davinci.txt** file and the number of times each word occured. The following is an example of the data that is contained in the file:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Summary

As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.

## <a id="nextsteps"></a>Next steps

For general information about MapReduce jobs in HDInsight:

* [Use MapReduce on HDInsight Hadoop](hdinsight-use-mapreduce.md)

For information about other ways you can work with Hadoop on HDInsight:

* [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md)
* [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md)
