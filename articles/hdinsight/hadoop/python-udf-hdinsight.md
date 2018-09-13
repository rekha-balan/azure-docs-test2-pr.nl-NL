---
title: Python UDF with Apache Hive and Pig - Azure HDInsight
description: Learn how to use Python User Defined Functions (UDF) from Hive and Pig in HDInsight, the Hadoop technology stack on Azure.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.topic: conceptual
ms.date: 02/27/2018
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ef9292e7e36f5accabf532ef4a26d334fb880859
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967757"
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="dff04-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="dff04-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="dff04-104">Learn how to use Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dff04-104">Learn how to use Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <a name="python"></a><span data-ttu-id="dff04-105">Python on HDInsight</span><span class="sxs-lookup"><span data-stu-id="dff04-105">Python on HDInsight</span></span>

<span data-ttu-id="dff04-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span><span class="sxs-lookup"><span data-stu-id="dff04-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="dff04-107">Apache Hive can be used with this version of Python for stream processing.</span><span class="sxs-lookup"><span data-stu-id="dff04-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="dff04-108">Stream processing uses STDOUT and STDIN to pass data between Hive and the UDF.</span><span class="sxs-lookup"><span data-stu-id="dff04-108">Stream processing uses STDOUT and STDIN to pass data between Hive and the UDF.</span></span>

