---
title: Tutorial - Connect to Azure Analysis Services with Power BI Desktop | Microsoft Docs
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: tutorial
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: owend
ms.openlocfilehash: 4096b9f77ba841abfcb4f29f2827aefacf22103f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855812"
---
# <a name="tutorial-connect-with-power-bi-desktop"></a><span data-ttu-id="461b0-102">Tutorial: Connect with Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="461b0-102">Tutorial: Connect with Power BI Desktop</span></span>

<span data-ttu-id="461b0-103">In this tutorial, you use Power BI Desktop to connect to the adventureworks sample model database on your server.</span><span class="sxs-lookup"><span data-stu-id="461b0-103">In this tutorial, you use Power BI Desktop to connect to the adventureworks sample model database on your server.</span></span> <span data-ttu-id="461b0-104">The tasks you complete simulate a typical user connection to the model and creating a basic report from model data.</span><span class="sxs-lookup"><span data-stu-id="461b0-104">The tasks you complete simulate a typical user connection to the model and creating a basic report from model data.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="461b0-105">Get your server name from the portal</span><span class="sxs-lookup"><span data-stu-id="461b0-105">Get your server name from the portal</span></span>
> * <span data-ttu-id="461b0-106">Connect by using Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="461b0-106">Connect by using Power BI Desktop</span></span>
> * <span data-ttu-id="461b0-107">Create a basic report</span><span class="sxs-lookup"><span data-stu-id="461b0-107">Create a basic report</span></span>

## <a name="prerequisites"></a><span data-ttu-id="461b0-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="461b0-108">Prerequisites</span></span>

