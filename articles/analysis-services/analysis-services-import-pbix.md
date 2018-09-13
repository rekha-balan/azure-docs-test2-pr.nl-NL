---
title: Import a Power BI Desktop file into Azure Analysis Services | Microsoft Docs
description: Describes how to import a Power BI Desktop file (pbix) by using Azure portal.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 08/16/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: a2855ca5dbb76d3fcc30c4b1007c20bb48c91c9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856876"
---
# <a name="import-a-power-bi-desktop-file"></a><span data-ttu-id="5101a-103">Import a Power BI Desktop file</span><span class="sxs-lookup"><span data-stu-id="5101a-103">Import a Power BI Desktop file</span></span>

<span data-ttu-id="5101a-104">You can import a data model in a Power BI Desktop file (pbix) into Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="5101a-104">You can import a data model in a Power BI Desktop file (pbix) into Azure Analysis Services.</span></span> <span data-ttu-id="5101a-105">Model metadata, cached data, and datasource connections are imported.</span><span class="sxs-lookup"><span data-stu-id="5101a-105">Model metadata, cached data, and datasource connections are imported.</span></span> <span data-ttu-id="5101a-106">Reports and visualizations are not imported.</span><span class="sxs-lookup"><span data-stu-id="5101a-106">Reports and visualizations are not imported.</span></span> <span data-ttu-id="5101a-107">Imported data models from Power BI Desktop are at the 1400 compatibility level.</span><span class="sxs-lookup"><span data-stu-id="5101a-107">Imported data models from Power BI Desktop are at the 1400 compatibility level.</span></span>

<span data-ttu-id="5101a-108">**Restrictions**</span><span class="sxs-lookup"><span data-stu-id="5101a-108">**Restrictions**</span></span>   

- <span data-ttu-id="5101a-109">Importing from a pbix file uses the web designer feature in the portal, which is **preview**.</span><span class="sxs-lookup"><span data-stu-id="5101a-109">Importing from a pbix file uses the web designer feature in the portal, which is **preview**.</span></span> <span data-ttu-id="5101a-110">Functionality is limited.</span><span class="sxs-lookup"><span data-stu-id="5101a-110">Functionality is limited.</span></span> <span data-ttu-id="5101a-111">For more advanced model development and testing, it's best to use Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="5101a-111">For more advanced model development and testing, it's best to use Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>
- <span data-ttu-id="5101a-112">You must have server administrator permissions to import from a pbix file.</span><span class="sxs-lookup"><span data-stu-id="5101a-112">You must have server administrator permissions to import from a pbix file.</span></span>
- <span data-ttu-id="5101a-113">The pbix model can connect to **Azure SQL Database** and **Azure SQL Data Warehouse** data sources only.</span><span class="sxs-lookup"><span data-stu-id="5101a-113">The pbix model can connect to **Azure SQL Database** and **Azure SQL Data Warehouse** data sources only.</span></span>
- <span data-ttu-id="5101a-114">The pbix model cannot have live or DirectQuery connections.</span><span class="sxs-lookup"><span data-stu-id="5101a-114">The pbix model cannot have live or DirectQuery connections.</span></span> 
- <span data-ttu-id="5101a-115">Import may fail if your pbix data model contains metadata not supported in Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="5101a-115">Import may fail if your pbix data model contains metadata not supported in Analysis Services.</span></span>


## <a name="to-import-from-pbix"></a><span data-ttu-id="5101a-116">To import from pbix</span><span class="sxs-lookup"><span data-stu-id="5101a-116">To import from pbix</span></span>

