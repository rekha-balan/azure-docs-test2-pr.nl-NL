---
title: Client libraries required for connecting to Azure Analysis Services | Microsoft Docs
description: Describes client libraries required for client applications and tools to connect Azure Analysis Services
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
ms.date: 04/14/2016
ms.author: owend
ms.openlocfilehash: c29a6627f712b9d89ac65e845f3ccb4fb87bf8fb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562890"
---
# <a name="client-libraries-for-connecting-to-azure-analysis-services"></a><span data-ttu-id="00604-103">Client libraries for connecting to Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="00604-103">Client libraries for connecting to Azure Analysis Services</span></span>

<span data-ttu-id="00604-104">Client libraries are necessary for client applications and tools to connect to Analysis Services servers.</span><span class="sxs-lookup"><span data-stu-id="00604-104">Client libraries are necessary for client applications and tools to connect to Analysis Services servers.</span></span> 

<span data-ttu-id="00604-105">Analysis Services utilize three client libraries.</span><span class="sxs-lookup"><span data-stu-id="00604-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="00604-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span><span class="sxs-lookup"><span data-stu-id="00604-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="00604-107">The Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span><span class="sxs-lookup"><span data-stu-id="00604-107">The Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="00604-108">Typically, all three are installed at the same time.</span><span class="sxs-lookup"><span data-stu-id="00604-108">Typically, all three are installed at the same time.</span></span> <span data-ttu-id="00604-109">Azure Analysis Services requires the latest versions.</span><span class="sxs-lookup"><span data-stu-id="00604-109">Azure Analysis Services requires the latest versions.</span></span> 

<span data-ttu-id="00604-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span><span class="sxs-lookup"><span data-stu-id="00604-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="00604-111">However, depending on the version of Excel, or whether or not newer versions of Excel and Power BI Desktop are updated monthly, the client libraries installed may not be updated to the latest versions required by Azure Analysis Service.</span><span class="sxs-lookup"><span data-stu-id="00604-111">However, depending on the version of Excel, or whether or not newer versions of Excel and Power BI Desktop are updated monthly, the client libraries installed may not be updated to the latest versions required by Azure Analysis Service.</span></span> <span data-ttu-id="00604-112">The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="00604-112">The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="00604-113">These applications require manually installing the libraries.</span><span class="sxs-lookup"><span data-stu-id="00604-113">These applications require manually installing the libraries.</span></span> <span data-ttu-id="00604-114">The client libraries for manual installation are included in SQL Server feature packs as distributable packages; however, these are tied to the SQL Server version and may not be the latest.</span><span class="sxs-lookup"><span data-stu-id="00604-114">The client libraries for manual installation are included in SQL Server feature packs as distributable packages; however, these are tied to the SQL Server version and may not be the latest.</span></span>  

<span data-ttu-id="00604-115">Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source.</span><span class="sxs-lookup"><span data-stu-id="00604-115">Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source.</span></span> <span data-ttu-id="00604-116">To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="00604-116">To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-the-latest-preview-client-libraries"></a><span data-ttu-id="00604-117">Download the latest **preview** client libraries</span><span class="sxs-lookup"><span data-stu-id="00604-117">Download the latest **preview** client libraries</span></span>  
<span data-ttu-id="00604-118">Use the following client libraries to get the latest bug fixes and updates.</span><span class="sxs-lookup"><span data-stu-id="00604-118">Use the following client libraries to get the latest bug fixes and updates.</span></span> <span data-ttu-id="00604-119">These are recommended when connecting to Azure Analysis Services or SQL Server vNext Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="00604-119">These are recommended when connecting to Azure Analysis Services or SQL Server vNext Analysis Services.</span></span>

[<span data-ttu-id="00604-120">MSOLAP (amd64) Preview</span><span class="sxs-lookup"><span data-stu-id="00604-120">MSOLAP (amd64) Preview</span></span>](http://download.microsoft.com/download/4/8/2/482E5799-9B8E-4724-8A4C-F301BAE788EE/14.0.500.170/amd64/SQL_AS_OLEDB.msi)</br>
[<span data-ttu-id="00604-121">MSOLAP (x86) Preview</span><span class="sxs-lookup"><span data-stu-id="00604-121">MSOLAP (x86) Preview</span></span>](http://download.microsoft.com/download/4/8/2/482E5799-9B8E-4724-8A4C-F301BAE788EE/14.0.500.170/x86/SQL_AS_OLEDB.msi)</br>
[<span data-ttu-id="00604-122">AMO Preview</span><span class="sxs-lookup"><span data-stu-id="00604-122">AMO Preview</span></span>](http://download.microsoft.com/download/4/8/2/482E5799-9B8E-4724-8A4C-F301BAE788EE/14.0.500.170/SQL_AS_AMO.msi)</br>
[<span data-ttu-id="00604-123">ADOMD Preview</span><span class="sxs-lookup"><span data-stu-id="00604-123">ADOMD Preview</span></span>](http://download.microsoft.com/download/4/8/2/482E5799-9B8E-4724-8A4C-F301BAE788EE/14.0.500.170/SQL_AS_ADOMD.msi)</br>

## <a name="download-the-latest-rtm-client-libraries"></a><span data-ttu-id="00604-124">Download the latest **RTM** client libraries</span><span class="sxs-lookup"><span data-stu-id="00604-124">Download the latest **RTM** client libraries</span></span>  
<span data-ttu-id="00604-125">Use the following client libraries if you are in a production environment and require fully released and supported versions.</span><span class="sxs-lookup"><span data-stu-id="00604-125">Use the following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="00604-126">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="00604-126">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[<span data-ttu-id="00604-127">MSOLAP (x86)</span><span class="sxs-lookup"><span data-stu-id="00604-127">MSOLAP (x86)</span></span>](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[<span data-ttu-id="00604-128">AMO</span><span class="sxs-lookup"><span data-stu-id="00604-128">AMO</span></span>](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[<span data-ttu-id="00604-129">ADOMD</span><span class="sxs-lookup"><span data-stu-id="00604-129">ADOMD</span></span>](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a><span data-ttu-id="00604-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="00604-130">Next steps</span></span>
<span data-ttu-id="00604-131">[Connect to an Azure Analysis Services server](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="00604-131">[Connect to an Azure Analysis Services server](analysis-services-connect.md).</span></span>
