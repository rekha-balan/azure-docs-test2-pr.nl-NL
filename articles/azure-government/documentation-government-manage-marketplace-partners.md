---
title: Azure Marketplace for Azure Government partners | Microsoft Docs
description: This article provides a comparison of features and guidance on developing applications for Azure Government.
services: azure-government
cloud: gov
documentationcenter: ''
author: tsingh
manager: asimm
ms.assetid: 7790d3c5-d0fa-4662-b4f0-a174cb7d6c9f
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 11/14/2016
ms.author: zakramer;tsingh;divacc
ms.openlocfilehash: ca93c6c77704d4e7dac0294dcef9195060cb687e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564353"
---
# <a name="azure-marketplace-for-azure-government"></a>Azure Marketplace for Azure Government
If you're an Azure Government partner who's interested in publishing offerings to the Azure Marketplace, find the details in this article.

Currently BYOL VM Images and Solution Templates are supported in Azure Government Marketplace. As a best practice, Solution Templates should be reviewed prior to publishing to Azure Government to ensure it will function on both Azure Public and Azure Government Clouds. If you are only publishing a VM Image you can proceed to the publishing steps further below.

## <a name="pre-publishing-validation-for-solution-templates"></a>Pre-Publishing Validation for Solution Templates

Before you publish your solution template to Azure Government, we recommend checking a couple of common best practice areas to ensure your Template will work in both Azure Public Cloud and Azure Government.

1.  Verify endpoints are not hard coded into your solution Template for Azure Public Cloud. These won't be valid for any other Azure Environments. Instead modify the Solution template to request an API call to pull the valid end point:  

  Example:

  Incorrect VHD uri (hard coded) "uri": "[concat('https://', variables('storageAccountName'), '.blob.core.windows.net/',  '/osdisk.vhd')]",

  Correct VHD uri (referenced)

  "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'osdisk.vhd')]",

  The corrected syntax will ensure the template will work on any cloud (Gov, Public Azure, AzureStack, China, etc)

2.  Verify that resources used in your solution template are available in the Sovereign Cloud you are publishing to.
RPs in Azure & API version

    Identify availability Azure Government using Resource Explorer in the portal:

  1.    Log into Azure Government Portal
  2.    Launch Resource Explorer, following steps listed here https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-supported-services#supported-regions

  Most commonly used extensions; Availability in Fairfax  

  | Publisher/Type | Available Versions in Fairfax |
  | --- | --- |
  | Microsoft.OSTCExtensions/CustomScriptForLinux | 1; 1.1; 1.2.2.0; 1.3.0.2; 1.4.1.0; 1.5.2.0 |
  | Microsoft.Compute/CustomScriptExtension | 1.2; 1.3; 1.4; 1.7; 1.8 |
  | Microsoft.Azure.Extensions/DockerExtension | Not Available |
  | Microsoft.Azure.Extensions/CustomScript | 2.0.2 |
  | Microsoft.OSTCExtensions/LinuxDiagnostic | 2.0.9005; 2.1.9005; 2.2.9005; 2.3.9011 |
  | Microsoft.Powershell/DSC | 2.19.0.0 |

> [!NOTE]
> If you put locations in for a list of allowed values, you will need to periodically update it as new regions are added.  


## <a name="publishing"></a>Publishing
> [!NOTE]
> If you are not an existing Azure Certified Marketplace partner, complete the steps that show how to [publish and manage an offer](../marketplace-publishing/marketplace-publishing-getting-started.md) before proceeding.
>
>

### <a name="step-1"></a>Step 1
Sign in to [Azure Publishing](https://publish.windowsazure.com).

### <a name="step-2"></a>Step 2
Click the offer that you want to publish.

### <a name="step-3"></a>Step 3
Click **SKUS**, and select the **Azure Government Cloud** box.

> [!NOTE]
> Only Bring Your Own License (BYOL) SKUs are supported.  This option is not available for Pay-as-You-Go (PayG) SKUs.
>
>

![Offer page where the SKUS and Azure Government Cloud options are located](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-government/media/government-manage-marketplace-partner-1.png)

### <a name="step-4"></a>Step 4
Click the **+ Add Certification** link to add links to any certifications for your offer.

![Offer page with Add Certification link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-government/media/government-manage-marketplace-partner-2.png)

### <a name="step-5"></a>Step 5
To test your image in the publishing portal, request a [trial account](https://azuregov.microsoft.com/trial/azuregovtrial) for Microsoft Azure Government.

Your eligibility as a partner who serves US federal, state, local, or tribal entities is verified, and confirmation will be provided via email.  Your trial account will be available in three to five business days.

### <a name="step-6"></a>Step 6
Click **Publish**, and click **Push to Staging**.

![Publish and Push to Staging options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-government/media/government-manage-marketplace-partner-3.png)

You're prompted to enter a whitelisted subscription that has access to the staged offer. Enter the subscription ID from your newly acquired Azure Government trial account.

![Prompt where you specify the subscription IDs that can access the offer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-government/media/government-manage-marketplace-partner-4.png)

### <a name="step-7"></a>Step 7
After the offer is successfully staged, you can test your image by signing in to the [Azure portal](https://portal.azure.us) by using your Azure Government trial account.

### <a name="step-8"></a>Step 8
After you have validated your image by using the trial subscription, you can make the offer available live by clicking **Publish** and requesting approval to go to production.

![Request approval to go to production command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-government/media/government-manage-marketplace-partner-5.png)

## <a name="next-steps"></a>Next steps
For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).