<span data-ttu-id="dff04-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span><span class="sxs-lookup"><span data-stu-id="dff04-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="dff04-110">Jython runs directly on the Java Virtual Machine and does not use streaming.</span><span class="sxs-lookup"><span data-stu-id="dff04-110">Jython runs directly on the Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="dff04-111">Jython is the recommended Python interpreter when using Python with Pig.</span><span class="sxs-lookup"><span data-stu-id="dff04-111">Jython is the recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="dff04-112">The steps in this document make the following assumptions:</span><span class="sxs-lookup"><span data-stu-id="dff04-112">The steps in this document make the following assumptions:</span></span> 
>
> * <span data-ttu-id="dff04-113">You create the Python scripts on your local development environment.</span><span class="sxs-lookup"><span data-stu-id="dff04-113">You create the Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="dff04-114">You upload the scripts to HDInsight using either the `scp` command from a local Bash session or the provided PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="dff04-114">You upload the scripts to HDInsight using either the `scp` command from a local Bash session or the provided PowerShell script.</span></span>
>
> <span data-ttu-id="dff04-115">If you want to use the [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview to work with HDInsight, then you must:</span><span class="sxs-lookup"><span data-stu-id="dff04-115">If you want to use the [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview to work with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="dff04-116">Create the scripts inside the cloud shell environment.</span><span class="sxs-lookup"><span data-stu-id="dff04-116">Create the scripts inside the cloud shell environment.</span></span>
> * <span data-ttu-id="dff04-117">Use `scp` to upload the files from the cloud shell to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dff04-117">Use `scp` to upload the files from the cloud shell to HDInsight.</span></span>
> * <span data-ttu-id="dff04-118">Use `ssh` from the cloud shell to connect to HDInsight and run the examples.</span><span class="sxs-lookup"><span data-stu-id="dff04-118">Use `ssh` from the cloud shell to connect to HDInsight and run the examples.</span></span>

## <a name="hivepython"></a><span data-ttu-id="dff04-119">Hive UDF</span><span class="sxs-lookup"><span data-stu-id="dff04-119">Hive UDF</span></span>

<span data-ttu-id="dff04-120">Python can be used as a UDF from Hive through the HiveQL `TRANSFORM` statement.</span><span class="sxs-lookup"><span data-stu-id="dff04-120">Python can be used as a UDF from Hive through the HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="dff04-121">For example, the following HiveQL invokes the `hiveudf.py` file stored in the default Azure Storage account for the cluster.</span><span class="sxs-lookup"><span data-stu-id="dff04-121">For example, the following HiveQL invokes the `hiveudf.py` file stored in the default Azure Storage account for the cluster.</span></span>

<span data-ttu-id="dff04-122">**Linux-based HDInsight**</span><span class="sxs-lookup"><span data-stu-id="dff04-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="dff04-123">**Windows-based HDInsight**</span><span class="sxs-lookup"><span data-stu-id="dff04-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="dff04-124">On Windows-based HDInsight clusters, the `USING` clause must specify the full path to python.exe.</span><span class="sxs-lookup"><span data-stu-id="dff04-124">On Windows-based HDInsight clusters, the `USING` clause must specify the full path to python.exe.</span></span>

<span data-ttu-id="dff04-125">Here's what this example does:</span><span class="sxs-lookup"><span data-stu-id="dff04-125">Here's what this example does:</span></span>

1. <span data-ttu-id="dff04-126">The `add file` statement at the beginning of the file adds the `hiveudf.py` file to the distributed cache, so it's accessible by all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="dff04-126">The `add file` statement at the beginning of the file adds the `hiveudf.py` file to the distributed cache, so it's accessible by all nodes in the cluster.</span></span>
2. <span data-ttu-id="dff04-127">The `SELECT TRANSFORM ... USING` statement selects data from the `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="dff04-127">The `SELECT TRANSFORM ... USING` statement selects data from the `hivesampletable`.</span></span> <span data-ttu-id="dff04-128">It also passes the clientid, devicemake, and devicemodel values to the `hiveudf.py` script.</span><span class="sxs-lookup"><span data-stu-id="dff04-128">It also passes the clientid, devicemake, and devicemodel values to the `hiveudf.py` script.</span></span>
3. <span data-ttu-id="dff04-129">The `AS` clause describes the fields returned from `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="dff04-129">The `AS` clause describes the fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-the-hiveudfpy-file"></a><span data-ttu-id="dff04-130">Create the hiveudf.py file</span><span class="sxs-lookup"><span data-stu-id="dff04-130">Create the hiveudf.py file</span></span>


<span data-ttu-id="dff04-131">On your development environment, create a text file named `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="dff04-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="dff04-132">Use the following code as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="dff04-132">Use the following code as the contents of the file:</span></span>

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

<span data-ttu-id="dff04-133">This script performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="dff04-133">This script performs the following actions:</span></span>

1. <span data-ttu-id="dff04-134">Read a line of data from STDIN.</span><span class="sxs-lookup"><span data-stu-id="dff04-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="dff04-135">The trailing newline character is removed using `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="dff04-135">The trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="dff04-136">When doing stream processing, a single line contains all the values with a tab character between each value.</span><span class="sxs-lookup"><span data-stu-id="dff04-136">When doing stream processing, a single line contains all the values with a tab character between each value.</span></span> <span data-ttu-id="dff04-137">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span><span class="sxs-lookup"><span data-stu-id="dff04-137">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span></span>
4. <span data-ttu-id="dff04-138">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span><span class="sxs-lookup"><span data-stu-id="dff04-138">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="dff04-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="dff04-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="dff04-140">The `while` loop repeats until no `line` is read.</span><span class="sxs-lookup"><span data-stu-id="dff04-140">The `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="dff04-141">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span><span class="sxs-lookup"><span data-stu-id="dff04-141">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span></span>

<span data-ttu-id="dff04-142">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dff04-142">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span></span>

## <a name="pigpython"></a><span data-ttu-id="dff04-143">Pig UDF</span><span class="sxs-lookup"><span data-stu-id="dff04-143">Pig UDF</span></span>

<span data-ttu-id="dff04-144">A Python script can be used as a UDF from Pig through the `GENERATE` statement.</span><span class="sxs-lookup"><span data-stu-id="dff04-144">A Python script can be used as a UDF from Pig through the `GENERATE` statement.</span></span> <span data-ttu-id="dff04-145">You can run the script using either Jython or C Python.</span><span class="sxs-lookup"><span data-stu-id="dff04-145">You can run the script using either Jython or C Python.</span></span>

* <span data-ttu-id="dff04-146">Jython runs on the JVM, and can natively be called from Pig.</span><span class="sxs-lookup"><span data-stu-id="dff04-146">Jython runs on the JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="dff04-147">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span><span class="sxs-lookup"><span data-stu-id="dff04-147">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span></span> <span data-ttu-id="dff04-148">The output of the Python script is sent back into Pig.</span><span class="sxs-lookup"><span data-stu-id="dff04-148">The output of the Python script is sent back into Pig.</span></span>

<span data-ttu-id="dff04-149">To specify the Python interpreter, use `register` when referencing the Python script.</span><span class="sxs-lookup"><span data-stu-id="dff04-149">To specify the Python interpreter, use `register` when referencing the Python script.</span></span> <span data-ttu-id="dff04-150">The following examples register scripts with Pig as `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="dff04-150">The following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="dff04-151">**To use Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="dff04-151">**To use Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="dff04-152">**To use C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="dff04-152">**To use C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dff04-153">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span><span class="sxs-lookup"><span data-stu-id="dff04-153">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="dff04-154">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span><span class="sxs-lookup"><span data-stu-id="dff04-154">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span></span>

<span data-ttu-id="dff04-155">Once past registration, the Pig Latin for this example is the same for both:</span><span class="sxs-lookup"><span data-stu-id="dff04-155">Once past registration, the Pig Latin for this example is the same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="dff04-156">Here's what this example does:</span><span class="sxs-lookup"><span data-stu-id="dff04-156">Here's what this example does:</span></span>

1. <span data-ttu-id="dff04-157">The first line loads the sample data file, `sample.log` into `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="dff04-157">The first line loads the sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="dff04-158">It also defines each record as a `chararray`.</span><span class="sxs-lookup"><span data-stu-id="dff04-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="dff04-159">The next line filters out any null values, storing the result of the operation into `LOG`.</span><span class="sxs-lookup"><span data-stu-id="dff04-159">The next line filters out any null values, storing the result of the operation into `LOG`.</span></span>
3. <span data-ttu-id="dff04-160">Next, it iterates over the records in `LOG` and uses `GENERATE` to invoke the `create_structure` method contained in the Python/Jython script loaded as `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="dff04-160">Next, it iterates over the records in `LOG` and uses `GENERATE` to invoke the `create_structure` method contained in the Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="dff04-161">`LINE` is used to pass the current record to the function.</span><span class="sxs-lookup"><span data-stu-id="dff04-161">`LINE` is used to pass the current record to the function.</span></span>
4. <span data-ttu-id="dff04-162">Finally, the outputs are dumped to STDOUT using the `DUMP` command.</span><span class="sxs-lookup"><span data-stu-id="dff04-162">Finally, the outputs are dumped to STDOUT using the `DUMP` command.</span></span> <span data-ttu-id="dff04-163">This command displays the results after the operation completes.</span><span class="sxs-lookup"><span data-stu-id="dff04-163">This command displays the results after the operation completes.</span></span>

### <a name="create-the-pigudfpy-file"></a><span data-ttu-id="dff04-164">Create the pigudf.py file</span><span class="sxs-lookup"><span data-stu-id="dff04-164">Create the pigudf.py file</span></span>

<span data-ttu-id="dff04-165">On your development environment, create a text file named `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="dff04-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="dff04-166">Use the following code as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="dff04-166">Use the following code as the contents of the file:</span></span>

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

<span data-ttu-id="dff04-167">In the Pig Latin example, the `LINE` input is defined as a chararray because there is no consistent schema for the input.</span><span class="sxs-lookup"><span data-stu-id="dff04-167">In the Pig Latin example, the `LINE` input is defined as a chararray because there is no consistent schema for the input.</span></span> <span data-ttu-id="dff04-168">The Python script transforms the data into a consistent schema for output.</span><span class="sxs-lookup"><span data-stu-id="dff04-168">The Python script transforms the data into a consistent schema for output.</span></span>

1. <span data-ttu-id="dff04-169">The `@outputSchema` statement defines the format of the data that is returned to Pig.</span><span class="sxs-lookup"><span data-stu-id="dff04-169">The `@outputSchema` statement defines the format of the data that is returned to Pig.</span></span> <span data-ttu-id="dff04-170">In this case, it's a **data bag**, which is a Pig data type.</span><span class="sxs-lookup"><span data-stu-id="dff04-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="dff04-171">The bag contains the following fields, all of which are chararray (strings):</span><span class="sxs-lookup"><span data-stu-id="dff04-171">The bag contains the following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="dff04-172">date - the date the log entry was created</span><span class="sxs-lookup"><span data-stu-id="dff04-172">date - the date the log entry was created</span></span>
   * <span data-ttu-id="dff04-173">time - the time the log entry was created</span><span class="sxs-lookup"><span data-stu-id="dff04-173">time - the time the log entry was created</span></span>
   * <span data-ttu-id="dff04-174">classname - the class name the entry was created for</span><span class="sxs-lookup"><span data-stu-id="dff04-174">classname - the class name the entry was created for</span></span>
   * <span data-ttu-id="dff04-175">level - the log level</span><span class="sxs-lookup"><span data-stu-id="dff04-175">level - the log level</span></span>
   * <span data-ttu-id="dff04-176">detail - verbose details for the log entry</span><span class="sxs-lookup"><span data-stu-id="dff04-176">detail - verbose details for the log entry</span></span>

2. <span data-ttu-id="dff04-177">Next, the `def create_structure(input)` defines the function that Pig passes line items to.</span><span class="sxs-lookup"><span data-stu-id="dff04-177">Next, the `def create_structure(input)` defines the function that Pig passes line items to.</span></span>

3. <span data-ttu-id="dff04-178">The example data, `sample.log`, mostly conforms to the date, time, classname, level, and detail schema.</span><span class="sxs-lookup"><span data-stu-id="dff04-178">The example data, `sample.log`, mostly conforms to the date, time, classname, level, and detail schema.</span></span> <span data-ttu-id="dff04-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="dff04-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="dff04-180">These lines must be modified to match the schema.</span><span class="sxs-lookup"><span data-stu-id="dff04-180">These lines must be modified to match the schema.</span></span> <span data-ttu-id="dff04-181">The `if` statement checks for those, then massages the input data to move the `*java.lang.Exception*` string to the end, bringing the data in-line with the expected output schema.</span><span class="sxs-lookup"><span data-stu-id="dff04-181">The `if` statement checks for those, then massages the input data to move the `*java.lang.Exception*` string to the end, bringing the data in-line with the expected output schema.</span></span>

4. <span data-ttu-id="dff04-182">Next, the `split` command is used to split the data at the first four space characters.</span><span class="sxs-lookup"><span data-stu-id="dff04-182">Next, the `split` command is used to split the data at the first four space characters.</span></span> <span data-ttu-id="dff04-183">The output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span><span class="sxs-lookup"><span data-stu-id="dff04-183">The output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="dff04-184">Finally, the values are returned to Pig.</span><span class="sxs-lookup"><span data-stu-id="dff04-184">Finally, the values are returned to Pig.</span></span>

<span data-ttu-id="dff04-185">When the data is returned to Pig, it has a consistent schema as defined in the `@outputSchema` statement.</span><span class="sxs-lookup"><span data-stu-id="dff04-185">When the data is returned to Pig, it has a consistent schema as defined in the `@outputSchema` statement.</span></span>

## <a name="running"></a><span data-ttu-id="dff04-186">Upload and run the examples</span><span class="sxs-lookup"><span data-stu-id="dff04-186">Upload and run the examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dff04-187">The **SSH** steps only work with a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dff04-187">The **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="dff04-188">The **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span><span class="sxs-lookup"><span data-stu-id="dff04-188">The **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="dff04-189">SSH</span><span class="sxs-lookup"><span data-stu-id="dff04-189">SSH</span></span>

<span data-ttu-id="dff04-190">For more information on using SSH, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="dff04-190">For more information on using SSH, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="dff04-191">Use `scp` to copy the files to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dff04-191">Use `scp` to copy the files to your HDInsight cluster.</span></span> <span data-ttu-id="dff04-192">For example, the following command copies the files to a cluster named **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="dff04-192">For example, the following command copies the files to a cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="dff04-193">Use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="dff04-193">Use SSH to connect to the cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="dff04-194">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="dff04-194">For more information, see the [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

3. <span data-ttu-id="dff04-195">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="dff04-195">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="dff04-196">After uploading the files, use the following steps to run the Hive and Pig jobs.</span><span class="sxs-lookup"><span data-stu-id="dff04-196">After uploading the files, use the following steps to run the Hive and Pig jobs.</span></span>

#### <a name="use-the-hive-udf"></a><span data-ttu-id="dff04-197">Use the Hive UDF</span><span class="sxs-lookup"><span data-stu-id="dff04-197">Use the Hive UDF</span></span>

1. <span data-ttu-id="dff04-198">To connect to Hive, use the following command:</span><span class="sxs-lookup"><span data-stu-id="dff04-198">To connect to Hive, use the following command:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="dff04-199">This command starts the Beeline client.</span><span class="sxs-lookup"><span data-stu-id="dff04-199">This command starts the Beeline client.</span></span>

2. <span data-ttu-id="dff04-200">Enter the following query at the `0: jdbc:hive2://headnodehost:10001/>` prompt:</span><span class="sxs-lookup"><span data-stu-id="dff04-200">Enter the following query at the `0: jdbc:hive2://headnodehost:10001/>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="dff04-201">After entering the last line, the job should start.</span><span class="sxs-lookup"><span data-stu-id="dff04-201">After entering the last line, the job should start.</span></span> <span data-ttu-id="dff04-202">Once the job completes, it returns output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="dff04-202">Once the job completes, it returns output similar to the following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

4. <span data-ttu-id="dff04-203">To exit Beeline, use the following command:</span><span class="sxs-lookup"><span data-stu-id="dff04-203">To exit Beeline, use the following command:</span></span>

    ```hive
    !q
    ```

#### <a name="use-the-pig-udf"></a><span data-ttu-id="dff04-204">Use the Pig UDF</span><span class="sxs-lookup"><span data-stu-id="dff04-204">Use the Pig UDF</span></span>

1. <span data-ttu-id="dff04-205">To connect to pig, use the following command:</span><span class="sxs-lookup"><span data-stu-id="dff04-205">To connect to pig, use the following command:</span></span>

    ```bash
    pig
    ```

2. <span data-ttu-id="dff04-206">Enter the following statements at the `grunt>` prompt:</span><span class="sxs-lookup"><span data-stu-id="dff04-206">Enter the following statements at the `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="dff04-207">After entering the following line, the job should start.</span><span class="sxs-lookup"><span data-stu-id="dff04-207">After entering the following line, the job should start.</span></span> <span data-ttu-id="dff04-208">Once the job completes, it returns output similar to the following data:</span><span class="sxs-lookup"><span data-stu-id="dff04-208">Once the job completes, it returns output similar to the following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="dff04-209">Use `quit` to exit the Grunt shell, and then use the following to edit the pigudf.py file on the local file system:</span><span class="sxs-lookup"><span data-stu-id="dff04-209">Use `quit` to exit the Grunt shell, and then use the following to edit the pigudf.py file on the local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="dff04-210">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span><span class="sxs-lookup"><span data-stu-id="dff04-210">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="dff04-211">This line modifies the Python script to work with C Python instead of Jython.</span><span class="sxs-lookup"><span data-stu-id="dff04-211">This line modifies the Python script to work with C Python instead of Jython.</span></span> <span data-ttu-id="dff04-212">Once the change has been made, use **Ctrl+X** to exit the editor.</span><span class="sxs-lookup"><span data-stu-id="dff04-212">Once the change has been made, use **Ctrl+X** to exit the editor.</span></span> <span data-ttu-id="dff04-213">Select **Y**, and then **Enter** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="dff04-213">Select **Y**, and then **Enter** to save the changes.</span></span>

6. <span data-ttu-id="dff04-214">Use the `pig` command to start the shell again.</span><span class="sxs-lookup"><span data-stu-id="dff04-214">Use the `pig` command to start the shell again.</span></span> <span data-ttu-id="dff04-215">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span><span class="sxs-lookup"><span data-stu-id="dff04-215">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="dff04-216">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span><span class="sxs-lookup"><span data-stu-id="dff04-216">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span></span>

### <a name="powershell-upload-the-files"></a><span data-ttu-id="dff04-217">PowerShell: Upload the files</span><span class="sxs-lookup"><span data-stu-id="dff04-217">PowerShell: Upload the files</span></span>

<span data-ttu-id="dff04-218">You can use PowerShell to upload the files to the HDInsight server.</span><span class="sxs-lookup"><span data-stu-id="dff04-218">You can use PowerShell to upload the files to the HDInsight server.</span></span> <span data-ttu-id="dff04-219">Use the following script to upload the Python files:</span><span class="sxs-lookup"><span data-stu-id="dff04-219">Use the following script to upload the Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="dff04-220">The steps in this section use Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dff04-220">The steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="dff04-221">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dff04-221">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!code-powershell[main](../../../powershell_scripts/hdinsight/run-python-udf/run-python-udf.ps1?range=5-41)]

> [!IMPORTANT]
> <span data-ttu-id="dff04-222">Change the `C:\path\to` value to the path to the files on your development environment.</span><span class="sxs-lookup"><span data-stu-id="dff04-222">Change the `C:\path\to` value to the path to the files on your development environment.</span></span>

<span data-ttu-id="dff04-223">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span><span class="sxs-lookup"><span data-stu-id="dff04-223">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span></span>

> [!NOTE]
> <span data-ttu-id="dff04-224">For more information on uploading files, see the [Upload data for Hadoop jobs in HDInsight](../hdinsight-upload-data.md) document.</span><span class="sxs-lookup"><span data-stu-id="dff04-224">For more information on uploading files, see the [Upload data for Hadoop jobs in HDInsight](../hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-the-hive-udf"></a><span data-ttu-id="dff04-225">PowerShell: Use the Hive UDF</span><span class="sxs-lookup"><span data-stu-id="dff04-225">PowerShell: Use the Hive UDF</span></span>

<span data-ttu-id="dff04-226">PowerShell can also be used to remotely run Hive queries.</span><span class="sxs-lookup"><span data-stu-id="dff04-226">PowerShell can also be used to remotely run Hive queries.</span></span> <span data-ttu-id="dff04-227">Use the following PowerShell script to run a Hive query that uses **hiveudf.py** script:</span><span class="sxs-lookup"><span data-stu-id="dff04-227">Use the following PowerShell script to run a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dff04-228">Before running, the script prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dff04-228">Before running, the script prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span></span>

[!code-powershell[main](../../../powershell_scripts/hdinsight/run-python-udf/run-python-udf.ps1?range=45-94)]

<span data-ttu-id="dff04-229">The output for the **Hive** job should appear similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="dff04-229">The output for the **Hive** job should appear similar to the following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="dff04-230">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="dff04-230">Pig (Jython)</span></span>

<span data-ttu-id="dff04-231">PowerShell can also be used to run Pig Latin jobs.</span><span class="sxs-lookup"><span data-stu-id="dff04-231">PowerShell can also be used to run Pig Latin jobs.</span></span> <span data-ttu-id="dff04-232">To run a Pig Latin job that uses the **pigudf.py** script, use the following PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="dff04-232">To run a Pig Latin job that uses the **pigudf.py** script, use the following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="dff04-233">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span><span class="sxs-lookup"><span data-stu-id="dff04-233">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span></span>

[!code-powershell[main](../../../powershell_scripts/hdinsight/run-python-udf/run-python-udf.ps1?range=98-144)]

<span data-ttu-id="dff04-234">The output for the **Pig** job should appear similar to the following data:</span><span class="sxs-lookup"><span data-stu-id="dff04-234">The output for the **Pig** job should appear similar to the following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a><span data-ttu-id="dff04-235">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="dff04-235">Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="dff04-236">Errors when running jobs</span><span class="sxs-lookup"><span data-stu-id="dff04-236">Errors when running jobs</span></span>

<span data-ttu-id="dff04-237">When running the hive job, you may encounter an error similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="dff04-237">When running the hive job, you may encounter an error similar to the following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing to your custom script. It may have crashed with an error.

<span data-ttu-id="dff04-238">This problem may be caused by the line endings in the Python file.</span><span class="sxs-lookup"><span data-stu-id="dff04-238">This problem may be caused by the line endings in the Python file.</span></span> <span data-ttu-id="dff04-239">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span><span class="sxs-lookup"><span data-stu-id="dff04-239">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="dff04-240">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span><span class="sxs-lookup"><span data-stu-id="dff04-240">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span></span>

[!code-powershell[main](../../../powershell_scripts/hdinsight/run-python-udf/run-python-udf.ps1?range=148-150)]

### <a name="powershell-scripts"></a><span data-ttu-id="dff04-241">PowerShell scripts</span><span class="sxs-lookup"><span data-stu-id="dff04-241">PowerShell scripts</span></span>

<span data-ttu-id="dff04-242">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span><span class="sxs-lookup"><span data-stu-id="dff04-242">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span></span> <span data-ttu-id="dff04-243">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span><span class="sxs-lookup"><span data-stu-id="dff04-243">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span></span>

[!code-powershell[main](../../../powershell_scripts/hdinsight/run-python-udf/run-python-udf.ps1?range=135-139)]

<span data-ttu-id="dff04-244">The error information (STDERR) and the result of the job (STDOUT) are also logged to your HDInsight storage.</span><span class="sxs-lookup"><span data-stu-id="dff04-244">The error information (STDERR) and the result of the job (STDOUT) are also logged to your HDInsight storage.</span></span>

| <span data-ttu-id="dff04-245">For this job...</span><span class="sxs-lookup"><span data-stu-id="dff04-245">For this job...</span></span> | <span data-ttu-id="dff04-246">Look at these files in the blob container</span><span class="sxs-lookup"><span data-stu-id="dff04-246">Look at these files in the blob container</span></span> |
| --- | --- |
| <span data-ttu-id="dff04-247">Hive</span><span class="sxs-lookup"><span data-stu-id="dff04-247">Hive</span></span> |<span data-ttu-id="dff04-248">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="dff04-248">/HivePython/stderr</span></span><p><span data-ttu-id="dff04-249">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="dff04-249">/HivePython/stdout</span></span> |
| <span data-ttu-id="dff04-250">Pig</span><span class="sxs-lookup"><span data-stu-id="dff04-250">Pig</span></span> |<span data-ttu-id="dff04-251">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="dff04-251">/PigPython/stderr</span></span><p><span data-ttu-id="dff04-252">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="dff04-252">/PigPython/stdout</span></span> |

## <a name="next"></a><span data-ttu-id="dff04-253">Next steps</span><span class="sxs-lookup"><span data-stu-id="dff04-253">Next steps</span></span>

<span data-ttu-id="dff04-254">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="dff04-254">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="dff04-255">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="dff04-255">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="dff04-256">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="dff04-256">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="dff04-257">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="dff04-257">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="dff04-258">Use MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="dff04-258">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
