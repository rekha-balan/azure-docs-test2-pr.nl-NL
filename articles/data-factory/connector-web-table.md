---
title: Copy data from Web Table using Azure Data Factory | Microsoft Docs
description: Learn about Web Table Connector of Azure Data Factory that lets you copy data from a web table to data stores supported by Data Factory as sinks.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/28/2018
ms.author: jingwang
ms.openlocfilehash: 995bf4586b88671c65077d965b0588de8de74e5c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968886"
---
# <a name="copy-data-from-web-table-by-using-azure-data-factory"></a><span data-ttu-id="240e1-103">Copy data from Web table by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="240e1-103">Copy data from Web table by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-web-table-connector.md)
> * [Current version](connector-web-table.md)

<span data-ttu-id="240e1-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a Web table database.</span><span class="sxs-lookup"><span data-stu-id="240e1-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a Web table database.</span></span> <span data-ttu-id="240e1-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="240e1-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="240e1-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="240e1-108">Supported capabilities</span></span>

<span data-ttu-id="240e1-109">You can copy data from Web table database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="240e1-109">You can copy data from Web table database to any supported sink data store.</span></span> <span data-ttu-id="240e1-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="240e1-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="240e1-111">Specifically, this Web table connector supports **extracting table content from an HTML page**.</span><span class="sxs-lookup"><span data-stu-id="240e1-111">Specifically, this Web table connector supports **extracting table content from an HTML page**.</span></span> <span data-ttu-id="240e1-112">To retrieve data from a HTTP/s endpoint, use [HTTP connector](connector-http.md) instead.</span><span class="sxs-lookup"><span data-stu-id="240e1-112">To retrieve data from a HTTP/s endpoint, use [HTTP connector](connector-http.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="240e1-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="240e1-113">Prerequisites</span></span>

<span data-ttu-id="240e1-114">To use this Web table connector, you need to set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="240e1-114">To use this Web table connector, you need to set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="240e1-115">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="240e1-115">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="240e1-116">Getting started</span><span class="sxs-lookup"><span data-stu-id="240e1-116">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="240e1-117">The following sections provide details about properties that are used to define Data Factory entities specific to Web table connector.</span><span class="sxs-lookup"><span data-stu-id="240e1-117">The following sections provide details about properties that are used to define Data Factory entities specific to Web table connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="240e1-118">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="240e1-118">Linked service properties</span></span>

<span data-ttu-id="240e1-119">The following properties are supported for Web table linked service:</span><span class="sxs-lookup"><span data-stu-id="240e1-119">The following properties are supported for Web table linked service:</span></span>

| <span data-ttu-id="240e1-120">Property</span><span class="sxs-lookup"><span data-stu-id="240e1-120">Property</span></span> | <span data-ttu-id="240e1-121">Description</span><span class="sxs-lookup"><span data-stu-id="240e1-121">Description</span></span> | <span data-ttu-id="240e1-122">Required</span><span class="sxs-lookup"><span data-stu-id="240e1-122">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="240e1-123">type</span><span class="sxs-lookup"><span data-stu-id="240e1-123">type</span></span> | <span data-ttu-id="240e1-124">The type property must be set to: **Web**</span><span class="sxs-lookup"><span data-stu-id="240e1-124">The type property must be set to: **Web**</span></span> |<span data-ttu-id="240e1-125">Yes</span><span class="sxs-lookup"><span data-stu-id="240e1-125">Yes</span></span> |
| <span data-ttu-id="240e1-126">url</span><span class="sxs-lookup"><span data-stu-id="240e1-126">url</span></span> | <span data-ttu-id="240e1-127">URL to the Web source</span><span class="sxs-lookup"><span data-stu-id="240e1-127">URL to the Web source</span></span> |<span data-ttu-id="240e1-128">Yes</span><span class="sxs-lookup"><span data-stu-id="240e1-128">Yes</span></span> |
| <span data-ttu-id="240e1-129">authenticationType</span><span class="sxs-lookup"><span data-stu-id="240e1-129">authenticationType</span></span> | <span data-ttu-id="240e1-130">Allowed value is: **Anonymous**.</span><span class="sxs-lookup"><span data-stu-id="240e1-130">Allowed value is: **Anonymous**.</span></span> |<span data-ttu-id="240e1-131">Yes</span><span class="sxs-lookup"><span data-stu-id="240e1-131">Yes</span></span> |
| <span data-ttu-id="240e1-132">connectVia</span><span class="sxs-lookup"><span data-stu-id="240e1-132">connectVia</span></span> | <span data-ttu-id="240e1-133">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="240e1-133">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="240e1-134">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="240e1-134">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span></span> |<span data-ttu-id="240e1-135">Yes</span><span class="sxs-lookup"><span data-stu-id="240e1-135">Yes</span></span> |

<span data-ttu-id="240e1-136">**Example:**</span><span class="sxs-lookup"><span data-stu-id="240e1-136">**Example:**</span></span>

```json
{
    "name": "WebLinkedService",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "url" : "https://en.wikipedia.org/wiki/",
            "authenticationType": "Anonymous"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="240e1-137">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="240e1-137">Dataset properties</span></span>

<span data-ttu-id="240e1-138">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="240e1-138">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="240e1-139">This section provides a list of properties supported by Web table dataset.</span><span class="sxs-lookup"><span data-stu-id="240e1-139">This section provides a list of properties supported by Web table dataset.</span></span>

<span data-ttu-id="240e1-140">To copy data from Web table, set the type property of the dataset to **WebTable**.</span><span class="sxs-lookup"><span data-stu-id="240e1-140">To copy data from Web table, set the type property of the dataset to **WebTable**.</span></span> <span data-ttu-id="240e1-141">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="240e1-141">The following properties are supported:</span></span>

| <span data-ttu-id="240e1-142">Property</span><span class="sxs-lookup"><span data-stu-id="240e1-142">Property</span></span> | <span data-ttu-id="240e1-143">Description</span><span class="sxs-lookup"><span data-stu-id="240e1-143">Description</span></span> | <span data-ttu-id="240e1-144">Required</span><span class="sxs-lookup"><span data-stu-id="240e1-144">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="240e1-145">type</span><span class="sxs-lookup"><span data-stu-id="240e1-145">type</span></span> | <span data-ttu-id="240e1-146">The type property of the dataset must be set to: **WebTable**</span><span class="sxs-lookup"><span data-stu-id="240e1-146">The type property of the dataset must be set to: **WebTable**</span></span> | <span data-ttu-id="240e1-147">Yes</span><span class="sxs-lookup"><span data-stu-id="240e1-147">Yes</span></span> |
| <span data-ttu-id="240e1-148">path</span><span class="sxs-lookup"><span data-stu-id="240e1-148">path</span></span> |<span data-ttu-id="240e1-149">A relative URL to the resource that contains the table.</span><span class="sxs-lookup"><span data-stu-id="240e1-149">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="240e1-150">No.</span><span class="sxs-lookup"><span data-stu-id="240e1-150">No.</span></span> <span data-ttu-id="240e1-151">When path is not specified, only the URL specified in the linked service definition is used.</span><span class="sxs-lookup"><span data-stu-id="240e1-151">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="240e1-152">index</span><span class="sxs-lookup"><span data-stu-id="240e1-152">index</span></span> |<span data-ttu-id="240e1-153">The index of the table in the resource.</span><span class="sxs-lookup"><span data-stu-id="240e1-153">The index of the table in the resource.</span></span> <span data-ttu-id="240e1-154">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span><span class="sxs-lookup"><span data-stu-id="240e1-154">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="240e1-155">Yes</span><span class="sxs-lookup"><span data-stu-id="240e1-155">Yes</span></span> |

<span data-ttu-id="240e1-156">**Example:**</span><span class="sxs-lookup"><span data-stu-id="240e1-156">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": {
            "referenceName": "<Web linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="240e1-157">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="240e1-157">Copy activity properties</span></span>

<span data-ttu-id="240e1-158">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="240e1-158">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="240e1-159">This section provides a list of properties supported by Web table source.</span><span class="sxs-lookup"><span data-stu-id="240e1-159">This section provides a list of properties supported by Web table source.</span></span>

### <a name="web-table-as-source"></a><span data-ttu-id="240e1-160">Web table as source</span><span class="sxs-lookup"><span data-stu-id="240e1-160">Web table as source</span></span>

<span data-ttu-id="240e1-161">To copy data from Web table, set the source type in the copy activity to **WebSource**, no additional properties are supported.</span><span class="sxs-lookup"><span data-stu-id="240e1-161">To copy data from Web table, set the source type in the copy activity to **WebSource**, no additional properties are supported.</span></span>

<span data-ttu-id="240e1-162">**Example:**</span><span class="sxs-lookup"><span data-stu-id="240e1-162">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromWebTable",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Web table input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "WebSource"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="240e1-163">Get index of a table in an HTML page</span><span class="sxs-lookup"><span data-stu-id="240e1-163">Get index of a table in an HTML page</span></span>

<span data-ttu-id="240e1-164">To get the index of a table which you need to configure in [dataset properties](#dataset-properties), you can use e.g. Excel 2016 as the tool as follows:</span><span class="sxs-lookup"><span data-stu-id="240e1-164">To get the index of a table which you need to configure in [dataset properties](#dataset-properties), you can use e.g. Excel 2016 as the tool as follows:</span></span>

1. <span data-ttu-id="240e1-165">Launch **Excel 2016** and switch to the **Data** tab.</span><span class="sxs-lookup"><span data-stu-id="240e1-165">Launch **Excel 2016** and switch to the **Data** tab.</span></span>
2. <span data-ttu-id="240e1-166">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span><span class="sxs-lookup"><span data-stu-id="240e1-166">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span></span>

    ![Power Query menu](./media/copy-data-from-web-table/PowerQuery-Menu.png)
3. <span data-ttu-id="240e1-168">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="240e1-168">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![From Web dialog](./media/copy-data-from-web-table/FromWeb-DialogBox.png)

    <span data-ttu-id="240e1-170">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="240e1-170">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="240e1-171">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="240e1-171">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Access Web content dialog box](./media/copy-data-from-web-table/AccessWebContentDialog.png)
5. <span data-ttu-id="240e1-173">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span><span class="sxs-lookup"><span data-stu-id="240e1-173">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span></span>  

   ![Navigator dialog](./media/copy-data-from-web-table/Navigator-DialogBox.png)
6. <span data-ttu-id="240e1-175">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="240e1-175">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span></span>

    ![Advanced Editor button](./media/copy-data-from-web-table/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="240e1-177">In the Advanced Editor dialog box, the number next to "Source" is the index.</span><span class="sxs-lookup"><span data-stu-id="240e1-177">In the Advanced Editor dialog box, the number next to "Source" is the index.</span></span>

    ![Advanced Editor - Index](./media/copy-data-from-web-table/AdvancedEditor-Index.png)

<span data-ttu-id="240e1-179">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span><span class="sxs-lookup"><span data-stu-id="240e1-179">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span></span> <span data-ttu-id="240e1-180">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span><span class="sxs-lookup"><span data-stu-id="240e1-180">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="240e1-181">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="240e1-181">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>


## <a name="next-steps"></a><span data-ttu-id="240e1-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="240e1-182">Next steps</span></span>
<span data-ttu-id="240e1-183">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="240e1-183">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
