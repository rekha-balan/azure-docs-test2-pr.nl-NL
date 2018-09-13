---
title: Transform data with Databricks Python - Azure | Microsoft Docs
description: Learn how to process or transform data by running a Databricks Python.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.assetid: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/15/2018
ms.author: douglasl
ms.openlocfilehash: 17a8e6f6d6d374c6f8620ecb525727e6fee8c4b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857631"
---
# <a name="transform-data-by-running-a-python-activity-in-azure-databricks"></a><span data-ttu-id="0e464-103">Transform data by running a Python activity in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="0e464-103">Transform data by running a Python activity in Azure Databricks</span></span>

<span data-ttu-id="0e464-104">The Azure Databricks Python Activity in a [Data Factory pipeline](concepts-pipelines-activities.md) runs a Python file in your Azure Databricks cluster.</span><span class="sxs-lookup"><span data-stu-id="0e464-104">The Azure Databricks Python Activity in a [Data Factory pipeline](concepts-pipelines-activities.md) runs a Python file in your Azure Databricks cluster.</span></span> <span data-ttu-id="0e464-105">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="0e464-105">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span> <span data-ttu-id="0e464-106">Azure Databricks is a managed platform for running Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="0e464-106">Azure Databricks is a managed platform for running Apache Spark.</span></span>

<span data-ttu-id="0e464-107">For an eleven-minute introduction and demonstration of this feature, watch the following video:</span><span class="sxs-lookup"><span data-stu-id="0e464-107">For an eleven-minute introduction and demonstration of this feature, watch the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Execute-Jars-and-Python-scripts-on-Azure-Databricks-using-Data-Factory/player]

## <a name="databricks-python-activity-definition"></a><span data-ttu-id="0e464-108">Databricks Python activity definition</span><span class="sxs-lookup"><span data-stu-id="0e464-108">Databricks Python activity definition</span></span>

<span data-ttu-id="0e464-109">Here is the sample JSON definition of a Databricks Python Activity:</span><span class="sxs-lookup"><span data-stu-id="0e464-109">Here is the sample JSON definition of a Databricks Python Activity:</span></span>

```json
{
    "activity": {
        "name": "MyActivity",
        "description": "MyActivity description",
        "type": "DatabricksSparkPython",
        "linkedServiceName": {
            "referenceName": "MyDatabricksLinkedservice",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "pythonFile": "dbfs:/docs/pi.py",
            "parameters": [
                "10"
            ],
            "libraries": [
                {
                    "pypi": {
                        "package": "tensorflow"
                    }
                }
            ]
        }
    }
}
```

## <a name="databricks-python-activity-properties"></a><span data-ttu-id="0e464-110">Databricks Python activity properties</span><span class="sxs-lookup"><span data-stu-id="0e464-110">Databricks Python activity properties</span></span>

<span data-ttu-id="0e464-111">The following table describes the JSON properties used in the JSON definition:</span><span class="sxs-lookup"><span data-stu-id="0e464-111">The following table describes the JSON properties used in the JSON definition:</span></span>

|<span data-ttu-id="0e464-112">Property</span><span class="sxs-lookup"><span data-stu-id="0e464-112">Property</span></span>|<span data-ttu-id="0e464-113">Description</span><span class="sxs-lookup"><span data-stu-id="0e464-113">Description</span></span>|<span data-ttu-id="0e464-114">Required</span><span class="sxs-lookup"><span data-stu-id="0e464-114">Required</span></span>|
|---|---|---|
|<span data-ttu-id="0e464-115">name</span><span class="sxs-lookup"><span data-stu-id="0e464-115">name</span></span>|<span data-ttu-id="0e464-116">Name of the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="0e464-116">Name of the activity in the pipeline.</span></span>|<span data-ttu-id="0e464-117">Yes</span><span class="sxs-lookup"><span data-stu-id="0e464-117">Yes</span></span>|
|<span data-ttu-id="0e464-118">description</span><span class="sxs-lookup"><span data-stu-id="0e464-118">description</span></span>|<span data-ttu-id="0e464-119">Text describing what the activity does.</span><span class="sxs-lookup"><span data-stu-id="0e464-119">Text describing what the activity does.</span></span>|<span data-ttu-id="0e464-120">No</span><span class="sxs-lookup"><span data-stu-id="0e464-120">No</span></span>|
|<span data-ttu-id="0e464-121">type</span><span class="sxs-lookup"><span data-stu-id="0e464-121">type</span></span>|<span data-ttu-id="0e464-122">For Databricks Python Activity, the activity type is  DatabricksSparkPython.</span><span class="sxs-lookup"><span data-stu-id="0e464-122">For Databricks Python Activity, the activity type is  DatabricksSparkPython.</span></span>|<span data-ttu-id="0e464-123">Yes</span><span class="sxs-lookup"><span data-stu-id="0e464-123">Yes</span></span>|
|<span data-ttu-id="0e464-124">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0e464-124">linkedServiceName</span></span>|<span data-ttu-id="0e464-125">Name of the Databricks Linked Service on which the Python activity runs.</span><span class="sxs-lookup"><span data-stu-id="0e464-125">Name of the Databricks Linked Service on which the Python activity runs.</span></span> <span data-ttu-id="0e464-126">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="0e464-126">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span>|<span data-ttu-id="0e464-127">Yes</span><span class="sxs-lookup"><span data-stu-id="0e464-127">Yes</span></span>|
|<span data-ttu-id="0e464-128">pythonFile</span><span class="sxs-lookup"><span data-stu-id="0e464-128">pythonFile</span></span>|<span data-ttu-id="0e464-129">The URI of the Python file to be executed.</span><span class="sxs-lookup"><span data-stu-id="0e464-129">The URI of the Python file to be executed.</span></span> <span data-ttu-id="0e464-130">Only DBFS paths are supported.</span><span class="sxs-lookup"><span data-stu-id="0e464-130">Only DBFS paths are supported.</span></span>|<span data-ttu-id="0e464-131">Yes</span><span class="sxs-lookup"><span data-stu-id="0e464-131">Yes</span></span>|
|<span data-ttu-id="0e464-132">parameters</span><span class="sxs-lookup"><span data-stu-id="0e464-132">parameters</span></span>|<span data-ttu-id="0e464-133">Command line parameters that will be passed to the Python file.</span><span class="sxs-lookup"><span data-stu-id="0e464-133">Command line parameters that will be passed to the Python file.</span></span> <span data-ttu-id="0e464-134">This is an array of strings.</span><span class="sxs-lookup"><span data-stu-id="0e464-134">This is an array of strings.</span></span>|<span data-ttu-id="0e464-135">No</span><span class="sxs-lookup"><span data-stu-id="0e464-135">No</span></span>|
|<span data-ttu-id="0e464-136">libraries</span><span class="sxs-lookup"><span data-stu-id="0e464-136">libraries</span></span>|<span data-ttu-id="0e464-137">A list of libraries to be installed on the cluster that will execute the job.</span><span class="sxs-lookup"><span data-stu-id="0e464-137">A list of libraries to be installed on the cluster that will execute the job.</span></span> <span data-ttu-id="0e464-138">It can be an array of <string, object></span><span class="sxs-lookup"><span data-stu-id="0e464-138">It can be an array of <string, object></span></span>|<span data-ttu-id="0e464-139">No</span><span class="sxs-lookup"><span data-stu-id="0e464-139">No</span></span>|

