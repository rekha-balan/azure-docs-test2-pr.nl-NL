---
title: Connect to Azure Analysis Services with Power BI | Microsoft Docs
description: Learn how to connect to an Azure Analysis Services server by using Power BI.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 04/12/2017
ms.author: owend
ms.openlocfilehash: b17251f8e88dc02ddf792da41121fe2730bc50e8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563247"
---
# <a name="connect-with-power-bi"></a>Connect with Power BI

Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data. 

> [!TIP]
> Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a>Connect in Power BI Desktop

1. In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.

2. In **Server**, enter the server name. 
    
    Be sure to include the full URL. For example, asazure://westcentralus.asazure.windows.net/advworks.

3. In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here. Otherwise, you can leave this field blank and select a database or perspective later.

4. Leave the default **Connect live** option, then press **Connect**. 

5. If prompted, enter your login credentials. 

6. In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**. Click  a model or perspective to show all the objects for that view.

    The model opens in Power BI Desktop with a blank report in Report view. The Fields list displays all non-hidden model objects. Connection status is displayed in the lower-right corner.

## <a name="connect-in-power-bi-service"></a>Connect in Power BI (service)

1. Create a Power BI Desktop file that has a live connection to your model on your server.
2. In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**. Locate and select your file.



## <a name="see-also"></a>See also
[Connect to Azure Analysis Services](analysis-services-connect.md)   
[Client libraries](analysis-services-data-providers.md)

