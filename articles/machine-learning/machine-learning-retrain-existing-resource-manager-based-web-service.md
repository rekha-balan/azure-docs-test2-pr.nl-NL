---
title: Retrain an existing predictive web service | Microsoft Docs
description: Learn how to retrain a model and update the web service to use the newly trained model in Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondl
editor: ''
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: 286b8deeacd1678fe746e2c3227b2246329b6c7e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550954"
---
# <a name="retrain-an-existing-predictive-web-service"></a>Retrain an existing predictive web service
This document describes the retraining process for the following scenario:

* You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.
* You have new data that you want your predictive web service to use to perform its scoring.

> [!NOTE] 
> To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service. For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md). 

Starting with your existing web service and experiments, you need to follow these steps:

1. Update the model.
   1. Modify your training experiment to allow for web service inputs and outputs.
   2. Deploy the training experiment as a retraining web service.
   3. Use the training experiment's Batch Execution Service (BES) to retrain the model.
2. Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.
   1. Sign in to your Azure Resource Manager account.
   2. Get the web service definition.
   3. Export the web service definition as JSON.
   4. Update the reference to the ilearner blob in the JSON.
   5. Import the JSON into a web service definition.
   6. Update the web service with a new web service definition.

## <a name="deploy-the-training-experiment"></a>Deploy the training experiment
To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model. By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment. If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.

To update your training experiment:

1. Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module). Typically, you want to ensure that your input data is processed in the same way as your original training data.
2. Connect a *Web Service Output* module to the output of your *Train Model* module.
3. If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.

Run your experiment.

Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.  

At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**. The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page. Type a name for your web service, choose a payment plan, and then click **Deploy**. You can only use the Batch Execution method for creating trained models.

## <a name="retrain-the-model-with-new-data-by-using-bes"></a>Retrain the model with new data by using BES
For this example, we're using C# to create the retraining application. You can also use Python or R sample code to accomplish this task.

To call the retraining APIs:

1. Create a C# console application in Visual Studio (**New** > **Project** > **Windows Desktop** > **Console Application**).
2. Sign in to the Machine Learning Web Services portal.
3. Click the web service that you're working with.
4. Click **Consume**.
5. At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.
6. Copy the sample C# code for batch execution and paste it into the Program.cs file. Make sure that the namespace remains intact.

Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments. To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).

The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.

![Consume page][1]

### <a name="update-the-apikey-declaration"></a>Update the apikey declaration
Locate the **apikey** declaration:

    const string apiKey = "abc123"; // Replace this with the API key for the web service

In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.

### <a name="update-the-azure-storage-information"></a>Update the Azure Storage information
The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.  

To update the Azure Storage information, you must retrieve the storage account name, key, and container information for your storage account from the Azure classic portal, and then update the correspondi After running your experiment, the resulting workflow should be similar to the following:

![Resulting workflow after run][4]ng values in the code.

1. Sign in to the Azure classic portal.
2. In the left navigation column, click **Storage**.
3. From the list of storage accounts, select one to store the retrained model.
4. At the bottom of the page, click **Manage Access Keys**.
5. Copy and save the **Primary Access Key** and close the dialog.
6. At the top of the page, click **Containers**.
7. Select an existing container, or create a new one and save the name.

Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the classic portal.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

You also must ensure that the input file is available at the location that you specify in the code.

### <a name="specify-the-output-location"></a>Specify the output location
When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`. See the following example:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you want to use for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

The following is an example of retraining output: ![Retraining output][6]

## <a name="evaluate-the-retraining-results"></a>Evaluate the retraining results
When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.

You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.  

Examine the results to determine whether the newly trained model performs well enough to replace the existing one.

Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.

## <a name="retrain-the-web-service"></a>Retrain the web service
When you retrain a new web service, you update the predictive web service definition to reference the new trained model. The web service definition is an internal representation of the trained model of the web service and is not directly modifiable. Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.

## <a name="sign-in-to-azure-resource-manager"></a>Sign in to Azure Resource Manager
You must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-the-web-service-definition-object"></a>Get the Web Service Definition object
Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription. Locate the web service, and then look at its web service ID. The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element. In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal. Select the web service. The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element. In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-object-as-json"></a>Export the Web Service Definition object as JSON
To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON-format file.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob"></a>Update the reference to the ilearner blob
In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob. The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.

     "asset3": {
        "name": "Retrain Sample [trained model]",
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

## <a name="import-the-json-into-a-web-service-definition-object"></a>Import the JSON into a Web Service Definition object
You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service"></a>Update the web service
Finally, use the [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the predictive experiment.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/



