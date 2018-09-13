---
title: Excel add-in for Machine Learning Web services | Microsoft Docs
description: How to use Azure Machine Learning Web services directly in Excel without writing any code.
services: machine-learning
documentationcenter: ''
author: marthalc
ms.author: marthalc
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.component: studio
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 2/1/2018
ms.openlocfilehash: 8fade171095ff6a9f4c10925089452d8925e11fe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966485"
---
# <a name="excel-add-in-for-azure-machine-learning-studio-web-services"></a><span data-ttu-id="10687-103">Excel Add-in for Azure Machine Learning Studio web services</span><span class="sxs-lookup"><span data-stu-id="10687-103">Excel Add-in for Azure Machine Learning Studio web services</span></span>
<span data-ttu-id="10687-104">Excel makes it easy to call web services directly without the need to write any code.</span><span class="sxs-lookup"><span data-stu-id="10687-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="10687-105">Steps to Use an Existing web service in the Workbook</span><span class="sxs-lookup"><span data-stu-id="10687-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="10687-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span><span class="sxs-lookup"><span data-stu-id="10687-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span> 
 
> [!NOTE]
> <span data-ttu-id="10687-107">You will see the list of the Web Services related to the file and at the bottom a checkbox for "Auto-predict".</span><span class="sxs-lookup"><span data-stu-id="10687-107">You will see the list of the Web Services related to the file and at the bottom a checkbox for "Auto-predict".</span></span> <span data-ttu-id="10687-108">If you enable auto-predict the predictions of **all** your services will be updated everytime there is a change on the inputs.</span><span class="sxs-lookup"><span data-stu-id="10687-108">If you enable auto-predict the predictions of **all** your services will be updated everytime there is a change on the inputs.</span></span> <span data-ttu-id="10687-109">If unchecked you will have to click on "Predict All" for refresh.</span><span class="sxs-lookup"><span data-stu-id="10687-109">If unchecked you will have to click on "Predict All" for refresh.</span></span> <span data-ttu-id="10687-110">For enabling auto-predict at a service level go to step 6.</span><span class="sxs-lookup"><span data-stu-id="10687-110">For enabling auto-predict at a service level go to step 6.</span></span>

2. <span data-ttu-id="10687-111">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span><span class="sxs-lookup"><span data-stu-id="10687-111">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Select Web service][01]
3. <span data-ttu-id="10687-113">This takes you to the **Predict** section.</span><span class="sxs-lookup"><span data-stu-id="10687-113">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="10687-114">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span><span class="sxs-lookup"><span data-stu-id="10687-114">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="10687-115">Select the data with headers and click the input data range icon.</span><span class="sxs-lookup"><span data-stu-id="10687-115">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="10687-116">Make sure the "My data has headers" box is checked.</span><span class="sxs-lookup"><span data-stu-id="10687-116">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="10687-117">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span><span class="sxs-lookup"><span data-stu-id="10687-117">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="10687-118">Click **Predict**.</span><span class="sxs-lookup"><span data-stu-id="10687-118">Click **Predict**.</span></span> <span data-ttu-id="10687-119">If you select the "auto-predict" checkbox any change on the selected areas (the ones specified as input) will trigger a request and an update of the output cells without the need for you to press the predict button.</span><span class="sxs-lookup"><span data-stu-id="10687-119">If you select the "auto-predict" checkbox any change on the selected areas (the ones specified as input) will trigger a request and an update of the output cells without the need for you to press the predict button.</span></span>
   
    ![Predict section][02]

