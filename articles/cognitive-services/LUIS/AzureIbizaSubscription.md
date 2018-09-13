---
title: Creating LUIS subscription keys via Azure | Microsoft Docs
description: In this article, you create a metered key for your LUIS account to provide unlimited traffic to your endpoint following a payment plan.
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/01/2017
ms.author: cahann
ms.openlocfilehash: 705722a3efb8db264017e7cdd7696c92208f6b8d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663062"
---
# <a name="creating-subscription-keys-via-azure"></a>Creating Subscription Keys Via Azure

For unlimited traffic to your HTTP endpoint, you must create a metered key for your account on LUIS. Metered keys provide unlimited traffic to your endpoint following a payment plan. To create your key, follow these steps: 

1. Sign in to the **[Microsoft Azure Portal](https://ms.portal.azure.com/)** 
2. Click the green **+** sign in the upper left-hand panel and search for “Cognitive Services” in the marketplace, then click on **Cognitive Services APIs** and follow the **create experience** to create an API account you are interested in. 

    ![Azure Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/azure_search.png) 

3. Choose the API you are interested in by clicking on the **API Type** to create a subscription. In this case, choose the **Language Understanding Intelligent Service (LUIS)** option. Configure the subscription with settings including account name, pricing tiers, etc. 

    ![Azure API Choice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/azure_apiChoice.png) 

4. Once you have created the API account, you can view the keys generated in the **Settings->Keys** blade. These can be tested in your existing application or by following the LUIS documentation to create a new application. 

    ![Azure Keys](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/azure_keys.png)

When you have created your key, you can add it to your account via the application settings/configuration dialog, found in any application. 



