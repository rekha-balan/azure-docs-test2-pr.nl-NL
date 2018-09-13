---
title: Use C# with Hive and Pig on Hadoop in HDInsight - Azure
description: Learn how to use C# user-defined functions (UDF) with Hive and Pig streaming in Azure HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/27/2018
ms.author: jasonh
ms.openlocfilehash: 9a214aa51bcd4b7aab7a65cf2989edd9e9dd3dc6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866124"
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="b05a7-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b05a7-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="b05a7-104">Learn how to use C# user-defined functions (UDF) with Apache Hive and Pig on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b05a7-104">Learn how to use C# user-defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b05a7-105">The steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="b05a7-105">The steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="b05a7-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="b05a7-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b05a7-107">For more information, see [HDInsight component versioning](../hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b05a7-107">For more information, see [HDInsight component versioning](../hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="b05a7-108">Both Hive and Pig can pass data to external applications for processing.</span><span class="sxs-lookup"><span data-stu-id="b05a7-108">Both Hive and Pig can pass data to external applications for processing.</span></span> <span data-ttu-id="b05a7-109">This process is known as _streaming_.</span><span class="sxs-lookup"><span data-stu-id="b05a7-109">This process is known as _streaming_.</span></span> <span data-ttu-id="b05a7-110">When using a .NET application, the data is passed to the application on STDIN, and the application returns the results on STDOUT.</span><span class="sxs-lookup"><span data-stu-id="b05a7-110">When using a .NET application, the data is passed to the application on STDIN, and the application returns the results on STDOUT.</span></span> <span data-ttu-id="b05a7-111">To read and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span><span class="sxs-lookup"><span data-stu-id="b05a7-111">To read and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b05a7-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b05a7-112">Prerequisites</span></span>

