---
title: Use Python with Hive and Pig in HDInsight | Microsoft Docs
description: Learn how to use Python User Defined Functions (UDF) from Hive and Pig in HDInsight, the Hadoop technology stack on Azure.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/27/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 1fc13142d3e4f54e0945032a404eb497746ee5a0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670989"
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="68fb8-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="68fb8-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="68fb8-104">Hive and Pig are great for working with data in HDInsight, but sometimes you need a more general-purpose language.</span><span class="sxs-lookup"><span data-stu-id="68fb8-104">Hive and Pig are great for working with data in HDInsight, but sometimes you need a more general-purpose language.</span></span> <span data-ttu-id="68fb8-105">Both Hive and Pig allow you to create User Defined Functions (UDF) using many programming languages.</span><span class="sxs-lookup"><span data-stu-id="68fb8-105">Both Hive and Pig allow you to create User Defined Functions (UDF) using many programming languages.</span></span> <span data-ttu-id="68fb8-106">In this article, you learn how to use a Python UDF from Hive and Pig.</span><span class="sxs-lookup"><span data-stu-id="68fb8-106">In this article, you learn how to use a Python UDF from Hive and Pig.</span></span>

## <a name="requirements"></a><span data-ttu-id="68fb8-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="68fb8-107">Requirements</span></span>

* <span data-ttu-id="68fb8-108">An HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="68fb8-108">An HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="68fb8-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="68fb8-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="68fb8-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="68fb8-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="68fb8-111">A text editor</span><span class="sxs-lookup"><span data-stu-id="68fb8-111">A text editor</span></span>

## <a name="python"></a><span data-ttu-id="68fb8-112">Python on HDInsight</span><span class="sxs-lookup"><span data-stu-id="68fb8-112">Python on HDInsight</span></span>

<span data-ttu-id="68fb8-113">Python2.7 is installed by default on HDInsight 3.0 and later clusters.</span><span class="sxs-lookup"><span data-stu-id="68fb8-113">Python2.7 is installed by default on HDInsight 3.0 and later clusters.</span></span> <span data-ttu-id="68fb8-114">Hive can be used with this version of Python for stream processing (data is passed between Hive and Python using STDOUT/STDIN).</span><span class="sxs-lookup"><span data-stu-id="68fb8-114">Hive can be used with this version of Python for stream processing (data is passed between Hive and Python using STDOUT/STDIN).</span></span>

<span data-ttu-id="68fb8-115">HDInsight also includes Jython, which is a Python implementation written in Java.</span><span class="sxs-lookup"><span data-stu-id="68fb8-115">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="68fb8-116">Pig understands how to talk to Jython without having to resort to streaming, so it's preferable when using Pig.</span><span class="sxs-lookup"><span data-stu-id="68fb8-116">Pig understands how to talk to Jython without having to resort to streaming, so it's preferable when using Pig.</span></span> <span data-ttu-id="68fb8-117">You can also use normal Python (C Python,) with Pig.</span><span class="sxs-lookup"><span data-stu-id="68fb8-117">You can also use normal Python (C Python,) with Pig.</span></span>

## <a name="hivepython"></a><span data-ttu-id="68fb8-118">Hive and Python</span><span class="sxs-lookup"><span data-stu-id="68fb8-118">Hive and Python</span></span>

<span data-ttu-id="68fb8-119">Python can be used as a UDF from Hive through the HiveQL **TRANSFORM** statement.</span><span class="sxs-lookup"><span data-stu-id="68fb8-119">Python can be used as a UDF from Hive through the HiveQL **TRANSFORM** statement.</span></span> <span data-ttu-id="68fb8-120">For example, the following HiveQL invokes a Python script stored in the **streaming.py** file.</span><span class="sxs-lookup"><span data-stu-id="68fb8-120">For example, the following HiveQL invokes a Python script stored in the **streaming.py** file.</span></span>

<span data-ttu-id="68fb8-121">**Linux-based HDInsight**</span><span class="sxs-lookup"><span data-stu-id="68fb8-121">**Linux-based HDInsight**</span></span>

