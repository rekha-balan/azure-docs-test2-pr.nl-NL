---
title: Stream Analytics Data Lake Store Output | Microsoft Docs
description: Configuration of authentication and authorization of an Azure Data Lake Store in a Stream Analytics job
keywords: ''
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 667c21ad1c3c3f5910040efd356af22df0854f61
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540646"
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="ecc32-103">Stream Analytics Data Lake Store output</span><span class="sxs-lookup"><span data-stu-id="ecc32-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="ecc32-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="ecc32-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="ecc32-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span><span class="sxs-lookup"><span data-stu-id="ecc32-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="ecc32-106">Data Lake Store enables you to store data of any size, type and ingestion speed for operational and exploratory analytics.</span><span class="sxs-lookup"><span data-stu-id="ecc32-106">Data Lake Store enables you to store data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="ecc32-107">Authorize a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="ecc32-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="ecc32-108">When Data Lake Store is selected as an output in the Azure Management portal, you will be prompted to authorize the usage of your existing Data Lake Store or to request access to the Data Lake Store via the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="ecc32-108">When Data Lake Store is selected as an output in the Azure Management portal, you will be prompted to authorize the usage of your existing Data Lake Store or to request access to the Data Lake Store via the Azure Classic Portal.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="ecc32-109">If you already have access to Data Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span><span class="sxs-lookup"><span data-stu-id="ecc32-109">If you already have access to Data Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span></span> <span data-ttu-id="ecc32-110">The page will automatically close and you will be presented with the page that would allow you to configure the Data Lake Store output.</span><span class="sxs-lookup"><span data-stu-id="ecc32-110">The page will automatically close and you will be presented with the page that would allow you to configure the Data Lake Store output.</span></span>