## <a name="supported-libraries-for-databricks-activities"></a><span data-ttu-id="0e464-140">Supported libraries for databricks activities</span><span class="sxs-lookup"><span data-stu-id="0e464-140">Supported libraries for databricks activities</span></span>

<span data-ttu-id="0e464-141">In the above Databricks activity definition you specify these library types: *jar*, *egg*, *maven*, *pypi*, *cran*.</span><span class="sxs-lookup"><span data-stu-id="0e464-141">In the above Databricks activity definition you specify these library types: *jar*, *egg*, *maven*, *pypi*, *cran*.</span></span>

```json
{
    "libraries": [
        {
            "jar": "dbfs:/mnt/libraries/library.jar"
        },
        {
            "egg": "dbfs:/mnt/libraries/library.egg"
        },
        {
            "maven": {
                "coordinates": "org.jsoup:jsoup:1.7.2",
                "exclusions": [ "slf4j:slf4j" ]
            }
        },
        {
            "pypi": {
                "package": "simplejson",
                "repo": "http://my-pypi-mirror.com"
            }
        },
        {
            "cran": {
                "package": "ada",
                "repo": "http://cran.us.r-project.org"
            }
        }
    ]
}

```

<span data-ttu-id="0e464-142">For more details refer [Databricks documentation](https://docs.azuredatabricks.net/api/latest/libraries.html#managedlibrarieslibrary) for library types.</span><span class="sxs-lookup"><span data-stu-id="0e464-142">For more details refer [Databricks documentation](https://docs.azuredatabricks.net/api/latest/libraries.html#managedlibrarieslibrary) for library types.</span></span>

## <a name="how-to-upload-a-library-in-databricks"></a><span data-ttu-id="0e464-143">How to upload a library in Databricks</span><span class="sxs-lookup"><span data-stu-id="0e464-143">How to upload a library in Databricks</span></span>

#### <a name="using-databricks-workspace-uihttpsdocsazuredatabricksnetuser-guidelibrarieshtmlcreate-a-library"></a>[<span data-ttu-id="0e464-144">Using Databricks workspace UI</span><span class="sxs-lookup"><span data-stu-id="0e464-144">Using Databricks workspace UI</span></span>](https://docs.azuredatabricks.net/user-guide/libraries.html#create-a-library)

<span data-ttu-id="0e464-145">To obtain the dbfs path of the library added using UI, you can use [Databricks CLI (installation)](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#install-the-cli).</span><span class="sxs-lookup"><span data-stu-id="0e464-145">To obtain the dbfs path of the library added using UI, you can use [Databricks CLI (installation)](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#install-the-cli).</span></span> 

<span data-ttu-id="0e464-146">Typically the Jar libraries are stored under dbfs:/FileStore/jars while using the UI.</span><span class="sxs-lookup"><span data-stu-id="0e464-146">Typically the Jar libraries are stored under dbfs:/FileStore/jars while using the UI.</span></span> <span data-ttu-id="0e464-147">You can list all through the CLI: *databricks fs ls dbfs:/FileStore/jars*</span><span class="sxs-lookup"><span data-stu-id="0e464-147">You can list all through the CLI: *databricks fs ls dbfs:/FileStore/jars*</span></span> 



#### <a name="copy-library-using-databricks-clihttpsdocsazuredatabricksnetuser-guidedev-toolsdatabricks-clihtmlcopy-a-file-to-dbfs"></a>[<span data-ttu-id="0e464-148">Copy library using Databricks CLI</span><span class="sxs-lookup"><span data-stu-id="0e464-148">Copy library using Databricks CLI</span></span>](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#copy-a-file-to-dbfs)

<span data-ttu-id="0e464-149">Example: *databricks fs cp SparkPi-assembly-0.1.jar dbfs:/FileStore/jars*</span><span class="sxs-lookup"><span data-stu-id="0e464-149">Example: *databricks fs cp SparkPi-assembly-0.1.jar dbfs:/FileStore/jars*</span></span>