```hiveql
add file wasbs:///streaming.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python streaming.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="68fb8-122">**Windows-based HDInsight**</span><span class="sxs-lookup"><span data-stu-id="68fb8-122">**Windows-based HDInsight**</span></span>

```hiveql
add file wasbs:///streaming.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe streaming.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="68fb8-123">On Windows-based HDInsight clusters, the **USING** clause must specify the full path to python.exe.</span><span class="sxs-lookup"><span data-stu-id="68fb8-123">On Windows-based HDInsight clusters, the **USING** clause must specify the full path to python.exe.</span></span>

<span data-ttu-id="68fb8-124">Here's what this example does:</span><span class="sxs-lookup"><span data-stu-id="68fb8-124">Here's what this example does:</span></span>

1. <span data-ttu-id="68fb8-125">The **add file** statement at the beginning of the file adds the **streaming.py** file to the distributed cache, so it's accessible by all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="68fb8-125">The **add file** statement at the beginning of the file adds the **streaming.py** file to the distributed cache, so it's accessible by all nodes in the cluster.</span></span>
2. <span data-ttu-id="68fb8-126">The **SELECT TRANSFORM ... USING** statement selects data from the **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="68fb8-126">The **SELECT TRANSFORM ... USING** statement selects data from the **hivesampletable**.</span></span> <span data-ttu-id="68fb8-127">It also passes the clientid, devicemake, and devicemodel values to the **streaming.py** script.</span><span class="sxs-lookup"><span data-stu-id="68fb8-127">It also passes the clientid, devicemake, and devicemodel values to the **streaming.py** script.</span></span>
3. <span data-ttu-id="68fb8-128">The **AS** clause describes the fields returned from **streaming.py**</span><span class="sxs-lookup"><span data-stu-id="68fb8-128">The **AS** clause describes the fields returned from **streaming.py**</span></span>

<a name="streamingpy"></a> <span data-ttu-id="68fb8-129">Here's the **streaming.py** file used by the HiveQL example.</span><span class="sxs-lookup"><span data-stu-id="68fb8-129">Here's the **streaming.py** file used by the HiveQL example.</span></span>

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

<span data-ttu-id="68fb8-130">This script performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="68fb8-130">This script performs the following actions:</span></span>

1. <span data-ttu-id="68fb8-131">Read a line of data from STDIN.</span><span class="sxs-lookup"><span data-stu-id="68fb8-131">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="68fb8-132">The trailing newline character is removed using `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="68fb8-132">The trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="68fb8-133">When doing stream processing, a single line contains all the values with a tab character between each value.</span><span class="sxs-lookup"><span data-stu-id="68fb8-133">When doing stream processing, a single line contains all the values with a tab character between each value.</span></span> <span data-ttu-id="68fb8-134">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span><span class="sxs-lookup"><span data-stu-id="68fb8-134">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span></span>
4. <span data-ttu-id="68fb8-135">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span><span class="sxs-lookup"><span data-stu-id="68fb8-135">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="68fb8-136">This is accomplished by using `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="68fb8-136">This is accomplished by using `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="68fb8-137">The `while` loop repeats until no `line` is read.</span><span class="sxs-lookup"><span data-stu-id="68fb8-137">The `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="68fb8-138">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span><span class="sxs-lookup"><span data-stu-id="68fb8-138">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span></span>

<span data-ttu-id="68fb8-139">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="68fb8-139">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span></span>

## <a name="pigpython"></a><span data-ttu-id="68fb8-140">Pig and Python</span><span class="sxs-lookup"><span data-stu-id="68fb8-140">Pig and Python</span></span>

<span data-ttu-id="68fb8-141">A Python script can be used as a UDF from Pig through the **GENERATE** statement.</span><span class="sxs-lookup"><span data-stu-id="68fb8-141">A Python script can be used as a UDF from Pig through the **GENERATE** statement.</span></span> <span data-ttu-id="68fb8-142">You can run the script using either Jython or C Python.</span><span class="sxs-lookup"><span data-stu-id="68fb8-142">You can run the script using either Jython or C Python.</span></span>

