---
title: Quickstart - Configure a firewall for an Analysis Services server in Azure | Microsoft Docs
description: Learn how to configure a firewall for an Analysis Services server instance in Azure.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: quickstart
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: c16a189e72edd94cf6fc60580d89dd4cfd1742e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870281"
---
# <a name="quickstart-configure-server-firewall---portal"></a><span data-ttu-id="1376a-103">Quickstart: Configure server firewall - Portal</span><span class="sxs-lookup"><span data-stu-id="1376a-103">Quickstart: Configure server firewall - Portal</span></span>

<span data-ttu-id="1376a-104">This quickstart helps you configure a firewall for your Azure Analysis Services server.</span><span class="sxs-lookup"><span data-stu-id="1376a-104">This quickstart helps you configure a firewall for your Azure Analysis Services server.</span></span> <span data-ttu-id="1376a-105">Enabling a firewall and configuring IP address ranges for only those computers accessing your server are an important part of securing your server and data.</span><span class="sxs-lookup"><span data-stu-id="1376a-105">Enabling a firewall and configuring IP address ranges for only those computers accessing your server are an important part of securing your server and data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1376a-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1376a-106">Prerequisites</span></span>

- <span data-ttu-id="1376a-107">An Analysis Services server in your subscription.</span><span class="sxs-lookup"><span data-stu-id="1376a-107">An Analysis Services server in your subscription.</span></span> <span data-ttu-id="1376a-108">To learn more, see [Quickstart: Create a server - Portal](analysis-services-create-server.md) or [Quickstart: Create a server - PowerShell](analysis-services-create-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="1376a-108">To learn more, see [Quickstart: Create a server - Portal](analysis-services-create-server.md) or [Quickstart: Create a server - PowerShell](analysis-services-create-powershell.md)</span></span>
- <span data-ttu-id="1376a-109">One or more IP address ranges for client computers (if needed).</span><span class="sxs-lookup"><span data-stu-id="1376a-109">One or more IP address ranges for client computers (if needed).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="1376a-110">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1376a-110">Log in to the Azure portal</span></span> 

[<span data-ttu-id="1376a-111">Log in to the portal</span><span class="sxs-lookup"><span data-stu-id="1376a-111">Log in to the portal</span></span>](https://portal.azure.com)

## <a name="configure-a-firewall"></a><span data-ttu-id="1376a-112">Configure a firewall</span><span class="sxs-lookup"><span data-stu-id="1376a-112">Configure a firewall</span></span>

1. <span data-ttu-id="1376a-113">Click on your server to open the Overview page.</span><span class="sxs-lookup"><span data-stu-id="1376a-113">Click on your server to open the Overview page.</span></span> 
2. <span data-ttu-id="1376a-114">In **SETTINGS** > **Firewall** > **Enable firewall**, click **On**.</span><span class="sxs-lookup"><span data-stu-id="1376a-114">In **SETTINGS** > **Firewall** > **Enable firewall**, click **On**.</span></span>
3. <span data-ttu-id="1376a-115">To allow DirectQuery access from Power BI service, in **Allow accesss from Power BI**, click **On**.</span><span class="sxs-lookup"><span data-stu-id="1376a-115">To allow DirectQuery access from Power BI service, in **Allow accesss from Power BI**, click **On**.</span></span>  
4. <span data-ttu-id="1376a-116">(Optional) Specify one or more IP address ranges.</span><span class="sxs-lookup"><span data-stu-id="1376a-116">(Optional) Specify one or more IP address ranges.</span></span> <span data-ttu-id="1376a-117">Enter a name, starting, and ending IP address for each range.</span><span class="sxs-lookup"><span data-stu-id="1376a-117">Enter a name, starting, and ending IP address for each range.</span></span> 
5. <span data-ttu-id="1376a-118">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1376a-118">Click **Save**.</span></span>

     ![Firewall settings](./media/analysis-services-qs-firewall/aas-qs-firewall.png)

## <a name="clean-up-resources"></a><span data-ttu-id="1376a-120">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1376a-120">Clean up resources</span></span>

<span data-ttu-id="1376a-121">When no longer needed, delete IP address ranges, or disable the firewall.</span><span class="sxs-lookup"><span data-stu-id="1376a-121">When no longer needed, delete IP address ranges, or disable the firewall.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1376a-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="1376a-122">Next steps</span></span>
<span data-ttu-id="1376a-123">In this quickstart, you learned how to configure a firewall for your server.</span><span class="sxs-lookup"><span data-stu-id="1376a-123">In this quickstart, you learned how to configure a firewall for your server.</span></span> <span data-ttu-id="1376a-124">Now that you have server, and secured it with a firewall, you can add a basic sample data model to it from the portal.</span><span class="sxs-lookup"><span data-stu-id="1376a-124">Now that you have server, and secured it with a firewall, you can add a basic sample data model to it from the portal.</span></span> <span data-ttu-id="1376a-125">Having a sample model is helpful to learn about configuring model database roles and testing client connections.</span><span class="sxs-lookup"><span data-stu-id="1376a-125">Having a sample model is helpful to learn about configuring model database roles and testing client connections.</span></span> <span data-ttu-id="1376a-126">To learn more, continue to the tutorial for adding a sample model.</span><span class="sxs-lookup"><span data-stu-id="1376a-126">To learn more, continue to the tutorial for adding a sample model.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1376a-127">Tutorial: Add a sample model to your server</span><span class="sxs-lookup"><span data-stu-id="1376a-127">Tutorial: Add a sample model to your server</span></span>](analysis-services-create-sample-model.md)