<span data-ttu-id="ecc32-111">If you have not signed up for Data Lake Store, you can follow the “Sign up now” link to initiate the request, or follow the [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ecc32-111">If you have not signed up for Data Lake Store, you can follow the “Sign up now” link to initiate the request, or follow the [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-the-data-lake-store-output-properties"></a><span data-ttu-id="ecc32-112">Configure the Data Lake Store output properties</span><span class="sxs-lookup"><span data-stu-id="ecc32-112">Configure the Data Lake Store output properties</span></span>
<span data-ttu-id="ecc32-113">Once you have the Data Lake Store account authenticated, you can configure the properties for your Data Lake Store output.</span><span class="sxs-lookup"><span data-stu-id="ecc32-113">Once you have the Data Lake Store account authenticated, you can configure the properties for your Data Lake Store output.</span></span> <span data-ttu-id="ecc32-114">The table below is the list of property names and their description to configure your Data Lake Store output.</span><span class="sxs-lookup"><span data-stu-id="ecc32-114">The table below is the list of property names and their description to configure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="ecc32-115"><B>PROPERTY NAME</B></span><span class="sxs-lookup"><span data-stu-id="ecc32-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="ecc32-116"><B>DESCRIPTION</B></span><span class="sxs-lookup"><span data-stu-id="ecc32-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ecc32-117">Output Alias</span><span class="sxs-lookup"><span data-stu-id="ecc32-117">Output Alias</span></span></td>
<td><span data-ttu-id="ecc32-118">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ecc32-118">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ecc32-119">Data Lake Store Account</span><span class="sxs-lookup"><span data-stu-id="ecc32-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="ecc32-120">The name of the storage account where you are sending your output.</span><span class="sxs-lookup"><span data-stu-id="ecc32-120">The name of the storage account where you are sending your output.</span></span> <span data-ttu-id="ecc32-121">You will be presented with a drop down list of Data Lake Store accounts to which the user logged in to the portal has access to.</span><span class="sxs-lookup"><span data-stu-id="ecc32-121">You will be presented with a drop down list of Data Lake Store accounts to which the user logged in to the portal has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ecc32-122">Path Prefix Pattern [<I>optional</I>]</span><span class="sxs-lookup"><span data-stu-id="ecc32-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="ecc32-123">The file path used to write your files within the specified Data Lake Store Account.</span><span class="sxs-lookup"><span data-stu-id="ecc32-123">The file path used to write your files within the specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="ecc32-124">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="ecc32-124">{date}, {time}</span></span><BR><span data-ttu-id="ecc32-125">Example 1: folder1/logs/{date}/{time}</span><span class="sxs-lookup"><span data-stu-id="ecc32-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="ecc32-126">Example 2: folder1/logs/{date}</span><span class="sxs-lookup"><span data-stu-id="ecc32-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ecc32-127">Date Format [<I>optional</I>]</span><span class="sxs-lookup"><span data-stu-id="ecc32-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="ecc32-128">If the date token is used in the prefix path, you can select the date format in which your files are organized.</span><span class="sxs-lookup"><span data-stu-id="ecc32-128">If the date token is used in the prefix path, you can select the date format in which your files are organized.</span></span> <span data-ttu-id="ecc32-129">Example: YYYY/MM/DD</span><span class="sxs-lookup"><span data-stu-id="ecc32-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ecc32-130">Time Format [<I>optional</I>]</span><span class="sxs-lookup"><span data-stu-id="ecc32-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="ecc32-131">If the time token is used in the prefix path, specify the time format in which your files are organized.</span><span class="sxs-lookup"><span data-stu-id="ecc32-131">If the time token is used in the prefix path, specify the time format in which your files are organized.</span></span> <span data-ttu-id="ecc32-132">Currently the only supported value is HH.</span><span class="sxs-lookup"><span data-stu-id="ecc32-132">Currently the only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ecc32-133">Event Serialization Format</span><span class="sxs-lookup"><span data-stu-id="ecc32-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="ecc32-134">Serialization format for output data.</span><span class="sxs-lookup"><span data-stu-id="ecc32-134">Serialization format for output data.</span></span> <span data-ttu-id="ecc32-135">JSON, CSV, and Avro are supported.</span><span class="sxs-lookup"><span data-stu-id="ecc32-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ecc32-136">Encoding</span><span class="sxs-lookup"><span data-stu-id="ecc32-136">Encoding</span></span></td>
<td><span data-ttu-id="ecc32-137">If CSV or JSON format, an encoding must be specified.</span><span class="sxs-lookup"><span data-stu-id="ecc32-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="ecc32-138">UTF-8 is the only supported encoding format at this time.</span><span class="sxs-lookup"><span data-stu-id="ecc32-138">UTF-8 is the only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ecc32-139">Delimiter</span><span class="sxs-lookup"><span data-stu-id="ecc32-139">Delimiter</span></span></td>
<td><span data-ttu-id="ecc32-140">Only applicable for CSV serialization.</span><span class="sxs-lookup"><span data-stu-id="ecc32-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="ecc32-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span><span class="sxs-lookup"><span data-stu-id="ecc32-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="ecc32-142">Supported values are comma, semicolon, space, tab and vertical bar.</span><span class="sxs-lookup"><span data-stu-id="ecc32-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ecc32-143">Format</span><span class="sxs-lookup"><span data-stu-id="ecc32-143">Format</span></span></td>
<td><span data-ttu-id="ecc32-144">Only applicable for JSON serialization.</span><span class="sxs-lookup"><span data-stu-id="ecc32-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="ecc32-145">Line separated specifies that the output will be formatted by having each JSON object separated by a new line.</span><span class="sxs-lookup"><span data-stu-id="ecc32-145">Line separated specifies that the output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="ecc32-146">Array specifies that the output will be formatted as an array of JSON objects.</span><span class="sxs-lookup"><span data-stu-id="ecc32-146">Array specifies that the output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="ecc32-147">Renew Data Lake Store Authorization</span><span class="sxs-lookup"><span data-stu-id="ecc32-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="ecc32-148">Currently, there is a limitation where the authentication token needs to be manually refreshed every 90 days for all jobs with Data Lake Store output.</span><span class="sxs-lookup"><span data-stu-id="ecc32-148">Currently, there is a limitation where the authentication token needs to be manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="ecc32-149">You will also need to re-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span><span class="sxs-lookup"><span data-stu-id="ecc32-149">You will also need to re-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="ecc32-150">A symptom of this issue is no job output and an error in the Operation Logs indicating need for re-authorization.</span><span class="sxs-lookup"><span data-stu-id="ecc32-150">A symptom of this issue is no job output and an error in the Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="ecc32-151">To resolve this issue, stop your running job and go to your Data Lake Store output.</span><span class="sxs-lookup"><span data-stu-id="ecc32-151">To resolve this issue, stop your running job and go to your Data Lake Store output.</span></span> <span data-ttu-id="ecc32-152">Click the “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span><span class="sxs-lookup"><span data-stu-id="ecc32-152">Click the “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span></span> <span data-ttu-id="ecc32-153">The page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span><span class="sxs-lookup"><span data-stu-id="ecc32-153">The page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="ecc32-154">You then need to click “Save” at the bottom of the page, and can proceed by restarting your job from the Last Stopped Time to avoid data loss.</span><span class="sxs-lookup"><span data-stu-id="ecc32-154">You then need to click “Save” at the bottom of the page, and can proceed by restarting your job from the Last Stopped Time to avoid data loss.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)



