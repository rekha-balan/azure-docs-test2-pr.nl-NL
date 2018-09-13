---
title: Use C# with MapReduce on Hadoop in HDInsight - Azure | Microsoft Docs
description: Learn how to use C# to create MapReduce solutions with Hadoop in Azure HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/12/2017
ms.author: larryfr
ms.openlocfilehash: fa69b4d326b9348c336edbe2a53eec0fd9fafd1e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550008"
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="041ca-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="041ca-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="041ca-104">Learn how to use C# to create a MapReduce solution on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="041ca-104">Learn how to use C# to create a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="041ca-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="041ca-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="041ca-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="041ca-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="041ca-107">Hadoop streaming is a utility that allows you to run MapReduce jobs using a script or executable.</span><span class="sxs-lookup"><span data-stu-id="041ca-107">Hadoop streaming is a utility that allows you to run MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="041ca-108">In this example, .NET is used to implement the mapper and reducer for a word count solution.</span><span class="sxs-lookup"><span data-stu-id="041ca-108">In this example, .NET is used to implement the mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="041ca-109">.NET on HDInsight</span><span class="sxs-lookup"><span data-stu-id="041ca-109">.NET on HDInsight</span></span>

<span data-ttu-id="041ca-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span><span class="sxs-lookup"><span data-stu-id="041ca-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="041ca-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span><span class="sxs-lookup"><span data-stu-id="041ca-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="041ca-112">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="041ca-112">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="041ca-113">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="041ca-113">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="041ca-114">How Hadoop streaming works</span><span class="sxs-lookup"><span data-stu-id="041ca-114">How Hadoop streaming works</span></span>

<span data-ttu-id="041ca-115">The basic process used for streaming in this document is as follows:</span><span class="sxs-lookup"><span data-stu-id="041ca-115">The basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="041ca-116">Hadoop passes data to the mapper (mapper.exe in this example) on STDIN.</span><span class="sxs-lookup"><span data-stu-id="041ca-116">Hadoop passes data to the mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="041ca-117">The mapper processes the data, and emits tab-delimited key/value pairs to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="041ca-117">The mapper processes the data, and emits tab-delimited key/value pairs to STDOUT.</span></span>
3. <span data-ttu-id="041ca-118">The output is read by Hadoop, and then passed to the reducer (reducer.exe in this example) on STDIN.</span><span class="sxs-lookup"><span data-stu-id="041ca-118">The output is read by Hadoop, and then passed to the reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="041ca-119">The reducer reads the tab-delimited key/value pairs, processes the data, and then emits the result as tab-delimited key/value pairs on STDOUT.</span><span class="sxs-lookup"><span data-stu-id="041ca-119">The reducer reads the tab-delimited key/value pairs, processes the data, and then emits the result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="041ca-120">The output is read by Hadoop and written to the output directory.</span><span class="sxs-lookup"><span data-stu-id="041ca-120">The output is read by Hadoop and written to the output directory.</span></span>

<span data-ttu-id="041ca-121">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="041ca-121">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="041ca-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="041ca-122">Prerequisites</span></span>

* <span data-ttu-id="041ca-123">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="041ca-123">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="041ca-124">The steps in this document use Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="041ca-124">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="041ca-125">A way to upload .exe files to the cluster.</span><span class="sxs-lookup"><span data-stu-id="041ca-125">A way to upload .exe files to the cluster.</span></span> <span data-ttu-id="041ca-126">The steps in this document use the Data Lake Tools for Visual Studio to upload the files to primary storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="041ca-126">The steps in this document use the Data Lake Tools for Visual Studio to upload the files to primary storage for the cluster.</span></span>

* <span data-ttu-id="041ca-127">Azure PowerShell or a SSH client.</span><span class="sxs-lookup"><span data-stu-id="041ca-127">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="041ca-128">A Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="041ca-128">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="041ca-129">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="041ca-129">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-the-mapper"></a><span data-ttu-id="041ca-130">Create the mapper</span><span class="sxs-lookup"><span data-stu-id="041ca-130">Create the mapper</span></span>