<span data-ttu-id="68fb8-143">The difference between these are that Jython runs on the JVM and can natively be called from Pig.</span><span class="sxs-lookup"><span data-stu-id="68fb8-143">The difference between these are that Jython runs on the JVM and can natively be called from Pig.</span></span> <span data-ttu-id="68fb8-144">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span><span class="sxs-lookup"><span data-stu-id="68fb8-144">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span></span> <span data-ttu-id="68fb8-145">The output of the Python script is sent back into Pig.</span><span class="sxs-lookup"><span data-stu-id="68fb8-145">The output of the Python script is sent back into Pig.</span></span>

<span data-ttu-id="68fb8-146">To determine whether Pig uses Jython or C Python to run the script, use **register** when referencing the Python script from Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="68fb8-146">To determine whether Pig uses Jython or C Python to run the script, use **register** when referencing the Python script from Pig Latin.</span></span> <span data-ttu-id="68fb8-147">The following examples register scripts with Pig as **myfuncs**:</span><span class="sxs-lookup"><span data-stu-id="68fb8-147">The following examples register scripts with Pig as **myfuncs**:</span></span>

* <span data-ttu-id="68fb8-148">**To use Jython**: `register '/path/to/pig_python.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="68fb8-148">**To use Jython**: `register '/path/to/pig_python.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="68fb8-149">**To use C Python**: `register '/path/to/pig_python.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="68fb8-149">**To use C Python**: `register '/path/to/pig_python.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68fb8-150">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span><span class="sxs-lookup"><span data-stu-id="68fb8-150">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="68fb8-151">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span><span class="sxs-lookup"><span data-stu-id="68fb8-151">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span></span>

<span data-ttu-id="68fb8-152">Once past registration, the Pig Latin for this example is the same for both:</span><span class="sxs-lookup"><span data-stu-id="68fb8-152">Once past registration, the Pig Latin for this example is the same for both:</span></span>

```pig
LOGS = LOAD 'wasbs:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="68fb8-153">Here's what this example does:</span><span class="sxs-lookup"><span data-stu-id="68fb8-153">Here's what this example does:</span></span>

1. <span data-ttu-id="68fb8-154">The first line loads the sample data file, **sample.log** into **LOGS**.</span><span class="sxs-lookup"><span data-stu-id="68fb8-154">The first line loads the sample data file, **sample.log** into **LOGS**.</span></span> <span data-ttu-id="68fb8-155">It also defines each record as a **chararray**.</span><span class="sxs-lookup"><span data-stu-id="68fb8-155">It also defines each record as a **chararray**.</span></span>
2. <span data-ttu-id="68fb8-156">The next line filters out any null values, storing the result of the operation into **LOG**.</span><span class="sxs-lookup"><span data-stu-id="68fb8-156">The next line filters out any null values, storing the result of the operation into **LOG**.</span></span>
3. <span data-ttu-id="68fb8-157">Next, it iterates over the records in **LOG** and uses **GENERATE** to invoke the **create_structure** method contained in the Python/Jython script loaded as **myfuncs**.</span><span class="sxs-lookup"><span data-stu-id="68fb8-157">Next, it iterates over the records in **LOG** and uses **GENERATE** to invoke the **create_structure** method contained in the Python/Jython script loaded as **myfuncs**.</span></span>  <span data-ttu-id="68fb8-158">**LINE** is used to pass the current record to the function.</span><span class="sxs-lookup"><span data-stu-id="68fb8-158">**LINE** is used to pass the current record to the function.</span></span>
4. <span data-ttu-id="68fb8-159">Finally, the outputs are dumped to STDOUT using the **DUMP** command.</span><span class="sxs-lookup"><span data-stu-id="68fb8-159">Finally, the outputs are dumped to STDOUT using the **DUMP** command.</span></span> <span data-ttu-id="68fb8-160">This displays the results after the operation completes.</span><span class="sxs-lookup"><span data-stu-id="68fb8-160">This displays the results after the operation completes.</span></span>

