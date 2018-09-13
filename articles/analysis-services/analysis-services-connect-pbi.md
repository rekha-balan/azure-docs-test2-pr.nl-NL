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
# <a name="connect-with-power-bi"></a><span data-ttu-id="e726b-103">Connect with Power BI</span><span class="sxs-lookup"><span data-stu-id="e726b-103">Connect with Power BI</span></span>

<span data-ttu-id="e726b-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span><span class="sxs-lookup"><span data-stu-id="e726b-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="e726b-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="e726b-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="e726b-106">Connect in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="e726b-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="e726b-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span><span class="sxs-lookup"><span data-stu-id="e726b-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="e726b-108">In **Server**, enter the server name.</span><span class="sxs-lookup"><span data-stu-id="e726b-108">In **Server**, enter the server name.</span></span> 
    
    <span data-ttu-id="e726b-109">Be sure to include the full URL.</span><span class="sxs-lookup"><span data-stu-id="e726b-109">Be sure to include the full URL.</span></span> <span data-ttu-id="e726b-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="e726b-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="e726b-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span><span class="sxs-lookup"><span data-stu-id="e726b-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span></span> <span data-ttu-id="e726b-112">Otherwise, you can leave this field blank and select a database or perspective later.</span><span class="sxs-lookup"><span data-stu-id="e726b-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="e726b-113">Leave the default **Connect live** option, then press **Connect**.</span><span class="sxs-lookup"><span data-stu-id="e726b-113">Leave the default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="e726b-114">If prompted, enter your login credentials.</span><span class="sxs-lookup"><span data-stu-id="e726b-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="e726b-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="e726b-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span></span> <span data-ttu-id="e726b-116">Click  a model or perspective to show all the objects for that view.</span><span class="sxs-lookup"><span data-stu-id="e726b-116">Click  a model or perspective to show all the objects for that view.</span></span>

    <span data-ttu-id="e726b-117">The model opens in Power BI Desktop with a blank report in Report view.</span><span class="sxs-lookup"><span data-stu-id="e726b-117">The model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="e726b-118">The Fields list displays all non-hidden model objects.</span><span class="sxs-lookup"><span data-stu-id="e726b-118">The Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="e726b-119">Connection status is displayed in the lower-right corner.</span><span class="sxs-lookup"><span data-stu-id="e726b-119">Connection status is displayed in the lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="e726b-120">Connect in Power BI (service)</span><span class="sxs-lookup"><span data-stu-id="e726b-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="e726b-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span><span class="sxs-lookup"><span data-stu-id="e726b-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span></span>
2. <span data-ttu-id="e726b-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span><span class="sxs-lookup"><span data-stu-id="e726b-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="e726b-123">Locate and select your file.</span><span class="sxs-lookup"><span data-stu-id="e726b-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="e726b-124">See also</span><span class="sxs-lookup"><span data-stu-id="e726b-124">See also</span></span>
<span data-ttu-id="e726b-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="e726b-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="e726b-126">Client libraries</span><span class="sxs-lookup"><span data-stu-id="e726b-126">Client libraries</span></span>](analysis-services-data-providers.md)

