---
title: Excel add-in for Machine Learning Web services | Microsoft Docs
description: How to use Azure Machine Learning Web services directly in Excel without writing any code.
services: machine-learning
documentationcenter: ''
author: tedway
manager: jhubbard
editor: cgronlun
tags: ''
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: 340ca173f064325a01fea204697d821dca4df381
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556055"
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="f9aaa-103">Excel Add-in for Azure Machine Learning web services</span><span class="sxs-lookup"><span data-stu-id="f9aaa-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="f9aaa-104">Excel makes it easy to call web services directly without the need to write any code.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="f9aaa-105">Steps to Use an Existing web service in the Workbook</span><span class="sxs-lookup"><span data-stu-id="f9aaa-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="f9aaa-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span>
2. <span data-ttu-id="f9aaa-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Select Web service][01]
3. <span data-ttu-id="f9aaa-109">This takes you to the **Predict** section.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-109">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="f9aaa-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="f9aaa-111">Select the data with headers and click the input data range icon.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-111">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="f9aaa-112">Make sure the "My data has headers" box is checked.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-112">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="f9aaa-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="f9aaa-114">Click **Predict**.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-114">Click **Predict**.</span></span>
   
    ![Predict section][02]

<span data-ttu-id="f9aaa-116">Deploy a web service or use an existing Web service.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="f9aaa-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f9aaa-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="f9aaa-118">Get the API key for your web service.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-118">Get the API key for your web service.</span></span> <span data-ttu-id="f9aaa-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="f9aaa-120">**Use a Classic web service**</span><span class="sxs-lookup"><span data-stu-id="f9aaa-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="f9aaa-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Studio select a Web service][04]
2. <span data-ttu-id="f9aaa-123">Copy the API key for the web service.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-123">Copy the API key for the web service.</span></span>
   
    ![Studio API key][05]
3. <span data-ttu-id="f9aaa-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="f9aaa-126">Look for the **Request URI** section.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-126">Look for the **Request URI** section.</span></span>  <span data-ttu-id="f9aaa-127">Copy and save the URL.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-127">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="f9aaa-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="f9aaa-129">**Use a New web service**</span><span class="sxs-lookup"><span data-stu-id="f9aaa-129">**Use a New web service**</span></span>

1. <span data-ttu-id="f9aaa-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="f9aaa-131">Click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-131">Click **Consume**.</span></span>
3. <span data-ttu-id="f9aaa-132">Look for the **Basic consumption info** section.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-132">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="f9aaa-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="f9aaa-134">Steps to Add a New web service</span><span class="sxs-lookup"><span data-stu-id="f9aaa-134">Steps to Add a New web service</span></span>

1. <span data-ttu-id="f9aaa-135">Deploy a web service or use an existing Web service.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="f9aaa-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f9aaa-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="f9aaa-137">Click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-137">Click **Consume**.</span></span>
3. <span data-ttu-id="f9aaa-138">Look for the **Basic consumption info** section.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-138">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="f9aaa-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="f9aaa-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span><span class="sxs-lookup"><span data-stu-id="f9aaa-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![Go to Web service selection][03]
5. <span data-ttu-id="f9aaa-142">Click **Add Web Service**.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="f9aaa-143">Paste the URL into the Excel add-in text box labeled **URL**.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-143">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="f9aaa-144">Paste the API/Primary key into the text box labeled **API key**.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-144">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="f9aaa-145">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-145">Click **Add**.</span></span>
   
    ![URL and API key for a classic Web service.][06]
9. <span data-ttu-id="f9aaa-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span><span class="sxs-lookup"><span data-stu-id="f9aaa-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="f9aaa-148">Sharing Your Workbook</span><span class="sxs-lookup"><span data-stu-id="f9aaa-148">Sharing Your Workbook</span></span>
<span data-ttu-id="f9aaa-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="f9aaa-150">That means you should only share the workbook with individuals you trust.</span><span class="sxs-lookup"><span data-stu-id="f9aaa-150">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="f9aaa-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="f9aaa-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-excel-add-in-for-web-services/image6.png






