---
title: Retrain a New Azure Machine Learning web service with PowerShell | Microsoft Docs
description: Learn how to programmatically retrain a model and update the web service to use the newly trained model in Azure Machine Learning using the Machine Learning Management PowerShell cmdlets.
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.openlocfilehash: 069a3022cf9b6423b95e8f9f35686965d2654be7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864581"
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-the-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="d08ba-103">Retrain a New Resource Manager based web service using the Machine Learning Management PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="d08ba-103">Retrain a New Resource Manager based web service using the Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="d08ba-104">When you retrain a New web service, you update the predictive web service definition to reference the new trained model.</span><span class="sxs-lookup"><span data-stu-id="d08ba-104">When you retrain a New web service, you update the predictive web service definition to reference the new trained model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d08ba-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d08ba-105">Prerequisites</span></span>
<span data-ttu-id="d08ba-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="d08ba-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](retrain-models-programmatically.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d08ba-107">The predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span><span class="sxs-lookup"><span data-stu-id="d08ba-107">The predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span>
> <span data-ttu-id="d08ba-108">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span><span class="sxs-lookup"><span data-stu-id="d08ba-108">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="d08ba-109">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="d08ba-109">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md).</span></span>

<span data-ttu-id="d08ba-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="d08ba-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="d08ba-111">This process requires that you have installed the Azure Machine Learning Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d08ba-111">This process requires that you have installed the Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="d08ba-112">For information installing the Machine Learning cmdlets, see the [Azure Machine Learning Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/) reference on MSDN.</span><span class="sxs-lookup"><span data-stu-id="d08ba-112">For information installing the Machine Learning cmdlets, see the [Azure Machine Learning Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/) reference on MSDN.</span></span>

<span data-ttu-id="d08ba-113">Copied the following information from the retraining output:</span><span class="sxs-lookup"><span data-stu-id="d08ba-113">Copied the following information from the retraining output:</span></span>

* <span data-ttu-id="d08ba-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="d08ba-114">BaseLocation</span></span>
* <span data-ttu-id="d08ba-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="d08ba-115">RelativeLocation</span></span>

<span data-ttu-id="d08ba-116">The steps you take are:</span><span class="sxs-lookup"><span data-stu-id="d08ba-116">The steps you take are:</span></span>

1. <span data-ttu-id="d08ba-117">Sign in to your Azure Resource Manager account.</span><span class="sxs-lookup"><span data-stu-id="d08ba-117">Sign in to your Azure Resource Manager account.</span></span>
2. <span data-ttu-id="d08ba-118">Get the web service definition</span><span class="sxs-lookup"><span data-stu-id="d08ba-118">Get the web service definition</span></span>
3. <span data-ttu-id="d08ba-119">Export the Web Service Definition as JSON</span><span class="sxs-lookup"><span data-stu-id="d08ba-119">Export the Web Service Definition as JSON</span></span>
4. <span data-ttu-id="d08ba-120">Update the reference to the ilearner blob in the JSON.</span><span class="sxs-lookup"><span data-stu-id="d08ba-120">Update the reference to the ilearner blob in the JSON.</span></span>
5. <span data-ttu-id="d08ba-121">Import the JSON into a Web Service Definition</span><span class="sxs-lookup"><span data-stu-id="d08ba-121">Import the JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="d08ba-122">Update the web service with new Web Service Definition</span><span class="sxs-lookup"><span data-stu-id="d08ba-122">Update the web service with new Web Service Definition</span></span>

## <a name="sign-in-to-your-azure-resource-manager-account"></a><span data-ttu-id="d08ba-123">Sign in to your Azure Resource Manager account</span><span class="sxs-lookup"><span data-stu-id="d08ba-123">Sign in to your Azure Resource Manager account</span></span>
<span data-ttu-id="d08ba-124">You must first sign in to your Azure account from within the PowerShell environment using the [Connect-AzureRmAccount](/powershell/module/azurerm.profile/connect-azurermaccount) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d08ba-124">You must first sign in to your Azure account from within the PowerShell environment using the [Connect-AzureRmAccount](/powershell/module/azurerm.profile/connect-azurermaccount) cmdlet.</span></span>

