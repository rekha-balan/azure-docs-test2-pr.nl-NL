---
title: 'Azure Machine Learning Web Services: Deployment and consumption | Microsoft Docs'
description: Resources for deploying and consuming web services.
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondl
editor: ''
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 6db98921b48abd1e7c62a010e9ad7a7492484bd0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554111"
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Azure Machine Learning Web Services: Deployment and consumption
You can use Azure Machine Learning to deploy machine-learning workflows and models as web services. These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode. Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.

The next sections provide links to walkthroughs, code, and documentation to help get you started.

## <a name="deploy-a-web-service"></a>Deploy a web service
### <a name="with-azure-machine-learning-studio"></a>With Azure Machine Learning Studio
Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.

The following links provide general Information about how to deploy a new web service:

* For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).
* For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).
* For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).
* For specific examples that deploy a web service, see:

  * [Walkthrough Step 5: Deploy the Azure Machine Learning web service](machine-learning-walkthrough-5-publish-web-service.md)
  * [How to deploy a web service to multiple regions](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>With web services resource provider APIs (Azure Resource Manager APIs)
The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls. For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>With PowerShell cmdlets
Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.

To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices). After you create the .exe file from the code, you can type:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Running the application creates a web service JSON template. To use the template to deploy a web service, you must add the following information:

* Storage account name and key

    You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).
* Commitment plan ID

    You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.

Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.

Here's an example:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

See the following articles and sample code for additional details:

* [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN
* Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub

## <a name="consume-the-web-services"></a>Consume the web services
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a>From the Azure Machine Learning Web Services UI (Testing)
You can test your web service from the Azure Machine Learning Web Services portal. This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.

* [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md)
* [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)
* [Walkthrough Step 5: Deploy the Azure Machine Learning web service](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>From Excel
You can download an Excel template that consumes the web service:

* [Consuming an Azure Machine Learning web service from Excel](machine-learning-consuming-from-excel.md)
* [Excel add-in for Azure Machine Learning Web Services](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>From a REST-based client
Azure Machine Learning Web Services are RESTful APIs. You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started. For more information, see [How to consume an Azure Machine Learning web service that has been deployed from a Machine Learning experiment](machine-learning-consume-web-services.md).