- <span data-ttu-id="461b0-109">[Add the adventureworks sample model database](../analysis-services-create-sample-model.md) to your server.</span><span class="sxs-lookup"><span data-stu-id="461b0-109">[Add the adventureworks sample model database](../analysis-services-create-sample-model.md) to your server.</span></span>
- <span data-ttu-id="461b0-110">Have [*read*](../analysis-services-server-admins.md) permissions for the adventureworks sample model database.</span><span class="sxs-lookup"><span data-stu-id="461b0-110">Have [*read*](../analysis-services-server-admins.md) permissions for the adventureworks sample model database.</span></span>
- <span data-ttu-id="461b0-111">[Install the newest Power BI Desktop](https://powerbi.microsoft.com/desktop).</span><span class="sxs-lookup"><span data-stu-id="461b0-111">[Install the newest Power BI Desktop](https://powerbi.microsoft.com/desktop).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="461b0-112">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="461b0-112">Log in to the Azure portal</span></span>
<span data-ttu-id="461b0-113">In this tutorial, you log in to the portal to get the server name only.</span><span class="sxs-lookup"><span data-stu-id="461b0-113">In this tutorial, you log in to the portal to get the server name only.</span></span> <span data-ttu-id="461b0-114">Typically, users would get the server name from the server administrator.</span><span class="sxs-lookup"><span data-stu-id="461b0-114">Typically, users would get the server name from the server administrator.</span></span>

<span data-ttu-id="461b0-115">Log in to the [portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="461b0-115">Log in to the [portal](https://portal.azure.com/).</span></span>

## <a name="get-server-name"></a><span data-ttu-id="461b0-116">Get server name</span><span class="sxs-lookup"><span data-stu-id="461b0-116">Get server name</span></span>
<span data-ttu-id="461b0-117">In order to connect to your server from Power BI Desktop, you first need the server name.</span><span class="sxs-lookup"><span data-stu-id="461b0-117">In order to connect to your server from Power BI Desktop, you first need the server name.</span></span> <span data-ttu-id="461b0-118">You can get the server name from the portal.</span><span class="sxs-lookup"><span data-stu-id="461b0-118">You can get the server name from the portal.</span></span>

<span data-ttu-id="461b0-119">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span><span class="sxs-lookup"><span data-stu-id="461b0-119">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
   ![Get server name in Azure](./media/analysis-services-tutorial-pbid/aas-copy-server-name.png)

## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="461b0-121">Connect in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="461b0-121">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="461b0-122">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span><span class="sxs-lookup"><span data-stu-id="461b0-122">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

   ![Connect in Get Data](./media/analysis-services-tutorial-pbid/aas-pbid-connect-aasserver.png)

2. <span data-ttu-id="461b0-124">In **Server**, paste the server name, then in **Database**, enter **adventureworks**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="461b0-124">In **Server**, paste the server name, then in **Database**, enter **adventureworks**, and then click **OK**.</span></span>

   ![Specify servername and model database](./media/analysis-services-tutorial-pbid/aas-pbid-connect-aas-servername.png)

3. <span data-ttu-id="461b0-126">When prompted, enter your login credentials.</span><span class="sxs-lookup"><span data-stu-id="461b0-126">When prompted, enter your login credentials.</span></span> <span data-ttu-id="461b0-127">The account you enter must have at least read permissions for the adventureworks sample model database.</span><span class="sxs-lookup"><span data-stu-id="461b0-127">The account you enter must have at least read permissions for the adventureworks sample model database.</span></span>

    <span data-ttu-id="461b0-128">The adventureworks model opens in Power BI Desktop with a blank report in Report view.</span><span class="sxs-lookup"><span data-stu-id="461b0-128">The adventureworks model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="461b0-129">The **Fields** list displays all non-hidden model objects.</span><span class="sxs-lookup"><span data-stu-id="461b0-129">The **Fields** list displays all non-hidden model objects.</span></span> <span data-ttu-id="461b0-130">Connection status is displayed in the lower-right corner.</span><span class="sxs-lookup"><span data-stu-id="461b0-130">Connection status is displayed in the lower-right corner.</span></span>

4. <span data-ttu-id="461b0-131">In **VISUALIZATIONS**, select **Clustered Bar Chart**, then click **Format** (paint roller icon), and then turn on **Data labels**.</span><span class="sxs-lookup"><span data-stu-id="461b0-131">In **VISUALIZATIONS**, select **Clustered Bar Chart**, then click **Format** (paint roller icon), and then turn on **Data labels**.</span></span> 

   ![Visualizations](./media/analysis-services-tutorial-pbid/aas-pbid-visualizations-report.png)

5. <span data-ttu-id="461b0-133">In **FIELDS** > **Internet Sales** table, select **Internet Sales Total** and **Margin** measures.</span><span class="sxs-lookup"><span data-stu-id="461b0-133">In **FIELDS** > **Internet Sales** table, select **Internet Sales Total** and **Margin** measures.</span></span> <span data-ttu-id="461b0-134">In **Product Category** table, select **Product Category Name**.</span><span class="sxs-lookup"><span data-stu-id="461b0-134">In **Product Category** table, select **Product Category Name**.</span></span>

   ![Complete report](./media/analysis-services-tutorial-pbid/aas-pbid-complete-report.png)

    <span data-ttu-id="461b0-136">Take a few minutes to explore the adventureworks sample model by creating different visualizations and slicing on data and metrics.</span><span class="sxs-lookup"><span data-stu-id="461b0-136">Take a few minutes to explore the adventureworks sample model by creating different visualizations and slicing on data and metrics.</span></span> <span data-ttu-id="461b0-137">When you're happy with your report, be sure to save.</span><span class="sxs-lookup"><span data-stu-id="461b0-137">When you're happy with your report, be sure to save.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="461b0-138">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="461b0-138">Clean up resources</span></span>

<span data-ttu-id="461b0-139">If no longer needed, do not save your report or delete the file if you did save.</span><span class="sxs-lookup"><span data-stu-id="461b0-139">If no longer needed, do not save your report or delete the file if you did save.</span></span>

## <a name="next-steps"></a><span data-ttu-id="461b0-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="461b0-140">Next steps</span></span>
<span data-ttu-id="461b0-141">In this tutorial, you learned how to use Power BI Desktop to connect to a data model on a server and create a basic report.</span><span class="sxs-lookup"><span data-stu-id="461b0-141">In this tutorial, you learned how to use Power BI Desktop to connect to a data model on a server and create a basic report.</span></span> <span data-ttu-id="461b0-142">If you're not familiar with how to create a data model, see the [Adventure Works Internet Sales tabular data modeling tutorial](aas-adventure-works-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="461b0-142">If you're not familiar with how to create a data model, see the [Adventure Works Internet Sales tabular data modeling tutorial](aas-adventure-works-tutorial.md).</span></span>