## <a name="get-the-web-service-definition"></a><span data-ttu-id="d08ba-125">Get the Web Service Definition</span><span class="sxs-lookup"><span data-stu-id="d08ba-125">Get the Web Service Definition</span></span>
<span data-ttu-id="d08ba-126">Next, get the Web Service by calling the [Get-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/get-azurermmlwebservice) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d08ba-126">Next, get the Web Service by calling the [Get-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/get-azurermmlwebservice) cmdlet.</span></span> <span data-ttu-id="d08ba-127">The Web Service Definition is an internal representation of the trained model of the web service and is not directly modifiable.</span><span class="sxs-lookup"><span data-stu-id="d08ba-127">The Web Service Definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="d08ba-128">Make sure that you are retrieving the Web Service Definition for your Predictive experiment and not your training experiment.</span><span class="sxs-lookup"><span data-stu-id="d08ba-128">Make sure that you are retrieving the Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="d08ba-129">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span><span class="sxs-lookup"><span data-stu-id="d08ba-129">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="d08ba-130">Locate the web service, and then look at its web service ID.</span><span class="sxs-lookup"><span data-stu-id="d08ba-130">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="d08ba-131">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="d08ba-131">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="d08ba-132">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="d08ba-132">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="d08ba-133">Alternatively, to determine the resource group name of an existing web service, log on to the Microsoft Azure Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="d08ba-133">Alternatively, to determine the resource group name of an existing web service, log on to the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="d08ba-134">Select the web service.</span><span class="sxs-lookup"><span data-stu-id="d08ba-134">Select the web service.</span></span> <span data-ttu-id="d08ba-135">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="d08ba-135">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="d08ba-136">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="d08ba-136">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-as-json"></a><span data-ttu-id="d08ba-137">Export the Web Service Definition as JSON</span><span class="sxs-lookup"><span data-stu-id="d08ba-137">Export the Web Service Definition as JSON</span></span>
<span data-ttu-id="d08ba-138">To modify the definition to the trained model to use the newly Trained Model, you must first use the [Export-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/export-azurermmlwebservice) cmdlet to export it to a JSON format file.</span><span class="sxs-lookup"><span data-stu-id="d08ba-138">To modify the definition to the trained model to use the newly Trained Model, you must first use the [Export-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/export-azurermmlwebservice) cmdlet to export it to a JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob-in-the-json"></a><span data-ttu-id="d08ba-139">Update the reference to the ilearner blob in the JSON.</span><span class="sxs-lookup"><span data-stu-id="d08ba-139">Update the reference to the ilearner blob in the JSON.</span></span>
<span data-ttu-id="d08ba-140">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span><span class="sxs-lookup"><span data-stu-id="d08ba-140">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="d08ba-141">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span><span class="sxs-lookup"><span data-stu-id="d08ba-141">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span> <span data-ttu-id="d08ba-142">This updates the path to reference the new trained model.</span><span class="sxs-lookup"><span data-stu-id="d08ba-142">This updates the path to reference the new trained model.</span></span>

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-the-json-into-a-web-service-definition"></a><span data-ttu-id="d08ba-143">Import the JSON into a Web Service Definition</span><span class="sxs-lookup"><span data-stu-id="d08ba-143">Import the JSON into a Web Service Definition</span></span>
<span data-ttu-id="d08ba-144">You must use the [Import-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/import-azurermmlwebservice) cmdlet to convert the modified JSON file back into a Web Service Definition that you can use to update the Web Service Definition.</span><span class="sxs-lookup"><span data-stu-id="d08ba-144">You must use the [Import-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/import-azurermmlwebservice) cmdlet to convert the modified JSON file back into a Web Service Definition that you can use to update the Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service-with-new-web-service-definition"></a><span data-ttu-id="d08ba-145">Update the web service with new Web Service Definition</span><span class="sxs-lookup"><span data-stu-id="d08ba-145">Update the web service with new Web Service Definition</span></span>
<span data-ttu-id="d08ba-146">Finally, you use [Update-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/update-azurermmlwebservice) cmdlet to update the Web Service Definition.</span><span class="sxs-lookup"><span data-stu-id="d08ba-146">Finally, you use [Update-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/update-azurermmlwebservice) cmdlet to update the Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="d08ba-147">Summary</span><span class="sxs-lookup"><span data-stu-id="d08ba-147">Summary</span></span>
<span data-ttu-id="d08ba-148">Using the Machine Learning PowerShell management cmdlets, you can update the trained model of a predictive Web Service enabling scenarios such as:</span><span class="sxs-lookup"><span data-stu-id="d08ba-148">Using the Machine Learning PowerShell management cmdlets, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="d08ba-149">Periodic model retraining with new data.</span><span class="sxs-lookup"><span data-stu-id="d08ba-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="d08ba-150">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span><span class="sxs-lookup"><span data-stu-id="d08ba-150">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