<span data-ttu-id="10687-121">Deploy a web service or use an existing Web service.</span><span class="sxs-lookup"><span data-stu-id="10687-121">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="10687-122">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="10687-122">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="10687-123">Get the API key for your web service.</span><span class="sxs-lookup"><span data-stu-id="10687-123">Get the API key for your web service.</span></span> <span data-ttu-id="10687-124">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="10687-124">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="10687-125">**Use a Classic web service**</span><span class="sxs-lookup"><span data-stu-id="10687-125">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="10687-126">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span><span class="sxs-lookup"><span data-stu-id="10687-126">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Studio select a Web service][04]
2. <span data-ttu-id="10687-128">Copy the API key for the web service.</span><span class="sxs-lookup"><span data-stu-id="10687-128">Copy the API key for the web service.</span></span>
   
    ![Studio API key][05]
3. <span data-ttu-id="10687-130">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span><span class="sxs-lookup"><span data-stu-id="10687-130">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="10687-131">Look for the **Request URI** section.</span><span class="sxs-lookup"><span data-stu-id="10687-131">Look for the **Request URI** section.</span></span>  <span data-ttu-id="10687-132">Copy and save the URL.</span><span class="sxs-lookup"><span data-stu-id="10687-132">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="10687-133">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="10687-133">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="10687-134">**Use a New web service**</span><span class="sxs-lookup"><span data-stu-id="10687-134">**Use a New web service**</span></span>

1. <span data-ttu-id="10687-135">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span><span class="sxs-lookup"><span data-stu-id="10687-135">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="10687-136">Click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="10687-136">Click **Consume**.</span></span>
3. <span data-ttu-id="10687-137">Look for the **Basic consumption info** section.</span><span class="sxs-lookup"><span data-stu-id="10687-137">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="10687-138">Copy and save the **Primary Key** and the **Request-Response** URL.</span><span class="sxs-lookup"><span data-stu-id="10687-138">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="10687-139">Steps to Add a New web service</span><span class="sxs-lookup"><span data-stu-id="10687-139">Steps to Add a New web service</span></span>

1. <span data-ttu-id="10687-140">Deploy a web service or use an existing Web service.</span><span class="sxs-lookup"><span data-stu-id="10687-140">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="10687-141">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="10687-141">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="10687-142">Click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="10687-142">Click **Consume**.</span></span>
3. <span data-ttu-id="10687-143">Look for the **Basic consumption info** section.</span><span class="sxs-lookup"><span data-stu-id="10687-143">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="10687-144">Copy and save the **Primary Key** and the **Request-Response** URL.</span><span class="sxs-lookup"><span data-stu-id="10687-144">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="10687-145">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span><span class="sxs-lookup"><span data-stu-id="10687-145">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![Go to Web service selection][03]
5. <span data-ttu-id="10687-147">Click **Add Web Service**.</span><span class="sxs-lookup"><span data-stu-id="10687-147">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="10687-148">Paste the URL into the Excel add-in text box labeled **URL**.</span><span class="sxs-lookup"><span data-stu-id="10687-148">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="10687-149">Paste the API/Primary key into the text box labeled **API key**.</span><span class="sxs-lookup"><span data-stu-id="10687-149">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="10687-150">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="10687-150">Click **Add**.</span></span>
   
    ![URL and API key for a classic Web service.][06]
9. <span data-ttu-id="10687-152">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span><span class="sxs-lookup"><span data-stu-id="10687-152">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="10687-153">Sharing Your Workbook</span><span class="sxs-lookup"><span data-stu-id="10687-153">Sharing Your Workbook</span></span>
<span data-ttu-id="10687-154">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span><span class="sxs-lookup"><span data-stu-id="10687-154">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="10687-155">That means you should only share the workbook with individuals you trust.</span><span class="sxs-lookup"><span data-stu-id="10687-155">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="10687-156">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="10687-156">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/excel-add-in-for-web-services/image1.png
[02]: ./media/excel-add-in-for-web-services/image2.png
[03]: ./media/excel-add-in-for-web-services/image3.png
[04]: ./media/excel-add-in-for-web-services/image4.png
[05]: ./media/excel-add-in-for-web-services/image5.png
[06]: ./media/excel-add-in-for-web-services/image6.png