<span data-ttu-id="68fb8-161">The Python script file is similar between C Python and Jython, the only difference being that you must import from **pig\_util** when using C Python.</span><span class="sxs-lookup"><span data-stu-id="68fb8-161">The Python script file is similar between C Python and Jython, the only difference being that you must import from **pig\_util** when using C Python.</span></span> <span data-ttu-id="68fb8-162">Here is the **pig\_python.py** script:</span><span class="sxs-lookup"><span data-stu-id="68fb8-162">Here is the **pig\_python.py** script:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment the following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

> [!NOTE]
> <span data-ttu-id="68fb8-163">'pig_util' isn't something you need to worry about installing; it's automatically available to the script.</span><span class="sxs-lookup"><span data-stu-id="68fb8-163">'pig_util' isn't something you need to worry about installing; it's automatically available to the script.</span></span>

<span data-ttu-id="68fb8-164">Remember that we previously defined the **LINE** input as a chararray because there was no consistent schema for the input.</span><span class="sxs-lookup"><span data-stu-id="68fb8-164">Remember that we previously defined the **LINE** input as a chararray because there was no consistent schema for the input.</span></span> <span data-ttu-id="68fb8-165">The Python script transforms the data into a consistent schema for output.</span><span class="sxs-lookup"><span data-stu-id="68fb8-165">The Python script transforms the data into a consistent schema for output.</span></span>

1. <span data-ttu-id="68fb8-166">The **@outputSchema** statement defines the format of the data that is returned to Pig.</span><span class="sxs-lookup"><span data-stu-id="68fb8-166">The **@outputSchema** statement defines the format of the data that is returned to Pig.</span></span> <span data-ttu-id="68fb8-167">In this case, it's a **data bag**, which is a Pig data type.</span><span class="sxs-lookup"><span data-stu-id="68fb8-167">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="68fb8-168">The bag contains the following fields, all of which are chararray (strings):</span><span class="sxs-lookup"><span data-stu-id="68fb8-168">The bag contains the following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="68fb8-169">date - the date the log entry was created</span><span class="sxs-lookup"><span data-stu-id="68fb8-169">date - the date the log entry was created</span></span>
   * <span data-ttu-id="68fb8-170">time - the time the log entry was created</span><span class="sxs-lookup"><span data-stu-id="68fb8-170">time - the time the log entry was created</span></span>
   * <span data-ttu-id="68fb8-171">classname - the class name the entry was created for</span><span class="sxs-lookup"><span data-stu-id="68fb8-171">classname - the class name the entry was created for</span></span>
   * <span data-ttu-id="68fb8-172">level - the log level</span><span class="sxs-lookup"><span data-stu-id="68fb8-172">level - the log level</span></span>
   * <span data-ttu-id="68fb8-173">detail - verbose details for the log entry</span><span class="sxs-lookup"><span data-stu-id="68fb8-173">detail - verbose details for the log entry</span></span>

2. <span data-ttu-id="68fb8-174">Next, the **def create_structure(input)** defines the function that Pig passes line items to.</span><span class="sxs-lookup"><span data-stu-id="68fb8-174">Next, the **def create_structure(input)** defines the function that Pig passes line items to.</span></span>

3. <span data-ttu-id="68fb8-175">The example data, **sample.log**, mostly conforms to the date, time, classname, level, and detail schema we want to return.</span><span class="sxs-lookup"><span data-stu-id="68fb8-175">The example data, **sample.log**, mostly conforms to the date, time, classname, level, and detail schema we want to return.</span></span> <span data-ttu-id="68fb8-176">But it also contains a few lines that begin with the string '*java.lang.Exception*' that need to be modified to match the schema.</span><span class="sxs-lookup"><span data-stu-id="68fb8-176">But it also contains a few lines that begin with the string '*java.lang.Exception*' that need to be modified to match the schema.</span></span> <span data-ttu-id="68fb8-177">The **if** statement checks for those, then massages the input data to move the '*java.lang.Exception*' string to the end, bringing the data in-line with our expected output schema.</span><span class="sxs-lookup"><span data-stu-id="68fb8-177">The **if** statement checks for those, then massages the input data to move the '*java.lang.Exception*' string to the end, bringing the data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="68fb8-178">Next, the **split** command is used to split the data at the first four space characters.</span><span class="sxs-lookup"><span data-stu-id="68fb8-178">Next, the **split** command is used to split the data at the first four space characters.</span></span> <span data-ttu-id="68fb8-179">The output is assigned into **date**, **time**, **classname**, **level**, and **detail**.</span><span class="sxs-lookup"><span data-stu-id="68fb8-179">The output is assigned into **date**, **time**, **classname**, **level**, and **detail**.</span></span>