<span data-ttu-id="041ca-131">In Visual Studio, create a new __Console application__ named __mapper__.</span><span class="sxs-lookup"><span data-stu-id="041ca-131">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="041ca-132">Use the following code for the application:</span><span class="sxs-lookup"><span data-stu-id="041ca-132">Use the following code for the application:</span></span>

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data to the mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over the words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

<span data-ttu-id="041ca-133">After creating the application, build it to produce the `/bin/Debug/mapper.exe` file in the project directory.</span><span class="sxs-lookup"><span data-stu-id="041ca-133">After creating the application, build it to produce the `/bin/Debug/mapper.exe` file in the project directory.</span></span>

## <a name="create-the-reducer"></a><span data-ttu-id="041ca-134">Create the reducer</span><span class="sxs-lookup"><span data-stu-id="041ca-134">Create the reducer</span></span>

<span data-ttu-id="041ca-135">In Visual Studio, create a new __Console application__ named __reducer__.</span><span class="sxs-lookup"><span data-stu-id="041ca-135">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="041ca-136">Use the following code for the application:</span><span class="sxs-lookup"><span data-stu-id="041ca-136">Use the following code for the application:</span></span>

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get the word
                string word = sArr[0];
                // Get the count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for the word?
                if(words.ContainsKey(word))
                {
                    //If so, increment the count
                    words[word] += count;
                } else
                {
                    //Add the key to the collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

<span data-ttu-id="041ca-137">After creating the application, build it to produce the `/bin/Debug/reducer.exe` file in the project directory.</span><span class="sxs-lookup"><span data-stu-id="041ca-137">After creating the application, build it to produce the `/bin/Debug/reducer.exe` file in the project directory.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="041ca-138">Upload to storage</span><span class="sxs-lookup"><span data-stu-id="041ca-138">Upload to storage</span></span>

1. <span data-ttu-id="041ca-139">In Visual Studio, open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="041ca-139">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="041ca-140">Expand **Azure**, and then expand **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="041ca-140">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="041ca-141">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="041ca-141">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="041ca-142">Expand the HDInsight cluster that you wish to deploy this application to.</span><span class="sxs-lookup"><span data-stu-id="041ca-142">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="041ca-143">An entry with the text __(Default Storage Account)__ is listed.</span><span class="sxs-lookup"><span data-stu-id="041ca-143">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![Server Explorer showing the storage account for the cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="041ca-145">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="041ca-145">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="041ca-146">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span><span class="sxs-lookup"><span data-stu-id="041ca-146">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="041ca-147">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="041ca-147">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="041ca-148">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span><span class="sxs-lookup"><span data-stu-id="041ca-148">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="041ca-149">To upload the .exe files, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="041ca-149">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="041ca-150">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **mapper** project.</span><span class="sxs-lookup"><span data-stu-id="041ca-150">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **mapper** project.</span></span> <span data-ttu-id="041ca-151">Finally, select the **mapper.exe** file and click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="041ca-151">Finally, select the **mapper.exe** file and click **Ok**.</span></span>

        ![upload icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="041ca-153">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span><span class="sxs-lookup"><span data-stu-id="041ca-153">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="041ca-154">Finally, select the **mapper.exe** file and click **Open**.</span><span class="sxs-lookup"><span data-stu-id="041ca-154">Finally, select the **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="041ca-155">Once the __mapper.exe__ upload has finished, repeat the upload process for the __reducer.exe__ file.</span><span class="sxs-lookup"><span data-stu-id="041ca-155">Once the __mapper.exe__ upload has finished, repeat the upload process for the __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="041ca-156">Run a job: Using an SSH session</span><span class="sxs-lookup"><span data-stu-id="041ca-156">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="041ca-157">Use SSH to connect to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="041ca-157">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="041ca-158">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="041ca-158">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="041ca-159">Use one of the following command to start the MapReduce job:</span><span class="sxs-lookup"><span data-stu-id="041ca-159">Use one of the following command to start the MapReduce job:</span></span>

    * <span data-ttu-id="041ca-160">If using __Data Lake Store__ as default storage:</span><span class="sxs-lookup"><span data-stu-id="041ca-160">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="041ca-161">If using __Azure Storage__ as default storage:</span><span class="sxs-lookup"><span data-stu-id="041ca-161">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasbs:///mapper.exe,wasbs:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="041ca-162">The following list describes what each parameter does:</span><span class="sxs-lookup"><span data-stu-id="041ca-162">The following list describes what each parameter does:</span></span>

    * <span data-ttu-id="041ca-163">`hadoop-streaming.jar`: The jar file that contains the streaming MapReduce functionality.</span><span class="sxs-lookup"><span data-stu-id="041ca-163">`hadoop-streaming.jar`: The jar file that contains the streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="041ca-164">`-files`: Adds the `mapper.exe` and `reducer.exe` files to this job.</span><span class="sxs-lookup"><span data-stu-id="041ca-164">`-files`: Adds the `mapper.exe` and `reducer.exe` files to this job.</span></span> <span data-ttu-id="041ca-165">The `adl:///` or `wasb:///` before each file is the path to the root of default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="041ca-165">The `adl:///` or `wasb:///` before each file is the path to the root of default storage for the cluster.</span></span>
    * <span data-ttu-id="041ca-166">`-mapper`: Specifies which file implements the mapper.</span><span class="sxs-lookup"><span data-stu-id="041ca-166">`-mapper`: Specifies which file implements the mapper.</span></span>
    * <span data-ttu-id="041ca-167">`-reducer`: Specifies which file implements the reducer.</span><span class="sxs-lookup"><span data-stu-id="041ca-167">`-reducer`: Specifies which file implements the reducer.</span></span>
    * <span data-ttu-id="041ca-168">`-input`: The input data.</span><span class="sxs-lookup"><span data-stu-id="041ca-168">`-input`: The input data.</span></span>
    * <span data-ttu-id="041ca-169">`-output`: The output directory.</span><span class="sxs-lookup"><span data-stu-id="041ca-169">`-output`: The output directory.</span></span>

3. <span data-ttu-id="041ca-170">Once the MapReduce job completes, use the following to view the results:</span><span class="sxs-lookup"><span data-stu-id="041ca-170">Once the MapReduce job completes, use the following to view the results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="041ca-171">The following text is an example of the data returned by this command:</span><span class="sxs-lookup"><span data-stu-id="041ca-171">The following text is an example of the data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="041ca-172">Run a job: Using PowerShell</span><span class="sxs-lookup"><span data-stu-id="041ca-172">Run a job: Using PowerShell</span></span>

<span data-ttu-id="041ca-173">Use the following PowerShell script to run a MapReduce job and download the results.</span><span class="sxs-lookup"><span data-stu-id="041ca-173">Use the following PowerShell script to run a MapReduce job and download the results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="041ca-174">This script prompts you for the cluster login account name and password, along with the HDInsight cluster name.</span><span class="sxs-lookup"><span data-stu-id="041ca-174">This script prompts you for the cluster login account name and password, along with the HDInsight cluster name.</span></span> <span data-ttu-id="041ca-175">Once the job completes, the output is downloaded to the `output.txt` file in the directory the script is ran from.</span><span class="sxs-lookup"><span data-stu-id="041ca-175">Once the job completes, the output is downloaded to the `output.txt` file in the directory the script is ran from.</span></span> <span data-ttu-id="041ca-176">The following text is an example of the data in the `output.txt` file:</span><span class="sxs-lookup"><span data-stu-id="041ca-176">The following text is an example of the data in the `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="041ca-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="041ca-177">Next steps</span></span>

<span data-ttu-id="041ca-178">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="041ca-178">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="041ca-179">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="041ca-179">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="041ca-180">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="041ca-180">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

