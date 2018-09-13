---
title: How to use Power BI Embedded with REST | Microsoft Docs
description: 'Learn how to use Power BI Embedded with REST '
services: power-bi-embedded
documentationcenter: ''
author: guyinacube
manager: erikre
editor: ''
tags: ''
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 447926840628b7b47a9ba6e7a90a39ae1e31718a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555270"
---
# <a name="how-to-use-power-bi-embedded-with-rest"></a><span data-ttu-id="be941-103">How to use Power BI Embedded with REST</span><span class="sxs-lookup"><span data-stu-id="be941-103">How to use Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="be941-104">Power BI Embedded: What it is and what it's for</span><span class="sxs-lookup"><span data-stu-id="be941-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="be941-105">An overview of Power BI Embedded is described in the official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into the details about using it with REST.</span><span class="sxs-lookup"><span data-stu-id="be941-105">An overview of Power BI Embedded is described in the official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into the details about using it with REST.</span></span>

<span data-ttu-id="be941-106">It's quite simple, really.</span><span class="sxs-lookup"><span data-stu-id="be941-106">It's quite simple, really.</span></span> <span data-ttu-id="be941-107">you may want to use the dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span><span class="sxs-lookup"><span data-stu-id="be941-107">you may want to use the dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="be941-108">Most custom applications need to deliver the data for their own customers, not necessarily users in their own organization.</span><span class="sxs-lookup"><span data-stu-id="be941-108">Most custom applications need to deliver the data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="be941-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, the multi-tenancy is needed for the delivery.</span><span class="sxs-lookup"><span data-stu-id="be941-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, the multi-tenancy is needed for the delivery.</span></span>

<span data-ttu-id="be941-110">The custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span><span class="sxs-lookup"><span data-stu-id="be941-110">The custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="be941-111">Then, the embedding solution must collaborate with this existing authentication methods safely.</span><span class="sxs-lookup"><span data-stu-id="be941-111">Then, the embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="be941-112">It's also necessary for users to be able to use those ISV applications without the extra purchase or licensing of a Power BI subscription.</span><span class="sxs-lookup"><span data-stu-id="be941-112">It's also necessary for users to be able to use those ISV applications without the extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="be941-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span><span class="sxs-lookup"><span data-stu-id="be941-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="be941-114">So, now that we have that quick introduction out of the way, let's get into some details</span><span class="sxs-lookup"><span data-stu-id="be941-114">So, now that we have that quick introduction out of the way, let's get into some details</span></span>