5. <span data-ttu-id="68fb8-180">Finally, the values are returned to Pig.</span><span class="sxs-lookup"><span data-stu-id="68fb8-180">Finally, the values are returned to Pig.</span></span>

<span data-ttu-id="68fb8-181">When the data is returned to Pig, it has a consistent schema as defined in the **@outputSchema** statement.</span><span class="sxs-lookup"><span data-stu-id="68fb8-181">When the data is returned to Pig, it has a consistent schema as defined in the **@outputSchema** statement.</span></span>

## <a name="running"></a><span data-ttu-id="68fb8-182">Running the examples</span><span class="sxs-lookup"><span data-stu-id="68fb8-182">Running the examples</span></span>
<span data-ttu-id="68fb8-183">If you are using a Linux-based HDInsight cluster, use the **SSH** steps.</span><span class="sxs-lookup"><span data-stu-id="68fb8-183">If you are using a Linux-based HDInsight cluster, use the **SSH** steps.</span></span> <span data-ttu-id="68fb8-184">If you are using a Windows-based HDInsight cluster and a Windows client, use the **PowerShell** steps.</span><span class="sxs-lookup"><span data-stu-id="68fb8-184">If you are using a Windows-based HDInsight cluster and a Windows client, use the **PowerShell** steps.</span></span>

### <a name="ssh"></a><span data-ttu-id="68fb8-185">SSH</span><span class="sxs-lookup"><span data-stu-id="68fb8-185">SSH</span></span>

