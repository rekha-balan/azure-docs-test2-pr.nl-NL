---
title: Connect to Azure Analysis Services with Excel | Microsoft Docs
description: Learn how to connect to an Azure Analysis Services server by using Excel.
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
ms.openlocfilehash: 163827e323b728f507459563a1bbd4f39ffbd067
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563085"
---
# <a name="connect-with-excel"></a><span data-ttu-id="d5317-103">Connect with Excel</span><span class="sxs-lookup"><span data-stu-id="d5317-103">Connect with Excel</span></span>

<span data-ttu-id="d5317-104">Once you've created a server in Azure, and deployed a tabular model to it, you're ready to connect and begin exploring data.</span><span class="sxs-lookup"><span data-stu-id="d5317-104">Once you've created a server in Azure, and deployed a tabular model to it, you're ready to connect and begin exploring data.</span></span> 


## <a name="connect-in-excel"></a><span data-ttu-id="d5317-105">Connect in Excel</span><span class="sxs-lookup"><span data-stu-id="d5317-105">Connect in Excel</span></span>

<span data-ttu-id="d5317-106">Connecting to a server in Excel is supported by using Get Data in Excel 2016 or Power Query in earlier versions.</span><span class="sxs-lookup"><span data-stu-id="d5317-106">Connecting to a server in Excel is supported by using Get Data in Excel 2016 or Power Query in earlier versions.</span></span> <span data-ttu-id="d5317-107">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span><span class="sxs-lookup"><span data-stu-id="d5317-107">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="d5317-108">**To connect in Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="d5317-108">**To connect in Excel 2016**</span></span>

1. <span data-ttu-id="d5317-109">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="d5317-109">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="d5317-110">In the Data Connection Wizard, in **Server name**, paste the server name from the clipboard.</span><span class="sxs-lookup"><span data-stu-id="d5317-110">In the Data Connection Wizard, in **Server name**, paste the server name from the clipboard.</span></span> <span data-ttu-id="d5317-111">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span><span class="sxs-lookup"><span data-stu-id="d5317-111">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Connect from Excel logon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="d5317-113">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="d5317-113">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span></span>
   
    ![Connect from Excel select model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="d5317-115">See also</span><span class="sxs-lookup"><span data-stu-id="d5317-115">See also</span></span>
<span data-ttu-id="d5317-116">[Client libraries](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="d5317-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="d5317-117">Manage your server</span><span class="sxs-lookup"><span data-stu-id="d5317-117">Manage your server</span></span>](analysis-services-manage.md)     