<span data-ttu-id="be941-115">You can use the .NET \(C#) or Node.js SDK, to easily build your application with Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="be941-115">You can use the .NET \(C#) or Node.js SDK, to easily build your application with Power BI Embedded.</span></span> <span data-ttu-id="be941-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span><span class="sxs-lookup"><span data-stu-id="be941-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="be941-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply the essence of Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="be941-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply the essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="be941-118">Create Power BI workspace collection, and get access key \(Provisioning)</span><span class="sxs-lookup"><span data-stu-id="be941-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="be941-119">Power BI Embedded is one of the Azure services.</span><span class="sxs-lookup"><span data-stu-id="be941-119">Power BI Embedded is one of the Azure services.</span></span> <span data-ttu-id="be941-120">Only the ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and the user who views the report isn't charged or even require an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="be941-120">Only the ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and the user who views the report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="be941-121">Before starting our application development, we must create the **Power BI workspace collection** by using Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="be941-121">Before starting our application development, we must create the **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="be941-122">Each workspace of Power BI Embedded is the workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span><span class="sxs-lookup"><span data-stu-id="be941-122">Each workspace of Power BI Embedded is the workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="be941-123">The same access key is used in each workspace collection.</span><span class="sxs-lookup"><span data-stu-id="be941-123">The same access key is used in each workspace collection.</span></span> <span data-ttu-id="be941-124">In-effect, the workspace collection is the security boundary for Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="be941-124">In-effect, the workspace collection is the security boundary for Power BI Embedded.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="be941-125">When we finish creating the workspace collection, copy the access key from Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="be941-125">When we finish creating the workspace collection, copy the access key from Azure Portal.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="be941-126">We can also provision the workspace collection and get access key via REST API.</span><span class="sxs-lookup"><span data-stu-id="be941-126">We can also provision the workspace collection and get access key via REST API.</span></span> <span data-ttu-id="be941-127">To learn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="be941-127">To learn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="be941-128">Create .pbix file with Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="be941-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="be941-129">Next, we must create the data connection and reports to be embedded.</span><span class="sxs-lookup"><span data-stu-id="be941-129">Next, we must create the data connection and reports to be embedded.</span></span>
<span data-ttu-id="be941-130">For this task, there’s no programming or code.</span><span class="sxs-lookup"><span data-stu-id="be941-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="be941-131">We just use Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="be941-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="be941-132">In this article, we won't go through the details about how to use Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="be941-132">In this article, we won't go through the details about how to use Power BI Desktop.</span></span> <span data-ttu-id="be941-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="be941-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="be941-134">For our example, we'll just use the [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="be941-134">For our example, we'll just use the [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="be941-135">Create a Power BI workspace</span><span class="sxs-lookup"><span data-stu-id="be941-135">Create a Power BI workspace</span></span>

<span data-ttu-id="be941-136">Now that the provisioning is all done, let’s get started creating a customer’s workspace in the workspace collection via REST APIs.</span><span class="sxs-lookup"><span data-stu-id="be941-136">Now that the provisioning is all done, let’s get started creating a customer’s workspace in the workspace collection via REST APIs.</span></span> <span data-ttu-id="be941-137">The following HTTP POST Request (REST) is creating the new workspace in our existing workspace collection.</span><span class="sxs-lookup"><span data-stu-id="be941-137">The following HTTP POST Request (REST) is creating the new workspace in our existing workspace collection.</span></span> <span data-ttu-id="be941-138">This is the [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="be941-138">This is the [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="be941-139">In our example, the workspace collection name is **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="be941-139">In our example, the workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="be941-140">We just set the access key, which we previously copied, as **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="be941-140">We just set the access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="be941-141">It’s very simple authentication!</span><span class="sxs-lookup"><span data-stu-id="be941-141">It’s very simple authentication!</span></span>

<span data-ttu-id="be941-142">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="be941-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="be941-143">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="be941-143">**HTTP Response**</span></span>

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

<span data-ttu-id="be941-144">The returned **workspaceId** is used for the following subsequent API calls.</span><span class="sxs-lookup"><span data-stu-id="be941-144">The returned **workspaceId** is used for the following subsequent API calls.</span></span> <span data-ttu-id="be941-145">Our application must retain this value.</span><span class="sxs-lookup"><span data-stu-id="be941-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-the-workspace"></a><span data-ttu-id="be941-146">Import .pbix file into the workspace</span><span class="sxs-lookup"><span data-stu-id="be941-146">Import .pbix file into the workspace</span></span>

<span data-ttu-id="be941-147">Each report in a workspace corresponds to a single Power BI Desktop file with a dataset \(including datasource settings).</span><span class="sxs-lookup"><span data-stu-id="be941-147">Each report in a workspace corresponds to a single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="be941-148">We can import our .pbix file to the workspace as shown in the code below.</span><span class="sxs-lookup"><span data-stu-id="be941-148">We can import our .pbix file to the workspace as shown in the code below.</span></span> <span data-ttu-id="be941-149">As you can see, we can upload the binary of .pbix file using MIME multipart in http.</span><span class="sxs-lookup"><span data-stu-id="be941-149">As you can see, we can upload the binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="be941-150">The uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is the workspaceId, and query parameter **datasetDisplayName** is the dataset name to create.</span><span class="sxs-lookup"><span data-stu-id="be941-150">The uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is the workspaceId, and query parameter **datasetDisplayName** is the dataset name to create.</span></span> <span data-ttu-id="be941-151">The created dataset holds all data related artifacts in .pbix file such as imported data, the pointer to the data source, etc..</span><span class="sxs-lookup"><span data-stu-id="be941-151">The created dataset holds all data related artifacts in .pbix file such as imported data, the pointer to the data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{the content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="be941-152">This import task might run for a while.</span><span class="sxs-lookup"><span data-stu-id="be941-152">This import task might run for a while.</span></span> <span data-ttu-id="be941-153">When complete, our application can ask the task status using import id. In our example, the import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="be941-153">When complete, our application can ask the task status using import id. In our example, the import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="be941-154">The following is asking status using this import id:</span><span class="sxs-lookup"><span data-stu-id="be941-154">The following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="be941-155">If the task isn't complete, the HTTP response could be like this:</span><span class="sxs-lookup"><span data-stu-id="be941-155">If the task isn't complete, the HTTP response could be like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

<span data-ttu-id="be941-156">If the task is complete, the HTTP response could be more like this:</span><span class="sxs-lookup"><span data-stu-id="be941-156">If the task is complete, the HTTP response could be more like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="be941-157">Data source connectivity \(and multi-tenancy of data)</span><span class="sxs-lookup"><span data-stu-id="be941-157">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="be941-158">While almost all of the artifacts in .pbix file are imported into our workspace, the  credentials for data sources are not.</span><span class="sxs-lookup"><span data-stu-id="be941-158">While almost all of the artifacts in .pbix file are imported into our workspace, the  credentials for data sources are not.</span></span> <span data-ttu-id="be941-159">As a result, when using **DirectQuery mode**, the embedded report cannot be shown correctly.</span><span class="sxs-lookup"><span data-stu-id="be941-159">As a result, when using **DirectQuery mode**, the embedded report cannot be shown correctly.</span></span> <span data-ttu-id="be941-160">But, when using **Import mode**, we can view the report using the existing imported data.</span><span class="sxs-lookup"><span data-stu-id="be941-160">But, when using **Import mode**, we can view the report using the existing imported data.</span></span> <span data-ttu-id="be941-161">In such a case, we must set the credential using the following steps via REST calls.</span><span class="sxs-lookup"><span data-stu-id="be941-161">In such a case, we must set the credential using the following steps via REST calls.</span></span>

<span data-ttu-id="be941-162">First, we must get the gateway datasource.</span><span class="sxs-lookup"><span data-stu-id="be941-162">First, we must get the gateway datasource.</span></span> <span data-ttu-id="be941-163">We know the dataset **id** is the previously returned id.</span><span class="sxs-lookup"><span data-stu-id="be941-163">We know the dataset **id** is the previously returned id.</span></span>

<span data-ttu-id="be941-164">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="be941-164">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="be941-165">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="be941-165">**HTTP Response**</span></span>

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

<span data-ttu-id="be941-166">Using the returned gateway id and datasource id \(see the previous **gatewayId** and **id** in the returned result), we can change the credential of this datasource as follows:</span><span class="sxs-lookup"><span data-stu-id="be941-166">Using the returned gateway id and datasource id \(see the previous **gatewayId** and **id** in the returned result), we can change the credential of this datasource as follows:</span></span>

<span data-ttu-id="be941-167">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="be941-167">**HTTP Request**</span></span>

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

<span data-ttu-id="be941-168">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="be941-168">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="be941-169">In production, we can also set the different connection string for each workspace using REST API.</span><span class="sxs-lookup"><span data-stu-id="be941-169">In production, we can also set the different connection string for each workspace using REST API.</span></span> <span data-ttu-id="be941-170">\(i.e, we can separate the database for each customers.)</span><span class="sxs-lookup"><span data-stu-id="be941-170">\(i.e, we can separate the database for each customers.)</span></span>

<span data-ttu-id="be941-171">The following is changing the connection string of datasource via REST.</span><span class="sxs-lookup"><span data-stu-id="be941-171">The following is changing the connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="be941-172">Or, we can use Row Level Security in Power BI Embedded and we can separate the data for each users in one report.</span><span class="sxs-lookup"><span data-stu-id="be941-172">Or, we can use Row Level Security in Power BI Embedded and we can separate the data for each users in one report.</span></span> <span data-ttu-id="be941-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span><span class="sxs-lookup"><span data-stu-id="be941-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="be941-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way to refresh models via API.</span><span class="sxs-lookup"><span data-stu-id="be941-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way to refresh models via API.</span></span> <span data-ttu-id="be941-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="be941-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="be941-176">However, you'll really want to keep an eye on the [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span><span class="sxs-lookup"><span data-stu-id="be941-176">However, you'll really want to keep an eye on the [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="be941-177">Authentication and hosting (embedding) reports in our web page</span><span class="sxs-lookup"><span data-stu-id="be941-177">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="be941-178">In the previous REST API, we can use the access key **AppKey** itself as the authorization header.</span><span class="sxs-lookup"><span data-stu-id="be941-178">In the previous REST API, we can use the access key **AppKey** itself as the authorization header.</span></span> <span data-ttu-id="be941-179">Because these calls can be handled on the backend server side, it's safe.</span><span class="sxs-lookup"><span data-stu-id="be941-179">Because these calls can be handled on the backend server side, it's safe.</span></span>

<span data-ttu-id="be941-180">But, when we embed the report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span><span class="sxs-lookup"><span data-stu-id="be941-180">But, when we embed the report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="be941-181">Then the authorization header value must be secured.</span><span class="sxs-lookup"><span data-stu-id="be941-181">Then the authorization header value must be secured.</span></span> <span data-ttu-id="be941-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span><span class="sxs-lookup"><span data-stu-id="be941-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="be941-183">When we embed the report in our web page, we must use the computed token instead of access key **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="be941-183">When we embed the report in our web page, we must use the computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="be941-184">Our application must create the OAuth Json Web Token \(JWT) which consists of the claims and the computed digital signature.</span><span class="sxs-lookup"><span data-stu-id="be941-184">Our application must create the OAuth Json Web Token \(JWT) which consists of the claims and the computed digital signature.</span></span> <span data-ttu-id="be941-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span><span class="sxs-lookup"><span data-stu-id="be941-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="be941-186">First, we must prepare the input value, which is signed later.</span><span class="sxs-lookup"><span data-stu-id="be941-186">First, we must prepare the input value, which is signed later.</span></span> <span data-ttu-id="be941-187">This value is the base64 url encoded (rfc4648) string of the following json, and these are delimited by the dot \(.) character.</span><span class="sxs-lookup"><span data-stu-id="be941-187">This value is the base64 url encoded (rfc4648) string of the following json, and these are delimited by the dot \(.) character.</span></span> <span data-ttu-id="be941-188">Later, we'll explain how to get the report id.</span><span class="sxs-lookup"><span data-stu-id="be941-188">Later, we'll explain how to get the report id.</span></span>

> [!NOTE]
> <span data-ttu-id="be941-189">If we want to use Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in the claims.</span><span class="sxs-lookup"><span data-stu-id="be941-189">If we want to use Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in the claims.</span></span>

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

<span data-ttu-id="be941-190">Next, we must create the base64 encoded string of HMAC \(the signature) with SHA256 algorithm.</span><span class="sxs-lookup"><span data-stu-id="be941-190">Next, we must create the base64 encoded string of HMAC \(the signature) with SHA256 algorithm.</span></span> <span data-ttu-id="be941-191">This signed input value is the previous string.</span><span class="sxs-lookup"><span data-stu-id="be941-191">This signed input value is the previous string.</span></span>

<span data-ttu-id="be941-192">Last, we must combine the input value and signature string using period \(.) character.</span><span class="sxs-lookup"><span data-stu-id="be941-192">Last, we must combine the input value and signature string using period \(.) character.</span></span> <span data-ttu-id="be941-193">The completed string is the app token for the report embedding.</span><span class="sxs-lookup"><span data-stu-id="be941-193">The completed string is the app token for the report embedding.</span></span> <span data-ttu-id="be941-194">Even if the app token is discovered by a malicious user, they cannot get the original access key.</span><span class="sxs-lookup"><span data-stu-id="be941-194">Even if the app token is discovered by a malicious user, they cannot get the original access key.</span></span> <span data-ttu-id="be941-195">This app token will expire quickly.</span><span class="sxs-lookup"><span data-stu-id="be941-195">This app token will expire quickly.</span></span>

<span data-ttu-id="be941-196">Here's a PHP example for these steps:</span><span class="sxs-lookup"><span data-stu-id="be941-196">Here's a PHP example for these steps:</span></span>

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is the apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-the-report-into-the-web-page"></a><span data-ttu-id="be941-197">Finally, embed the report into the web page</span><span class="sxs-lookup"><span data-stu-id="be941-197">Finally, embed the report into the web page</span></span>

<span data-ttu-id="be941-198">For embedding our report, we must get the embed url and report **id** using the following REST API.</span><span class="sxs-lookup"><span data-stu-id="be941-198">For embedding our report, we must get the embed url and report **id** using the following REST API.</span></span>

<span data-ttu-id="be941-199">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="be941-199">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="be941-200">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="be941-200">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

<span data-ttu-id="be941-201">We can embed the report in our web app using the previous app token.</span><span class="sxs-lookup"><span data-stu-id="be941-201">We can embed the report in our web app using the previous app token.</span></span>
<span data-ttu-id="be941-202">If we look at the next sample code, the former part is the same as the previous example.</span><span class="sxs-lookup"><span data-stu-id="be941-202">If we look at the next sample code, the former part is the same as the previous example.</span></span> <span data-ttu-id="be941-203">In the latter part, this sample shows the **embedUrl** \(see the previous result) in the iframe, and is posting the app token into the iframe.</span><span class="sxs-lookup"><span data-stu-id="be941-203">In the latter part, this sample shows the **embedUrl** \(see the previous result) in the iframe, and is posting the app token into the iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="be941-204">You'll need to change the report id value to one of your own.</span><span class="sxs-lookup"><span data-stu-id="be941-204">You'll need to change the report id value to one of your own.</span></span> <span data-ttu-id="be941-205">Also, due to a bug in our content management system, the iframe tag in the code sample is read literally.</span><span class="sxs-lookup"><span data-stu-id="be941-205">Also, due to a bug in our content management system, the iframe tag in the code sample is read literally.</span></span> <span data-ttu-id="be941-206">Remove the capped text from the tag if you copy and paste this sample code.</span><span class="sxs-lookup"><span data-stu-id="be941-206">Remove the capped text from the tag if you copy and paste this sample code.</span></span>

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

<span data-ttu-id="be941-207">And here's our result:</span><span class="sxs-lookup"><span data-stu-id="be941-207">And here's our result:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="be941-208">At this time, Power BI Embedded only shows the report in the iframe.</span><span class="sxs-lookup"><span data-stu-id="be941-208">At this time, Power BI Embedded only shows the report in the iframe.</span></span> <span data-ttu-id="be941-209">But, keep an eye on the [Power BI Blog](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="be941-209">But, keep an eye on the [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="be941-210">Future improvements could use new client side APIs that will let us send information into the iframe as well as get information out. Exciting stuff!</span><span class="sxs-lookup"><span data-stu-id="be941-210">Future improvements could use new client side APIs that will let us send information into the iframe as well as get information out. Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="be941-211">See also</span><span class="sxs-lookup"><span data-stu-id="be941-211">See also</span></span>
* [<span data-ttu-id="be941-212">Authenticating and authorizing in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="be941-212">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="be941-213">More questions?</span><span class="sxs-lookup"><span data-stu-id="be941-213">More questions?</span></span> [<span data-ttu-id="be941-214">Try the Power BI Community</span><span class="sxs-lookup"><span data-stu-id="be941-214">Try the Power BI Community</span></span>](http://community.powerbi.com/)