* <span data-ttu-id="b05a7-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="b05a7-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="b05a7-114">Use whatever IDE you want.</span><span class="sxs-lookup"><span data-stu-id="b05a7-114">Use whatever IDE you want.</span></span> <span data-ttu-id="b05a7-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="b05a7-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="b05a7-116">The steps in this document use Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b05a7-116">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="b05a7-117">A way to upload .exe files to the cluster and run Pig and Hive jobs.</span><span class="sxs-lookup"><span data-stu-id="b05a7-117">A way to upload .exe files to the cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="b05a7-118">We recommend the Data Lake Tools for Visual Studio, Azure PowerShell, and Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b05a7-118">We recommend the Data Lake Tools for Visual Studio, Azure PowerShell, and Azure CLI.</span></span> <span data-ttu-id="b05a7-119">The steps in this document use the Data Lake Tools for Visual Studio to upload the files and run the example Hive query.</span><span class="sxs-lookup"><span data-stu-id="b05a7-119">The steps in this document use the Data Lake Tools for Visual Studio to upload the files and run the example Hive query.</span></span>

    <span data-ttu-id="b05a7-120">For information on other ways to run Hive queries and Pig jobs, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="b05a7-120">For information on other ways to run Hive queries and Pig jobs, see the following documents:</span></span>

    * [<span data-ttu-id="b05a7-121">Use Apache Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="b05a7-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="b05a7-122">Use Apache Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="b05a7-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="b05a7-123">A Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b05a7-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="b05a7-124">For more information on creating a cluster, see [Create an HDInsight cluster](../hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b05a7-124">For more information on creating a cluster, see [Create an HDInsight cluster](../hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="b05a7-125">.NET on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b05a7-125">.NET on HDInsight</span></span>

* <span data-ttu-id="b05a7-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span><span class="sxs-lookup"><span data-stu-id="b05a7-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="b05a7-127">Mono version 4.2.1 is included with HDInsight version 3.6.</span><span class="sxs-lookup"><span data-stu-id="b05a7-127">Mono version 4.2.1 is included with HDInsight version 3.6.</span></span>

    <span data-ttu-id="b05a7-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="b05a7-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="b05a7-129">To use a specific version of Mono, see the [Install or update Mono](../hdinsight-hadoop-install-mono.md) document.</span><span class="sxs-lookup"><span data-stu-id="b05a7-129">To use a specific version of Mono, see the [Install or update Mono](../hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="b05a7-130">__Windows-based HDInsight__ clusters use the Microsoft .NET CLR to run .NET applications.</span><span class="sxs-lookup"><span data-stu-id="b05a7-130">__Windows-based HDInsight__ clusters use the Microsoft .NET CLR to run .NET applications.</span></span>

<span data-ttu-id="b05a7-131">For more information on the version of the .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](../hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b05a7-131">For more information on the version of the .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](../hdinsight-component-versioning.md).</span></span>

## <a name="create-the-c-projects"></a><span data-ttu-id="b05a7-132">Create the C\# projects</span><span class="sxs-lookup"><span data-stu-id="b05a7-132">Create the C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="b05a7-133">Hive UDF</span><span class="sxs-lookup"><span data-stu-id="b05a7-133">Hive UDF</span></span>

1. <span data-ttu-id="b05a7-134">Open Visual Studio and create a solution.</span><span class="sxs-lookup"><span data-stu-id="b05a7-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="b05a7-135">For the project type, select **Console App (.NET Framework)**, and name the new project **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-135">For the project type, select **Console App (.NET Framework)**, and name the new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b05a7-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b05a7-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b05a7-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="b05a7-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="b05a7-138">Replace the contents of **Program.cs** with the following code:</span><span class="sxs-lookup"><span data-stu-id="b05a7-138">Replace the contents of **Program.cs** with the following code:</span></span>

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse the string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data to stdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for the given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array to hex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. <span data-ttu-id="b05a7-139">Build the project.</span><span class="sxs-lookup"><span data-stu-id="b05a7-139">Build the project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="b05a7-140">Pig UDF</span><span class="sxs-lookup"><span data-stu-id="b05a7-140">Pig UDF</span></span>

1. <span data-ttu-id="b05a7-141">Open Visual Studio and create a solution.</span><span class="sxs-lookup"><span data-stu-id="b05a7-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="b05a7-142">For the project type, select **Console Application**, and name the new project **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-142">For the project type, select **Console Application**, and name the new project **PigUDF**.</span></span>

2. <span data-ttu-id="b05a7-143">Replace the contents of the **Program.cs** file with the following code:</span><span class="sxs-lookup"><span data-stu-id="b05a7-143">Replace the contents of the **Program.cs** file with the following code:</span></span>

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim the error info off the beginning and add a note to the end of the line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split the fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="b05a7-144">This code parses the lines sent from Pig and reformats lines that begin with `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="b05a7-144">This code parses the lines sent from Pig and reformats lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="b05a7-145">Save **Program.cs**, and then build the project.</span><span class="sxs-lookup"><span data-stu-id="b05a7-145">Save **Program.cs**, and then build the project.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="b05a7-146">Upload to storage</span><span class="sxs-lookup"><span data-stu-id="b05a7-146">Upload to storage</span></span>

1. <span data-ttu-id="b05a7-147">In Visual Studio, open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="b05a7-148">Expand **Azure**, and then expand **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="b05a7-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="b05a7-150">Expand the HDInsight cluster that you wish to deploy this application to.</span><span class="sxs-lookup"><span data-stu-id="b05a7-150">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="b05a7-151">An entry with the text __(Default Storage Account)__ is listed.</span><span class="sxs-lookup"><span data-stu-id="b05a7-151">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![Server Explorer showing the storage account for the cluster](./media/apache-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="b05a7-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b05a7-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="b05a7-154">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span><span class="sxs-lookup"><span data-stu-id="b05a7-154">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="b05a7-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b05a7-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="b05a7-156">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span><span class="sxs-lookup"><span data-stu-id="b05a7-156">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="b05a7-157">To upload the .exe files, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="b05a7-157">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="b05a7-158">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **HiveCSharp** project.</span><span class="sxs-lookup"><span data-stu-id="b05a7-158">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **HiveCSharp** project.</span></span> <span data-ttu-id="b05a7-159">Finally, select the **HiveCSharp.exe** file and click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-159">Finally, select the **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![upload icon](./media/apache-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="b05a7-161">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span><span class="sxs-lookup"><span data-stu-id="b05a7-161">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="b05a7-162">Finally, select the **HiveCSharp.exe** file and click **Open**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-162">Finally, select the **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="b05a7-163">Once the __HiveCSharp.exe__ upload has finished, repeat the upload process for the __PigUDF.exe__ file.</span><span class="sxs-lookup"><span data-stu-id="b05a7-163">Once the __HiveCSharp.exe__ upload has finished, repeat the upload process for the __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="b05a7-164">Run a Hive query</span><span class="sxs-lookup"><span data-stu-id="b05a7-164">Run a Hive query</span></span>

1. <span data-ttu-id="b05a7-165">In Visual Studio, open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="b05a7-166">Expand **Azure**, and then expand **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="b05a7-167">Right-click the cluster that you deployed the **HiveCSharp** application to, and then select **Write a Hive Query**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-167">Right-click the cluster that you deployed the **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="b05a7-168">Use the following text for the Hive query:</span><span class="sxs-lookup"><span data-stu-id="b05a7-168">Use the following text for the Hive query:</span></span>

    ```hiveql
    -- Uncomment the following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment the following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b05a7-169">Uncomment the `add file` statement that matches the type of default storage used for your cluster.</span><span class="sxs-lookup"><span data-stu-id="b05a7-169">Uncomment the `add file` statement that matches the type of default storage used for your cluster.</span></span>

    <span data-ttu-id="b05a7-170">This query selects the `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes the fields to the HiveCSharp.exe application.</span><span class="sxs-lookup"><span data-stu-id="b05a7-170">This query selects the `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes the fields to the HiveCSharp.exe application.</span></span> <span data-ttu-id="b05a7-171">The query expects the application to return three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="b05a7-171">The query expects the application to return three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="b05a7-172">The query also expects to find HiveCSharp.exe in the root of the default storage container.</span><span class="sxs-lookup"><span data-stu-id="b05a7-172">The query also expects to find HiveCSharp.exe in the root of the default storage container.</span></span>

5. <span data-ttu-id="b05a7-173">Click **Submit** to submit the job to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b05a7-173">Click **Submit** to submit the job to the HDInsight cluster.</span></span> <span data-ttu-id="b05a7-174">The **Hive Job Summary** window opens.</span><span class="sxs-lookup"><span data-stu-id="b05a7-174">The **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="b05a7-175">Click **Refresh** to refresh the summary until **Job Status** changes to **Completed**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-175">Click **Refresh** to refresh the summary until **Job Status** changes to **Completed**.</span></span> <span data-ttu-id="b05a7-176">To view the job output, click **Job Output**.</span><span class="sxs-lookup"><span data-stu-id="b05a7-176">To view the job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="b05a7-177">Run a Pig job</span><span class="sxs-lookup"><span data-stu-id="b05a7-177">Run a Pig job</span></span>

1. <span data-ttu-id="b05a7-178">Use one of the following methods to connect to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="b05a7-178">Use one of the following methods to connect to your HDInsight cluster:</span></span>

    * <span data-ttu-id="b05a7-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span><span class="sxs-lookup"><span data-stu-id="b05a7-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="b05a7-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="b05a7-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="b05a7-181">For more information, see [Use SSH withHDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="b05a7-181">For more information, see [Use SSH withHDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="b05a7-182">If you are using a __Windows-based__ HDInsight cluster, [Connect to the cluster using Remote Desktop](../hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="b05a7-182">If you are using a __Windows-based__ HDInsight cluster, [Connect to the cluster using Remote Desktop](../hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="b05a7-183">Use one the following command to start the Pig command line:</span><span class="sxs-lookup"><span data-stu-id="b05a7-183">Use one the following command to start the Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="b05a7-184">If you are using a Windows-based cluster, use the following commands instead:</span><span class="sxs-lookup"><span data-stu-id="b05a7-184">If you are using a Windows-based cluster, use the following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="b05a7-185">A `grunt>` prompt is displayed.</span><span class="sxs-lookup"><span data-stu-id="b05a7-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="b05a7-186">Enter the following to run a Pig job that uses the .NET Framework application:</span><span class="sxs-lookup"><span data-stu-id="b05a7-186">Enter the following to run a Pig job that uses the .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="b05a7-187">The `DEFINE` statement creates an alias of `streamer` for the pigudf.exe applications, and `CACHE` loads it from default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b05a7-187">The `DEFINE` statement creates an alias of `streamer` for the pigudf.exe applications, and `CACHE` loads it from default storage for the cluster.</span></span> <span data-ttu-id="b05a7-188">Later, `streamer` is used with the `STREAM` operator to process the single lines contained in LOG and return the data as a series of columns.</span><span class="sxs-lookup"><span data-stu-id="b05a7-188">Later, `streamer` is used with the `STREAM` operator to process the single lines contained in LOG and return the data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b05a7-189">The application name that is used for streaming must be surrounded by the \` (backtick) character when aliased, and ' (single quote) when used with `SHIP`.</span><span class="sxs-lookup"><span data-stu-id="b05a7-189">The application name that is used for streaming must be surrounded by the \` (backtick) character when aliased, and ' (single quote) when used with `SHIP`.</span></span>

4. <span data-ttu-id="b05a7-190">After entering the last line, the job should start.</span><span class="sxs-lookup"><span data-stu-id="b05a7-190">After entering the last line, the job should start.</span></span> <span data-ttu-id="b05a7-191">It returns output similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="b05a7-191">It returns output similar to the following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="b05a7-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="b05a7-192">Next steps</span></span>

<span data-ttu-id="b05a7-193">In this document, you have learned how to use a .NET Framework application from Hive and Pig on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b05a7-193">In this document, you have learned how to use a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="b05a7-194">If you would like to learn how to use Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](python-udf-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="b05a7-194">If you would like to learn how to use Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](python-udf-hdinsight.md).</span></span>

<span data-ttu-id="b05a7-195">For other ways to use Pig and Hive, and to learn about using MapReduce, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="b05a7-195">For other ways to use Pig and Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="b05a7-196">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="b05a7-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b05a7-197">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="b05a7-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b05a7-198">Use MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="b05a7-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
