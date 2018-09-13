---
title: Deploy to Azure Analysis Services | Microsoft Docs
description: Learn how to deploy a tabular model to an Azure Analysis Services server.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
tags: ''
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 04/17/2017
ms.author: owend
ms.openlocfilehash: 9fdcf0d6e8d14f080dcdba359007046e1a969694
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555709"
---
# <a name="deploy-to-azure-analysis-services"></a><span data-ttu-id="b0719-103">Deploy to Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b0719-103">Deploy to Azure Analysis Services</span></span>
<span data-ttu-id="b0719-104">Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it.</span><span class="sxs-lookup"><span data-stu-id="b0719-104">Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it.</span></span> <span data-ttu-id="b0719-105">You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on.</span><span class="sxs-lookup"><span data-stu-id="b0719-105">You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on.</span></span> <span data-ttu-id="b0719-106">Or, you can use SQL Server Management Studio (SSMS) to deploy an existing tabular model database from an Analysis Services instance.</span><span class="sxs-lookup"><span data-stu-id="b0719-106">Or, you can use SQL Server Management Studio (SSMS) to deploy an existing tabular model database from an Analysis Services instance.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b0719-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="b0719-107">Before you begin</span></span>
<span data-ttu-id="b0719-108">To get started, you need:</span><span class="sxs-lookup"><span data-stu-id="b0719-108">To get started, you need:</span></span>

