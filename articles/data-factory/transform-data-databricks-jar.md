---
title: Transform data with Databricks Jar - Azure | Microsoft Docs
description: Learn how to process or transform data by running a Databricks Jar.
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
ms.openlocfilehash: a47d0130cd06a936da456ec6d78bde99907072f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966943"
---
# <a name="transform-data-by-running-a-jar-activity-in-azure-databricks"></a><span data-ttu-id="5b84d-103">Transform data by running a Jar activity in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="5b84d-103">Transform data by running a Jar activity in Azure Databricks</span></span>

<span data-ttu-id="5b84d-104">The Azure Databricks Jar Activity in a [Data Factory pipeline](concepts-pipelines-activities.md) runs a Spark Jar in your Azure Databricks cluster.</span><span class="sxs-lookup"><span data-stu-id="5b84d-104">The Azure Databricks Jar Activity in a [Data Factory pipeline](concepts-pipelines-activities.md) runs a Spark Jar in your Azure Databricks cluster.</span></span> <span data-ttu-id="5b84d-105">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="5b84d-105">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span> <span data-ttu-id="5b84d-106">Azure Databricks is a managed platform for running Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="5b84d-106">Azure Databricks is a managed platform for running Apache Spark.</span></span>

<span data-ttu-id="5b84d-107">For an eleven-minute introduction and demonstration of this feature, watch the following video:</span><span class="sxs-lookup"><span data-stu-id="5b84d-107">For an eleven-minute introduction and demonstration of this feature, watch the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Execute-Jars-and-Python-scripts-on-Azure-Databricks-using-Data-Factory/player]

## <a name="databricks-jar-activity-definition"></a><span data-ttu-id="5b84d-108">Databricks Jar activity definition</span><span class="sxs-lookup"><span data-stu-id="5b84d-108">Databricks Jar activity definition</span></span>

<span data-ttu-id="5b84d-109">Here is the sample JSON definition of a Databricks Jar Activity:</span><span class="sxs-lookup"><span data-stu-id="5b84d-109">Here is the sample JSON definition of a Databricks Jar Activity:</span></span>

```json
{
    "name": "SparkJarActivity",
    "type": "DatabricksSparkJar",
    "linkedServiceName": {
        "referenceName": "AzureDatabricks",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "mainClassName": "org.apache.spark.examples.SparkPi",
        "parameters": [ "10" ],
        "libraries": [
            {
                "jar": "dbfs:/docs/sparkpi.jar"
            }
        ]
    }
}

```

## <a name="databricks-jar-activity-properties"></a><span data-ttu-id="5b84d-110">Databricks Jar activity properties</span><span class="sxs-lookup"><span data-stu-id="5b84d-110">Databricks Jar activity properties</span></span>

<span data-ttu-id="5b84d-111">The following table describes the JSON properties used in the JSON definition:</span><span class="sxs-lookup"><span data-stu-id="5b84d-111">The following table describes the JSON properties used in the JSON definition:</span></span>

|<span data-ttu-id="5b84d-112">Property</span><span class="sxs-lookup"><span data-stu-id="5b84d-112">Property</span></span>|<span data-ttu-id="5b84d-113">Description</span><span class="sxs-lookup"><span data-stu-id="5b84d-113">Description</span></span>|<span data-ttu-id="5b84d-114">Required</span><span class="sxs-lookup"><span data-stu-id="5b84d-114">Required</span></span>|
|:--|---|:-:|
|<span data-ttu-id="5b84d-115">name</span><span class="sxs-lookup"><span data-stu-id="5b84d-115">name</span></span>|<span data-ttu-id="5b84d-116">Name of the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="5b84d-116">Name of the activity in the pipeline.</span></span>|<span data-ttu-id="5b84d-117">Yes</span><span class="sxs-lookup"><span data-stu-id="5b84d-117">Yes</span></span>|
|<span data-ttu-id="5b84d-118">description</span><span class="sxs-lookup"><span data-stu-id="5b84d-118">description</span></span>|<span data-ttu-id="5b84d-119">Text describing what the activity does.</span><span class="sxs-lookup"><span data-stu-id="5b84d-119">Text describing what the activity does.</span></span>|<span data-ttu-id="5b84d-120">No</span><span class="sxs-lookup"><span data-stu-id="5b84d-120">No</span></span>|
|<span data-ttu-id="5b84d-121">type</span><span class="sxs-lookup"><span data-stu-id="5b84d-121">type</span></span>|<span data-ttu-id="5b84d-122">For Databricks Jar Activity, the activity type is DatabricksSparkJar.</span><span class="sxs-lookup"><span data-stu-id="5b84d-122">For Databricks Jar Activity, the activity type is DatabricksSparkJar.</span></span>|<span data-ttu-id="5b84d-123">Yes</span><span class="sxs-lookup"><span data-stu-id="5b84d-123">Yes</span></span>|
|<span data-ttu-id="5b84d-124">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="5b84d-124">linkedServiceName</span></span>|<span data-ttu-id="5b84d-125">Name of the Databricks Linked Service on which the Jar activity runs.</span><span class="sxs-lookup"><span data-stu-id="5b84d-125">Name of the Databricks Linked Service on which the Jar activity runs.</span></span> <span data-ttu-id="5b84d-126">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="5b84d-126">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span>|<span data-ttu-id="5b84d-127">Yes</span><span class="sxs-lookup"><span data-stu-id="5b84d-127">Yes</span></span>|
|<span data-ttu-id="5b84d-128">mainClassName</span><span class="sxs-lookup"><span data-stu-id="5b84d-128">mainClassName</span></span>|<span data-ttu-id="5b84d-129">The full name of the class containing the main method to be executed.</span><span class="sxs-lookup"><span data-stu-id="5b84d-129">The full name of the class containing the main method to be executed.</span></span> <span data-ttu-id="5b84d-130">This class must be contained in a JAR provided as a library.</span><span class="sxs-lookup"><span data-stu-id="5b84d-130">This class must be contained in a JAR provided as a library.</span></span>|<span data-ttu-id="5b84d-131">Yes</span><span class="sxs-lookup"><span data-stu-id="5b84d-131">Yes</span></span>|
|<span data-ttu-id="5b84d-132">parameters</span><span class="sxs-lookup"><span data-stu-id="5b84d-132">parameters</span></span>|<span data-ttu-id="5b84d-133">Parameters that will be passed to the main method.</span><span class="sxs-lookup"><span data-stu-id="5b84d-133">Parameters that will be passed to the main method.</span></span>  <span data-ttu-id="5b84d-134">This is an array of strings.</span><span class="sxs-lookup"><span data-stu-id="5b84d-134">This is an array of strings.</span></span>|<span data-ttu-id="5b84d-135">No</span><span class="sxs-lookup"><span data-stu-id="5b84d-135">No</span></span>|
|<span data-ttu-id="5b84d-136">libraries</span><span class="sxs-lookup"><span data-stu-id="5b84d-136">libraries</span></span>|<span data-ttu-id="5b84d-137">A list of libraries to be installed on the cluster that will execute the job.</span><span class="sxs-lookup"><span data-stu-id="5b84d-137">A list of libraries to be installed on the cluster that will execute the job.</span></span> <span data-ttu-id="5b84d-138">It can be an array of <string, object></span><span class="sxs-lookup"><span data-stu-id="5b84d-138">It can be an array of <string, object></span></span>|<span data-ttu-id="5b84d-139">Yes (at least one containing the mainClassName method)</span><span class="sxs-lookup"><span data-stu-id="5b84d-139">Yes (at least one containing the mainClassName method)</span></span>|