<span data-ttu-id="68fb8-186">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="68fb8-186">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="68fb8-187">Using the Python examples [streaming.py](#streamingpy) and [pig_python.py](#jythonpy), create local copies of the files on your development machine.</span><span class="sxs-lookup"><span data-stu-id="68fb8-187">Using the Python examples [streaming.py](#streamingpy) and [pig_python.py](#jythonpy), create local copies of the files on your development machine.</span></span>

2. <span data-ttu-id="68fb8-188">Use `scp` to copy the files to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="68fb8-188">Use `scp` to copy the files to your HDInsight cluster.</span></span> <span data-ttu-id="68fb8-189">For example, the following command copies the files to a cluster named **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="68fb8-189">For example, the following command copies the files to a cluster named **mycluster**.</span></span>

        scp streaming.py pig_python.py myuser@mycluster-ssh.azurehdinsight.net:

3. <span data-ttu-id="68fb8-190">Use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="68fb8-190">Use SSH to connect to the cluster.</span></span> <span data-ttu-id="68fb8-191">For example, the following would connect to a cluster named **mycluster** as user **myuser**.</span><span class="sxs-lookup"><span data-stu-id="68fb8-191">For example, the following would connect to a cluster named **mycluster** as user **myuser**.</span></span>

        ssh myuser@mycluster-ssh.azurehdinsight.net
4. <span data-ttu-id="68fb8-192">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="68fb8-192">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span></span>

        hdfs dfs -put streaming.py /streaming.py
        hdfs dfs -put pig_python.py /pig_python.py

<span data-ttu-id="68fb8-193">After uploading the files, use the following steps to run the Hive and Pig jobs.</span><span class="sxs-lookup"><span data-stu-id="68fb8-193">After uploading the files, use the following steps to run the Hive and Pig jobs.</span></span>

#### <a name="hive"></a><span data-ttu-id="68fb8-194">Hive</span><span class="sxs-lookup"><span data-stu-id="68fb8-194">Hive</span></span>

1. <span data-ttu-id="68fb8-195">Use the `hive` command to start the hive shell.</span><span class="sxs-lookup"><span data-stu-id="68fb8-195">Use the `hive` command to start the hive shell.</span></span> <span data-ttu-id="68fb8-196">You should see a `hive>` prompt once the shell has loaded.</span><span class="sxs-lookup"><span data-stu-id="68fb8-196">You should see a `hive>` prompt once the shell has loaded.</span></span>
2. <span data-ttu-id="68fb8-197">Enter the following at the `hive>` prompt.</span><span class="sxs-lookup"><span data-stu-id="68fb8-197">Enter the following at the `hive>` prompt.</span></span>

   ```hive
   add file wasbs:///streaming.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python streaming.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```
3. <span data-ttu-id="68fb8-198">After entering the last line, the job should start.</span><span class="sxs-lookup"><span data-stu-id="68fb8-198">After entering the last line, the job should start.</span></span> <span data-ttu-id="68fb8-199">Once the job completes, it returns output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="68fb8-199">Once the job completes, it returns output similar to the following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig"></a><span data-ttu-id="68fb8-200">Pig</span><span class="sxs-lookup"><span data-stu-id="68fb8-200">Pig</span></span>

1. <span data-ttu-id="68fb8-201">Use the `pig` command to start the shell.</span><span class="sxs-lookup"><span data-stu-id="68fb8-201">Use the `pig` command to start the shell.</span></span> <span data-ttu-id="68fb8-202">You should see a `grunt>` prompt once the shell has loaded.</span><span class="sxs-lookup"><span data-stu-id="68fb8-202">You should see a `grunt>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="68fb8-203">Enter the following statements at the `grunt>` prompt:</span><span class="sxs-lookup"><span data-stu-id="68fb8-203">Enter the following statements at the `grunt>` prompt:</span></span>

   ```pig
   Register wasbs:///pig_python.py using jython as myfuncs;
   LOGS = LOAD 'wasbs:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="68fb8-204">After entering the following line, the job should start.</span><span class="sxs-lookup"><span data-stu-id="68fb8-204">After entering the following line, the job should start.</span></span> <span data-ttu-id="68fb8-205">Once the job completes, it returns output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="68fb8-205">Once the job completes, it returns output similar to the following.</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="68fb8-206">Use `quit` to exit the Grunt shell, and then use the following to edit the pig_python.py file on the local file system:</span><span class="sxs-lookup"><span data-stu-id="68fb8-206">Use `quit` to exit the Grunt shell, and then use the following to edit the pig_python.py file on the local file system:</span></span>

    <span data-ttu-id="68fb8-207">nano pig_python.py</span><span class="sxs-lookup"><span data-stu-id="68fb8-207">nano pig_python.py</span></span>

5. <span data-ttu-id="68fb8-208">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span><span class="sxs-lookup"><span data-stu-id="68fb8-208">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span></span>

        #from pig_util import outputSchema

    <span data-ttu-id="68fb8-209">Once the change has been made, use Ctrl+X to exit the editor.</span><span class="sxs-lookup"><span data-stu-id="68fb8-209">Once the change has been made, use Ctrl+X to exit the editor.</span></span> <span data-ttu-id="68fb8-210">Select Y, and then enter to save the changes.</span><span class="sxs-lookup"><span data-stu-id="68fb8-210">Select Y, and then enter to save the changes.</span></span>

6. <span data-ttu-id="68fb8-211">Use the `pig` command to start the shell again.</span><span class="sxs-lookup"><span data-stu-id="68fb8-211">Use the `pig` command to start the shell again.</span></span> <span data-ttu-id="68fb8-212">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span><span class="sxs-lookup"><span data-stu-id="68fb8-212">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span></span>

   ```pig
   Register 'pig_python.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasbs:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="68fb8-213">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span><span class="sxs-lookup"><span data-stu-id="68fb8-213">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span></span>

### <a name="powershell"></a><span data-ttu-id="68fb8-214">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68fb8-214">PowerShell</span></span>

<span data-ttu-id="68fb8-215">These steps use Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68fb8-215">These steps use Azure PowerShell.</span></span> <span data-ttu-id="68fb8-216">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="68fb8-216">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

1. <span data-ttu-id="68fb8-217">Using the Python examples [streaming.py](#streamingpy) and [pig_python.py](#jythonpy), create local copies of the files on your development machine.</span><span class="sxs-lookup"><span data-stu-id="68fb8-217">Using the Python examples [streaming.py](#streamingpy) and [pig_python.py](#jythonpy), create local copies of the files on your development machine.</span></span>
2. <span data-ttu-id="68fb8-218">Use  the following PowerShell script to upload the **streaming.py** and **pig\_python.py** files to the server.</span><span class="sxs-lookup"><span data-stu-id="68fb8-218">Use  the following PowerShell script to upload the **streaming.py** and **pig\_python.py** files to the server.</span></span> <span data-ttu-id="68fb8-219">Substitute the name of your Azure HDInsight cluster, and the path to the **streaming.py** and **pig\_python.py** files on the first three lines of the script.</span><span class="sxs-lookup"><span data-stu-id="68fb8-219">Substitute the name of your Azure HDInsight cluster, and the path to the **streaming.py** and **pig\_python.py** files on the first three lines of the script.</span></span>

   ```powershell
    # Login to your Azure subscription
    # Is there an active Azure subscription?
    $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
    if(-not($sub))
    {
        Add-AzureRmAccount
    }

    # Get cluster info
    $clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
    $pathToStreamingFile = "C:\path\to\streaming.py"
    $pathToJythonFile = "C:\path\to\pig_python.py"

    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroup = $clusterInfo.ResourceGroup
    $storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
    $container=$clusterInfo.DefaultStorageContainer
    $storageAccountKey=(Get-AzureRmStorageAccountKey `
        -Name $storageAccountName `
    -ResourceGroupName $resourceGroup)[0].Value

    #Create a storage content and upload the file
    $context = New-AzureStorageContext `
        -StorageAccountName $storageAccountName `
        -StorageAccountKey $storageAccountKey

    Set-AzureStorageBlobContent `
        -File $pathToStreamingFile `
        -Blob "streaming.py" `
        -Container $container `
        -Context $context

    Set-AzureStorageBlobContent `
        -File $pathToJythonFile `
        -Blob "pig_python.py" `
        -Container $container `
        -Context $context
   ```

    <span data-ttu-id="68fb8-220">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span><span class="sxs-lookup"><span data-stu-id="68fb8-220">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span></span>

   > [!NOTE]
   > <span data-ttu-id="68fb8-221">Other methods of uploading the scripts can be found in the [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span><span class="sxs-lookup"><span data-stu-id="68fb8-221">Other methods of uploading the scripts can be found in the [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

<span data-ttu-id="68fb8-222">After uploading the files, use the following PowerShell scripts to start the jobs.</span><span class="sxs-lookup"><span data-stu-id="68fb8-222">After uploading the files, use the following PowerShell scripts to start the jobs.</span></span> <span data-ttu-id="68fb8-223">When the job completes, the output should be written to the PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="68fb8-223">When the job completes, the output should be written to the PowerShell console.</span></span>

#### <a name="hive"></a><span data-ttu-id="68fb8-224">Hive</span><span class="sxs-lookup"><span data-stu-id="68fb8-224">Hive</span></span>

<span data-ttu-id="68fb8-225">The following script runs the **streaming.py** script.</span><span class="sxs-lookup"><span data-stu-id="68fb8-225">The following script runs the **streaming.py** script.</span></span> <span data-ttu-id="68fb8-226">Before running, it prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="68fb8-226">Before running, it prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

# If using a Windows-based HDInsight cluster, change the USING statement to:
# "USING 'D:\Python27\python.exe streaming.py' AS " +
$HiveQuery = "add file wasbs:///streaming.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python streaming.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for the Hive job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="68fb8-227">The output for the **Hive** job should appear similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="68fb8-227">The output for the **Hive** job should appear similar to the following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="68fb8-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="68fb8-228">Pig (Jython)</span></span>

<span data-ttu-id="68fb8-229">The following script uses the **pig_python.py** script, using the Jython interpreter.</span><span class="sxs-lookup"><span data-stu-id="68fb8-229">The following script uses the **pig_python.py** script, using the Jython interpreter.</span></span> <span data-ttu-id="68fb8-230">Before running, it prompts you for the HTTPs/Admin information for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="68fb8-230">Before running, it prompts you for the HTTPs/Admin information for the HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="68fb8-231">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span><span class="sxs-lookup"><span data-stu-id="68fb8-231">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

$PigQuery = "Register wasbs:///pig_python.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasbs:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for the Pig job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="68fb8-232">The output for the **Pig** job should appear similar to the following:</span><span class="sxs-lookup"><span data-stu-id="68fb8-232">The output for the **Pig** job should appear similar to the following:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a><span data-ttu-id="68fb8-233">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="68fb8-233">Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="68fb8-234">Errors when running jobs</span><span class="sxs-lookup"><span data-stu-id="68fb8-234">Errors when running jobs</span></span>

<span data-ttu-id="68fb8-235">When running the hive job, you may encounter an error similar to the following:</span><span class="sxs-lookup"><span data-stu-id="68fb8-235">When running the hive job, you may encounter an error similar to the following:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing to your custom script. It may have crashed with an error.

<span data-ttu-id="68fb8-236">This problem may be caused by the line endings in the streaming.py file.</span><span class="sxs-lookup"><span data-stu-id="68fb8-236">This problem may be caused by the line endings in the streaming.py file.</span></span> <span data-ttu-id="68fb8-237">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span><span class="sxs-lookup"><span data-stu-id="68fb8-237">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="68fb8-238">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span><span class="sxs-lookup"><span data-stu-id="68fb8-238">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span></span>

```powershell
$original_file ='c:\path\to\streaming.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="68fb8-239">PowerShell scripts</span><span class="sxs-lookup"><span data-stu-id="68fb8-239">PowerShell scripts</span></span>

<span data-ttu-id="68fb8-240">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span><span class="sxs-lookup"><span data-stu-id="68fb8-240">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span></span> <span data-ttu-id="68fb8-241">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span><span class="sxs-lookup"><span data-stu-id="68fb8-241">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="68fb8-242">The error information (STDERR,) and the result of the job (STDOUT,) are also logged to your HDInsight storage.</span><span class="sxs-lookup"><span data-stu-id="68fb8-242">The error information (STDERR,) and the result of the job (STDOUT,) are also logged to your HDInsight storage.</span></span>

| <span data-ttu-id="68fb8-243">For this job..</span><span class="sxs-lookup"><span data-stu-id="68fb8-243">For this job..</span></span> | <span data-ttu-id="68fb8-244">Look at these files in the blob container</span><span class="sxs-lookup"><span data-stu-id="68fb8-244">Look at these files in the blob container</span></span> |
| --- | --- |
| <span data-ttu-id="68fb8-245">Hive</span><span class="sxs-lookup"><span data-stu-id="68fb8-245">Hive</span></span> |<span data-ttu-id="68fb8-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="68fb8-246">/HivePython/stderr</span></span><p><span data-ttu-id="68fb8-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="68fb8-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="68fb8-248">Pig</span><span class="sxs-lookup"><span data-stu-id="68fb8-248">Pig</span></span> |<span data-ttu-id="68fb8-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="68fb8-249">/PigPython/stderr</span></span><p><span data-ttu-id="68fb8-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="68fb8-250">/PigPython/stdout</span></span> |

## <a name="next"></a><span data-ttu-id="68fb8-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="68fb8-251">Next steps</span></span>

<span data-ttu-id="68fb8-252">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="68fb8-252">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="68fb8-253">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="68fb8-253">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="68fb8-254">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="68fb8-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="68fb8-255">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="68fb8-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="68fb8-256">Use MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="68fb8-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