* <span data-ttu-id="b0719-109">**Analysis Services server** in Azure.</span><span class="sxs-lookup"><span data-stu-id="b0719-109">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="b0719-110">To learn more, see [Create an Analysis Services in Azure](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="b0719-110">To learn more, see [Create an Analysis Services in Azure](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="b0719-111">**Tabular model project** in SSDT or an existing tabular model at the 1200 compatibility level on an Analysis Services instance.</span><span class="sxs-lookup"><span data-stu-id="b0719-111">**Tabular model project** in SSDT or an existing tabular model at the 1200 compatibility level on an Analysis Services instance.</span></span> <span data-ttu-id="b0719-112">Never created one?</span><span class="sxs-lookup"><span data-stu-id="b0719-112">Never created one?</span></span> <span data-ttu-id="b0719-113">Try the [Adventure Works Tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0719-113">Try the [Adventure Works Tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="b0719-114">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b0719-114">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="b0719-115">The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.</span><span class="sxs-lookup"><span data-stu-id="b0719-115">The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.</span></span>

## <a name="to-deploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="b0719-116">To deploy a tabular model from SSDT</span><span class="sxs-lookup"><span data-stu-id="b0719-116">To deploy a tabular model from SSDT</span></span>
<span data-ttu-id="b0719-117">In order to deploy from SSDT, make sure you're using the [latest version](https://msdn.microsoft.com/library/mt204009.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0719-117">In order to deploy from SSDT, make sure you're using the [latest version](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="b0719-118">Before you deploy, make sure you can process the data in your tables.</span><span class="sxs-lookup"><span data-stu-id="b0719-118">Before you deploy, make sure you can process the data in your tables.</span></span> <span data-ttu-id="b0719-119">In SSDT, click **Model** > **Process** > **Process All**.</span><span class="sxs-lookup"><span data-stu-id="b0719-119">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="b0719-120">If processing fails, deploying will to.</span><span class="sxs-lookup"><span data-stu-id="b0719-120">If processing fails, deploying will to.</span></span>
> 
> 

1. <span data-ttu-id="b0719-121">Before you deploy, you need to get the server name.</span><span class="sxs-lookup"><span data-stu-id="b0719-121">Before you deploy, you need to get the server name.</span></span> <span data-ttu-id="b0719-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span><span class="sxs-lookup"><span data-stu-id="b0719-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Get server name in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="b0719-124">In SSDT > **Solution Explorer**, right-click the project > **Properties**.</span><span class="sxs-lookup"><span data-stu-id="b0719-124">In SSDT > **Solution Explorer**, right-click the project > **Properties**.</span></span> <span data-ttu-id="b0719-125">Then in **Deployment** > **Server** paste the server name.</span><span class="sxs-lookup"><span data-stu-id="b0719-125">Then in **Deployment** > **Server** paste the server name.</span></span>   
   
    ![Paste server name into deployment server property](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="b0719-127">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="b0719-127">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="b0719-128">You may be prompted to sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="b0719-128">You may be prompted to sign in to Azure.</span></span>
   
    ![Deploy to server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="b0719-130">Deployment status appears in both the Output window and in Deploy.</span><span class="sxs-lookup"><span data-stu-id="b0719-130">Deployment status appears in both the Output window and in Deploy.</span></span>
   
    ![Deployment status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="b0719-132">That's all there is to it!</span><span class="sxs-lookup"><span data-stu-id="b0719-132">That's all there is to it!</span></span>

## <a name="to-deploy-using-xmla-script"></a><span data-ttu-id="b0719-133">To deploy using XMLA script</span><span class="sxs-lookup"><span data-stu-id="b0719-133">To deploy using XMLA script</span></span>
1. <span data-ttu-id="b0719-134">In SSMS, right-click the tabular model database you want to deploy, click **Script** > **Script Database as** > **CREATE to**, then choose a location.</span><span class="sxs-lookup"><span data-stu-id="b0719-134">In SSMS, right-click the tabular model database you want to deploy, click **Script** > **Script Database as** > **CREATE to**, then choose a location.</span></span>
2. <span data-ttu-id="b0719-135">Execute the query on the server instance you want to deploy to.</span><span class="sxs-lookup"><span data-stu-id="b0719-135">Execute the query on the server instance you want to deploy to.</span></span> <span data-ttu-id="b0719-136">If you're deploying to the same server, you must at least change the **name** property in the XMLA script.</span><span class="sxs-lookup"><span data-stu-id="b0719-136">If you're deploying to the same server, you must at least change the **name** property in the XMLA script.</span></span>  

## <a name="but-something-went-wrong"></a><span data-ttu-id="b0719-137">But, something went wrong</span><span class="sxs-lookup"><span data-stu-id="b0719-137">But, something went wrong</span></span>
<span data-ttu-id="b0719-138">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server.</span><span class="sxs-lookup"><span data-stu-id="b0719-138">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server.</span></span> <span data-ttu-id="b0719-139">Make sure you can connect to your server using SSMS.</span><span class="sxs-lookup"><span data-stu-id="b0719-139">Make sure you can connect to your server using SSMS.</span></span> <span data-ttu-id="b0719-140">Then make sure the Deployment Server property for the project is correct.</span><span class="sxs-lookup"><span data-stu-id="b0719-140">Then make sure the Deployment Server property for the project is correct.</span></span>

<span data-ttu-id="b0719-141">If deployment fails on a table, it's likely because your server couldn't connect to a data source.</span><span class="sxs-lookup"><span data-stu-id="b0719-141">If deployment fails on a table, it's likely because your server couldn't connect to a data source.</span></span> <span data-ttu-id="b0719-142">If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b0719-142">If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0719-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0719-143">Next steps</span></span>
<span data-ttu-id="b0719-144">Now that you have your tabular model deployed to your server, you're ready to connect to it.</span><span class="sxs-lookup"><span data-stu-id="b0719-144">Now that you have your tabular model deployed to your server, you're ready to connect to it.</span></span> <span data-ttu-id="b0719-145">You can [connect to it with SSMS](analysis-services-manage.md) to manage it.</span><span class="sxs-lookup"><span data-stu-id="b0719-145">You can [connect to it with SSMS](analysis-services-manage.md) to manage it.</span></span> <span data-ttu-id="b0719-146">And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span><span class="sxs-lookup"><span data-stu-id="b0719-146">And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>