## <a name="supported-libraries-for-databricks-activities"></a><span data-ttu-id="5b84d-140">Supported libraries for databricks activities</span><span class="sxs-lookup"><span data-stu-id="5b84d-140">Supported libraries for databricks activities</span></span>

<span data-ttu-id="5b84d-141">In the above Databricks activity definition you specify these library types: *jar*, *egg*, *maven*, *pypi*, *cran*.</span><span class="sxs-lookup"><span data-stu-id="5b84d-141">In the above Databricks activity definition you specify these library types: *jar*, *egg*, *maven*, *pypi*, *cran*.</span></span>

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

<span data-ttu-id="5b84d-142">For more details refer [Databricks documentation](https://docs.azuredatabricks.net/api/latest/libraries.html#managedlibrarieslibrary) for library types.</span><span class="sxs-lookup"><span data-stu-id="5b84d-142">For more details refer [Databricks documentation](https://docs.azuredatabricks.net/api/latest/libraries.html#managedlibrarieslibrary) for library types.</span></span>

## <a name="how-to-upload-a-library-in-databricks"></a><span data-ttu-id="5b84d-143">How to upload a library in Databricks</span><span class="sxs-lookup"><span data-stu-id="5b84d-143">How to upload a library in Databricks</span></span>

#### <a name="using-databricks-workspace-uihttpsdocsazuredatabricksnetuser-guidelibrarieshtmlcreate-a-library"></a>[<span data-ttu-id="5b84d-144">Using Databricks workspace UI</span><span class="sxs-lookup"><span data-stu-id="5b84d-144">Using Databricks workspace UI</span></span>](https://docs.azuredatabricks.net/user-guide/libraries.html#create-a-library)

<span data-ttu-id="5b84d-145">To obtain the dbfs path of the library added using UI, you can use [Databricks CLI (installation)](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#install-the-cli).</span><span class="sxs-lookup"><span data-stu-id="5b84d-145">To obtain the dbfs path of the library added using UI, you can use [Databricks CLI (installation)](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#install-the-cli).</span></span> 

<span data-ttu-id="5b84d-146">Typically the Jar libraries are stored under dbfs:/FileStore/jars while using the UI.</span><span class="sxs-lookup"><span data-stu-id="5b84d-146">Typically the Jar libraries are stored under dbfs:/FileStore/jars while using the UI.</span></span> <span data-ttu-id="5b84d-147">You can list all through the CLI: *databricks fs ls dbfs:/FileStore/job-jars*</span><span class="sxs-lookup"><span data-stu-id="5b84d-147">You can list all through the CLI: *databricks fs ls dbfs:/FileStore/job-jars*</span></span> 



#### <a name="copy-library-using-databricks-clihttpsdocsazuredatabricksnetuser-guidedev-toolsdatabricks-clihtmlcopy-a-file-to-dbfs"></a>[<span data-ttu-id="5b84d-148">Copy library using Databricks CLI</span><span class="sxs-lookup"><span data-stu-id="5b84d-148">Copy library using Databricks CLI</span></span>](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#copy-a-file-to-dbfs)
<span data-ttu-id="5b84d-149">Use Databricks CLI [(installation steps)](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#install-the-cli).</span><span class="sxs-lookup"><span data-stu-id="5b84d-149">Use Databricks CLI [(installation steps)](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#install-the-cli).</span></span> 

<span data-ttu-id="5b84d-150">Example - copying JAR to dbfs: *dbfs cp SparkPi-assembly-0.1.jar dbfs:/docs/sparkpi.jar*</span><span class="sxs-lookup"><span data-stu-id="5b84d-150">Example - copying JAR to dbfs: *dbfs cp SparkPi-assembly-0.1.jar dbfs:/docs/sparkpi.jar*</span></span>