1. <span data-ttu-id="5101a-117">In your server's **Overview** > **Web designer**, click **Open**.</span><span class="sxs-lookup"><span data-stu-id="5101a-117">In your server's **Overview** > **Web designer**, click **Open**.</span></span>

    ![Create a model in Azure portal](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="5101a-119">In **Web designer** > **Models**, click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="5101a-119">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Create a model in Azure portal](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="5101a-121">In **New model**, type a model name, and then select Power BI Desktop file.</span><span class="sxs-lookup"><span data-stu-id="5101a-121">In **New model**, type a model name, and then select Power BI Desktop file.</span></span>

    ![New model dialog in Azure portal](./media/analysis-services-import-pbix/aas-import-pbix-new-model.png)

4. <span data-ttu-id="5101a-123">In **Import**, locate and select your file.</span><span class="sxs-lookup"><span data-stu-id="5101a-123">In **Import**, locate and select your file.</span></span>

     ![Connect dialog in Azure portal](./media/analysis-services-import-pbix/aas-import-pbix-select-file.png)

## <a name="change-credentials"></a><span data-ttu-id="5101a-125">Change credentials</span><span class="sxs-lookup"><span data-stu-id="5101a-125">Change credentials</span></span>

<span data-ttu-id="5101a-126">When you import a data model from a pbix file, by default, the credentials used to connect to a datasource are set to ServiceAccount.</span><span class="sxs-lookup"><span data-stu-id="5101a-126">When you import a data model from a pbix file, by default, the credentials used to connect to a datasource are set to ServiceAccount.</span></span> <span data-ttu-id="5101a-127">After a model has been imported from a pbix, you can change credentials by using the following methods:</span><span class="sxs-lookup"><span data-stu-id="5101a-127">After a model has been imported from a pbix, you can change credentials by using the following methods:</span></span>

- <span data-ttu-id="5101a-128">Use the July 2018 (version 17.8.1) or later version of SSMS to edit credentials.</span><span class="sxs-lookup"><span data-stu-id="5101a-128">Use the July 2018 (version 17.8.1) or later version of SSMS to edit credentials.</span></span> <span data-ttu-id="5101a-129">This is the easiest way.</span><span class="sxs-lookup"><span data-stu-id="5101a-129">This is the easiest way.</span></span>
- <span data-ttu-id="5101a-130">Use TMSL [Alter command](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl) on the [DataSources object](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl) to modify the connection string property.</span><span class="sxs-lookup"><span data-stu-id="5101a-130">Use TMSL [Alter command](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl) on the [DataSources object](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl) to modify the connection string property.</span></span> 
- <span data-ttu-id="5101a-131">Open the model in Visual Studio, edit the credentials for the datasource connection, and then re-deploy the model.</span><span class="sxs-lookup"><span data-stu-id="5101a-131">Open the model in Visual Studio, edit the credentials for the datasource connection, and then re-deploy the model.</span></span>

<span data-ttu-id="5101a-132">To change credentials by using SSMS.</span><span class="sxs-lookup"><span data-stu-id="5101a-132">To change credentials by using SSMS.</span></span> 

1. <span data-ttu-id="5101a-133">In SSMS, expand database > **Connections**.</span><span class="sxs-lookup"><span data-stu-id="5101a-133">In SSMS, expand database > **Connections**.</span></span> 
2. <span data-ttu-id="5101a-134">Right-click the database connection, and then click **Refresh Credentials**.</span><span class="sxs-lookup"><span data-stu-id="5101a-134">Right-click the database connection, and then click **Refresh Credentials**.</span></span> 

    ![Refresh credentials](./media/analysis-services-import-pbix/aas-import-pbix-creds.png)

3. <span data-ttu-id="5101a-136">In the credentials dialog, select a credential type, and enter credentials.</span><span class="sxs-lookup"><span data-stu-id="5101a-136">In the credentials dialog, select a credential type, and enter credentials.</span></span> <span data-ttu-id="5101a-137">For SQL authentication, select Database.</span><span class="sxs-lookup"><span data-stu-id="5101a-137">For SQL authentication, select Database.</span></span> <span data-ttu-id="5101a-138">For organization account (OAuth), select Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="5101a-138">For organization account (OAuth), select Microsoft account.</span></span>
    <span data-ttu-id="5101a-139">![Edit credentials](./media/analysis-services-import-pbix/aas-import-pbix-edit-creds.png)</span><span class="sxs-lookup"><span data-stu-id="5101a-139">![Edit credentials](./media/analysis-services-import-pbix/aas-import-pbix-edit-creds.png)</span></span>

<span data-ttu-id="5101a-140">The July 2018 version of Power BI Desktop includes a new feature for changing datasource permissions.</span><span class="sxs-lookup"><span data-stu-id="5101a-140">The July 2018 version of Power BI Desktop includes a new feature for changing datasource permissions.</span></span> <span data-ttu-id="5101a-141">On the **Home** tab, click **Edit Queries**  > **Data source settings**.</span><span class="sxs-lookup"><span data-stu-id="5101a-141">On the **Home** tab, click **Edit Queries**  > **Data source settings**.</span></span> <span data-ttu-id="5101a-142">Select the datasource connection, and then click **Edit Permissions**.</span><span class="sxs-lookup"><span data-stu-id="5101a-142">Select the datasource connection, and then click **Edit Permissions**.</span></span>


## <a name="see-also"></a><span data-ttu-id="5101a-143">See also</span><span class="sxs-lookup"><span data-stu-id="5101a-143">See also</span></span>

<span data-ttu-id="5101a-144">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="5101a-144">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
[<span data-ttu-id="5101a-145">Connect to Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="5101a-145">Connect to Azure Analysis Services</span></span>](analysis-services-connect.md)  
