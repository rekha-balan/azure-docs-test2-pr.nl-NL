---
title: Move data - Data Management Gateway | Microsoft Docs
description: Set up a data gateway to move data between on-premises and the cloud. Use Data Management Gateway in Azure Data Factory to move your data.
services: data-factory
documentationcenter: ''
author: nabhishek
manager: craigg
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: abnarain
robots: noindex
ms.openlocfilehash: d695627efddc0ca02c3d9299f4b8a13bdc85e8fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967237"
---
# <a name="move-data-between-on-premises-sources-and-the-cloud-with-data-management-gateway"></a><span data-ttu-id="f6629-104">Move data between on-premises sources and the cloud with Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="f6629-104">Move data between on-premises sources and the cloud with Data Management Gateway</span></span>
> [!NOTE]
> <span data-ttu-id="f6629-105">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f6629-105">This article applies to version 1 of Data Factory.</span></span> <span data-ttu-id="f6629-106">If you are using the current version of the Data Factory service, see [copy data between on-premises and cloud using Data Factory](../tutorial-hybrid-copy-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f6629-106">If you are using the current version of the Data Factory service, see [copy data between on-premises and cloud using Data Factory](../tutorial-hybrid-copy-powershell.md).</span></span>

<span data-ttu-id="f6629-107">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f6629-107">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="f6629-108">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f6629-108">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="f6629-109">Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="f6629-109">Data Management Gateway</span></span>
<span data-ttu-id="f6629-110">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span><span class="sxs-lookup"><span data-stu-id="f6629-110">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="f6629-111">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="f6629-111">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6629-112">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-112">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="f6629-113">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="f6629-113">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span></span> <span data-ttu-id="f6629-114">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span><span class="sxs-lookup"><span data-stu-id="f6629-114">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-to-cloud"></a><span data-ttu-id="f6629-115">Walkthrough: copy on-premises data to cloud</span><span class="sxs-lookup"><span data-stu-id="f6629-115">Walkthrough: copy on-premises data to cloud</span></span>
<span data-ttu-id="f6629-116">In this walkthrough you do the following steps:</span><span class="sxs-lookup"><span data-stu-id="f6629-116">In this walkthrough you do the following steps:</span></span> 

1. <span data-ttu-id="f6629-117">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="f6629-117">Create a data factory.</span></span>
2. <span data-ttu-id="f6629-118">Create a data management gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-118">Create a data management gateway.</span></span> 
3. <span data-ttu-id="f6629-119">Create linked services for source and sink data stores.</span><span class="sxs-lookup"><span data-stu-id="f6629-119">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="f6629-120">Create datasets to represent input and output data.</span><span class="sxs-lookup"><span data-stu-id="f6629-120">Create datasets to represent input and output data.</span></span>
5. <span data-ttu-id="f6629-121">Create a pipeline with a copy activity to move the data.</span><span class="sxs-lookup"><span data-stu-id="f6629-121">Create a pipeline with a copy activity to move the data.</span></span>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="f6629-122">Prerequisites for the tutorial</span><span class="sxs-lookup"><span data-stu-id="f6629-122">Prerequisites for the tutorial</span></span>
<span data-ttu-id="f6629-123">Before you begin this walkthrough, you must have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="f6629-123">Before you begin this walkthrough, you must have the following prerequisites:</span></span>

* <span data-ttu-id="f6629-124">**Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="f6629-124">**Azure subscription**.</span></span>  <span data-ttu-id="f6629-125">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="f6629-125">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f6629-126">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span><span class="sxs-lookup"><span data-stu-id="f6629-126">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="f6629-127">**Azure Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="f6629-127">**Azure Storage Account**.</span></span> <span data-ttu-id="f6629-128">You use the blob storage as a **destination/sink** data store in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f6629-128">You use the blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="f6629-129">if you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="f6629-129">if you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span>
* <span data-ttu-id="f6629-130">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f6629-130">**SQL Server**.</span></span> <span data-ttu-id="f6629-131">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f6629-131">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="f6629-132">Create data factory</span><span class="sxs-lookup"><span data-stu-id="f6629-132">Create data factory</span></span>
<span data-ttu-id="f6629-133">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="f6629-133">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="f6629-134">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f6629-134">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f6629-135">Click **Create a resource**, click **Intelligence + analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="f6629-135">Click **Create a resource**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![New->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="f6629-137">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span><span class="sxs-lookup"><span data-stu-id="f6629-137">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span></span>

    ![Add to Startboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="f6629-139">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="f6629-139">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="f6629-140">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="f6629-140">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="f6629-141">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f6629-141">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="f6629-142">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span><span class="sxs-lookup"><span data-stu-id="f6629-142">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="f6629-143">Select the **Azure subscription** where you want the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="f6629-143">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="f6629-144">Select existing **resource group** or create a resource group.</span><span class="sxs-lookup"><span data-stu-id="f6629-144">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="f6629-145">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="f6629-145">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="f6629-146">Click **Create** on the **New data factory** page.</span><span class="sxs-lookup"><span data-stu-id="f6629-146">Click **Create** on the **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f6629-147">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../../role-based-access-control/built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span><span class="sxs-lookup"><span data-stu-id="f6629-147">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../../role-based-access-control/built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="f6629-148">After creation is complete, you see the **Data Factory** page as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="f6629-148">After creation is complete, you see the **Data Factory** page as shown in the following image:</span></span>

   ![Data Factory Home Page](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="f6629-150">Create gateway</span><span class="sxs-lookup"><span data-stu-id="f6629-150">Create gateway</span></span>
1. <span data-ttu-id="f6629-151">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="f6629-151">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>

    ![Author and Deploy Tile](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="f6629-153">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span><span class="sxs-lookup"><span data-stu-id="f6629-153">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="f6629-154">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span><span class="sxs-lookup"><span data-stu-id="f6629-154">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span></span>

   ![New data gateway on toolbar](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="f6629-156">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6629-156">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span></span>     

    ![Create Gateway page](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="f6629-158">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span><span class="sxs-lookup"><span data-stu-id="f6629-158">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="f6629-159">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-159">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="f6629-160">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span><span class="sxs-lookup"><span data-stu-id="f6629-160">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="f6629-161">This feature is also available for a logical gateway with a single node.</span><span class="sxs-lookup"><span data-stu-id="f6629-161">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="f6629-162">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="f6629-162">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="f6629-163">In the **Configure** page, click **Install directly on this computer**.</span><span class="sxs-lookup"><span data-stu-id="f6629-163">In the **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="f6629-164">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span><span class="sxs-lookup"><span data-stu-id="f6629-164">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="f6629-165">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span><span class="sxs-lookup"><span data-stu-id="f6629-165">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="f6629-166">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span><span class="sxs-lookup"><span data-stu-id="f6629-166">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="f6629-167">Do the same for Firefox (install add-in).</span><span class="sxs-lookup"><span data-stu-id="f6629-167">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="f6629-168">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span><span class="sxs-lookup"><span data-stu-id="f6629-168">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Gateway - Configure page](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="f6629-170">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span><span class="sxs-lookup"><span data-stu-id="f6629-170">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span></span> <span data-ttu-id="f6629-171">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span><span class="sxs-lookup"><span data-stu-id="f6629-171">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="f6629-172">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="f6629-172">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="f6629-173">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span><span class="sxs-lookup"><span data-stu-id="f6629-173">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span></span>

    <span data-ttu-id="f6629-174">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-174">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f6629-175">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span><span class="sxs-lookup"><span data-stu-id="f6629-175">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span></span> <span data-ttu-id="f6629-176">You can add additional users to the **Data Management Gateway Users** local Windows group.</span><span class="sxs-lookup"><span data-stu-id="f6629-176">You can add additional users to the **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="f6629-177">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-177">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span></span>
   >
   >
5. <span data-ttu-id="f6629-178">Wait for a couple of minutes or wait until you see the following notification message:</span><span class="sxs-lookup"><span data-stu-id="f6629-178">Wait for a couple of minutes or wait until you see the following notification message:</span></span>

    ![Gateway installation successful](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="f6629-180">Launch **Data Management Gateway Configuration Manager** application on your computer.</span><span class="sxs-lookup"><span data-stu-id="f6629-180">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="f6629-181">In the **Search** window, type **Data Management Gateway** to access this utility.</span><span class="sxs-lookup"><span data-stu-id="f6629-181">In the **Search** window, type **Data Management Gateway** to access this utility.</span></span> <span data-ttu-id="f6629-182">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="f6629-182">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Gateway Configuration Manager](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="f6629-184">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span><span class="sxs-lookup"><span data-stu-id="f6629-184">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span></span> <span data-ttu-id="f6629-185">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span><span class="sxs-lookup"><span data-stu-id="f6629-185">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="f6629-186">On the **Home** tab, you can also do the following operations:</span><span class="sxs-lookup"><span data-stu-id="f6629-186">On the **Home** tab, you can also do the following operations:</span></span>

   * <span data-ttu-id="f6629-187">**Register** a gateway with a key from the Azure portal by using the Register button.</span><span class="sxs-lookup"><span data-stu-id="f6629-187">**Register** a gateway with a key from the Azure portal by using the Register button.</span></span>
   * <span data-ttu-id="f6629-188">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span><span class="sxs-lookup"><span data-stu-id="f6629-188">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="f6629-189">**Schedule updates** to be installed at a specific time of the day.</span><span class="sxs-lookup"><span data-stu-id="f6629-189">**Schedule updates** to be installed at a specific time of the day.</span></span>
   * <span data-ttu-id="f6629-190">View when the gateway was **last updated**.</span><span class="sxs-lookup"><span data-stu-id="f6629-190">View when the gateway was **last updated**.</span></span>
   * <span data-ttu-id="f6629-191">Specify time at which an update to the gateway can be installed.</span><span class="sxs-lookup"><span data-stu-id="f6629-191">Specify time at which an update to the gateway can be installed.</span></span>
8. <span data-ttu-id="f6629-192">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span><span class="sxs-lookup"><span data-stu-id="f6629-192">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span></span> <span data-ttu-id="f6629-193">(optional) Click **Change** to use your own certificate instead.</span><span class="sxs-lookup"><span data-stu-id="f6629-193">(optional) Click **Change** to use your own certificate instead.</span></span> <span data-ttu-id="f6629-194">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="f6629-194">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span></span>

    ![Gateway certificate configuration](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="f6629-196">You can also do the following actions on the **Settings** tab:</span><span class="sxs-lookup"><span data-stu-id="f6629-196">You can also do the following actions on the **Settings** tab:</span></span>

   * <span data-ttu-id="f6629-197">View or export the certificate being used by the gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-197">View or export the certificate being used by the gateway.</span></span>
   * <span data-ttu-id="f6629-198">Change the HTTPS endpoint used by the gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-198">Change the HTTPS endpoint used by the gateway.</span></span>    
   * <span data-ttu-id="f6629-199">Set an HTTP proxy to be used by the gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-199">Set an HTTP proxy to be used by the gateway.</span></span>     
9. <span data-ttu-id="f6629-200">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-200">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span></span> <span data-ttu-id="f6629-201">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span><span class="sxs-lookup"><span data-stu-id="f6629-201">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Diagnostics tab](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="f6629-203">You can also perform the following actions in the **Diagnostics** tab:</span><span class="sxs-lookup"><span data-stu-id="f6629-203">You can also perform the following actions in the **Diagnostics** tab:</span></span>

   * <span data-ttu-id="f6629-204">Use **Test Connection** section to an on-premises data source using the gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-204">Use **Test Connection** section to an on-premises data source using the gateway.</span></span>
   * <span data-ttu-id="f6629-205">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span><span class="sxs-lookup"><span data-stu-id="f6629-205">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="f6629-206">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span><span class="sxs-lookup"><span data-stu-id="f6629-206">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="f6629-207">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span><span class="sxs-lookup"><span data-stu-id="f6629-207">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span></span>
11. <span data-ttu-id="f6629-208">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span><span class="sxs-lookup"><span data-stu-id="f6629-208">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span></span>
12. <span data-ttu-id="f6629-209">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="f6629-209">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span></span>  <span data-ttu-id="f6629-210">If you click it, you should see the associated JSON.</span><span class="sxs-lookup"><span data-stu-id="f6629-210">If you click it, you should see the associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="f6629-211">Create linked services</span><span class="sxs-lookup"><span data-stu-id="f6629-211">Create linked services</span></span>
<span data-ttu-id="f6629-212">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f6629-212">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="f6629-213">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f6629-213">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span></span> <span data-ttu-id="f6629-214">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span><span class="sxs-lookup"><span data-stu-id="f6629-214">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span></span>

#### <a name="add-a-linked-service-to-an-on-premises-sql-server-database"></a><span data-ttu-id="f6629-215">Add a linked service to an on-premises SQL Server database</span><span class="sxs-lookup"><span data-stu-id="f6629-215">Add a linked service to an on-premises SQL Server database</span></span>
1. <span data-ttu-id="f6629-216">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f6629-216">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span></span>

   ![New SQL Server linked service](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="f6629-218">In the **JSON editor** on the right, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="f6629-218">In the **JSON editor** on the right, do the following steps:</span></span>

   1. <span data-ttu-id="f6629-219">For the **gatewayName**, specify **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="f6629-219">For the **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="f6629-220">In the **connectionString**, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="f6629-220">In the **connectionString**, do the following steps:</span></span>    

      1. <span data-ttu-id="f6629-221">For **servername**, enter the name of the server that hosts the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="f6629-221">For **servername**, enter the name of the server that hosts the SQL Server database.</span></span>
      2. <span data-ttu-id="f6629-222">For **databasename**, enter the name of the database.</span><span class="sxs-lookup"><span data-stu-id="f6629-222">For **databasename**, enter the name of the database.</span></span>
      3. <span data-ttu-id="f6629-223">Click **Encrypt** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="f6629-223">Click **Encrypt** button on the toolbar.</span></span> <span data-ttu-id="f6629-224">You see the Credentials Manager application.</span><span class="sxs-lookup"><span data-stu-id="f6629-224">You see the Credentials Manager application.</span></span>

         ![Credentials Manager application](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="f6629-226">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6629-226">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="f6629-227">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span><span class="sxs-lookup"><span data-stu-id="f6629-227">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span></span>
      5. <span data-ttu-id="f6629-228">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f6629-228">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span></span>

         <span data-ttu-id="f6629-229">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span><span class="sxs-lookup"><span data-stu-id="f6629-229">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="f6629-230">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="f6629-230">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="f6629-231">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="f6629-231">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span></span> <span data-ttu-id="f6629-232">You should see the linked service in the tree view.</span><span class="sxs-lookup"><span data-stu-id="f6629-232">You should see the linked service in the tree view.</span></span>

      ![SQL Server linked service in the tree view](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="f6629-234">Add a linked service for an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="f6629-234">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="f6629-235">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="f6629-235">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="f6629-236">Enter the name of your Azure storage account for the **Account name**.</span><span class="sxs-lookup"><span data-stu-id="f6629-236">Enter the name of your Azure storage account for the **Account name**.</span></span>
3. <span data-ttu-id="f6629-237">Enter the key for your Azure storage account for the **Account key**.</span><span class="sxs-lookup"><span data-stu-id="f6629-237">Enter the key for your Azure storage account for the **Account key**.</span></span>
4. <span data-ttu-id="f6629-238">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f6629-238">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="f6629-239">Create datasets</span><span class="sxs-lookup"><span data-stu-id="f6629-239">Create datasets</span></span>
<span data-ttu-id="f6629-240">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span><span class="sxs-lookup"><span data-stu-id="f6629-240">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="f6629-241">Before creating datasets, do the following steps (detailed steps follows the list):</span><span class="sxs-lookup"><span data-stu-id="f6629-241">Before creating datasets, do the following steps (detailed steps follows the list):</span></span>

* <span data-ttu-id="f6629-242">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span><span class="sxs-lookup"><span data-stu-id="f6629-242">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span></span>
* <span data-ttu-id="f6629-243">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f6629-243">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-the-tutorial"></a><span data-ttu-id="f6629-244">Prepare On-premises SQL Server for the tutorial</span><span class="sxs-lookup"><span data-stu-id="f6629-244">Prepare On-premises SQL Server for the tutorial</span></span>
1. <span data-ttu-id="f6629-245">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span><span class="sxs-lookup"><span data-stu-id="f6629-245">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="f6629-246">Insert some sample into the table:</span><span class="sxs-lookup"><span data-stu-id="f6629-246">Insert some sample into the table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="f6629-247">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="f6629-247">Create input dataset</span></span>

1. <span data-ttu-id="f6629-248">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span><span class="sxs-lookup"><span data-stu-id="f6629-248">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="f6629-249">Replace the JSON in the right pane with the following text:</span><span class="sxs-lookup"><span data-stu-id="f6629-249">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="f6629-250">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="f6629-250">Note the following points:</span></span>

   * <span data-ttu-id="f6629-251">**type** is set to **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="f6629-251">**type** is set to **SqlServerTable**.</span></span>
   * <span data-ttu-id="f6629-252">**tableName** is set to **emp**.</span><span class="sxs-lookup"><span data-stu-id="f6629-252">**tableName** is set to **emp**.</span></span>
   * <span data-ttu-id="f6629-253">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span><span class="sxs-lookup"><span data-stu-id="f6629-253">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="f6629-254">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span><span class="sxs-lookup"><span data-stu-id="f6629-254">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span></span> <span data-ttu-id="f6629-255">It denotes the input data is produced external to the Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="f6629-255">It denotes the input data is produced external to the Azure Data Factory service.</span></span> <span data-ttu-id="f6629-256">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span><span class="sxs-lookup"><span data-stu-id="f6629-256">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span></span>    

   <span data-ttu-id="f6629-257">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span><span class="sxs-lookup"><span data-stu-id="f6629-257">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="f6629-258">Click **Deploy** on the command bar to deploy the dataset.</span><span class="sxs-lookup"><span data-stu-id="f6629-258">Click **Deploy** on the command bar to deploy the dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="f6629-259">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="f6629-259">Create output dataset</span></span>

1. <span data-ttu-id="f6629-260">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="f6629-260">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="f6629-261">Replace the JSON in the right pane with the following text:</span><span class="sxs-lookup"><span data-stu-id="f6629-261">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="f6629-262">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="f6629-262">Note the following points:</span></span>

   * <span data-ttu-id="f6629-263">**type** is set to **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="f6629-263">**type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="f6629-264">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span><span class="sxs-lookup"><span data-stu-id="f6629-264">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="f6629-265">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span><span class="sxs-lookup"><span data-stu-id="f6629-265">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span></span> <span data-ttu-id="f6629-266">Create the **adftutorial** container if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="f6629-266">Create the **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="f6629-267">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span><span class="sxs-lookup"><span data-stu-id="f6629-267">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="f6629-268">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f6629-268">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span></span>

   <span data-ttu-id="f6629-269">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="f6629-269">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="f6629-270">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span><span class="sxs-lookup"><span data-stu-id="f6629-270">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span></span> <span data-ttu-id="f6629-271">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span><span class="sxs-lookup"><span data-stu-id="f6629-271">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="f6629-272">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span><span class="sxs-lookup"><span data-stu-id="f6629-272">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="f6629-273">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span><span class="sxs-lookup"><span data-stu-id="f6629-273">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="f6629-274">Click **Deploy** on the command bar to deploy the dataset.</span><span class="sxs-lookup"><span data-stu-id="f6629-274">Click **Deploy** on the command bar to deploy the dataset.</span></span> <span data-ttu-id="f6629-275">Confirm that you see both the datasets in the tree view.</span><span class="sxs-lookup"><span data-stu-id="f6629-275">Confirm that you see both the datasets in the tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="f6629-276">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="f6629-276">Create pipeline</span></span>
<span data-ttu-id="f6629-277">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span><span class="sxs-lookup"><span data-stu-id="f6629-277">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="f6629-278">In Data Factory Editor, click **... More**, and click **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f6629-278">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="f6629-279">Replace the JSON in the right pane with the following text:</span><span class="sxs-lookup"><span data-stu-id="f6629-279">Replace the JSON in the right pane with the following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL to Azure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server to blob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="f6629-280">Replace the value of the **start** property with the current day and **end** value with the next day.</span><span class="sxs-lookup"><span data-stu-id="f6629-280">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span>
   >
   >

   <span data-ttu-id="f6629-281">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="f6629-281">Note the following points:</span></span>

   * <span data-ttu-id="f6629-282">In the activities section, there is only activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="f6629-282">In the activities section, there is only activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="f6629-283">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="f6629-283">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span></span>
   * <span data-ttu-id="f6629-284">In the **typeProperties** section, **SqlSource** is specified as the **source type** and \*\*BlobSink \*\*is specified as the **sink type**.</span><span class="sxs-lookup"><span data-stu-id="f6629-284">In the **typeProperties** section, **SqlSource** is specified as the **source type** and \*\*BlobSink \*\*is specified as the **sink type**.</span></span>
   * <span data-ttu-id="f6629-285">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="f6629-285">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="f6629-286">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="f6629-286">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="f6629-287">For example: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="f6629-287">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="f6629-288">The **end** time is optional, but we use it in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f6629-288">The **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="f6629-289">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="f6629-289">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="f6629-290">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="f6629-290">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="f6629-291">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span><span class="sxs-lookup"><span data-stu-id="f6629-291">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="f6629-292">In the example, there are 24 data slices as each data slice is produced hourly.</span><span class="sxs-lookup"><span data-stu-id="f6629-292">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="f6629-293">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span><span class="sxs-lookup"><span data-stu-id="f6629-293">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="f6629-294">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span><span class="sxs-lookup"><span data-stu-id="f6629-294">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="f6629-295">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="f6629-295">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="f6629-296">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="f6629-296">**Congratulations!**</span></span> <span data-ttu-id="f6629-297">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f6629-297">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span></span>

#### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="f6629-298">View the data factory in a Diagram View</span><span class="sxs-lookup"><span data-stu-id="f6629-298">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="f6629-299">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span><span class="sxs-lookup"><span data-stu-id="f6629-299">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="f6629-300">:</span><span class="sxs-lookup"><span data-stu-id="f6629-300">:</span></span>

    ![Diagram Link](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="f6629-302">You should see the diagram similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="f6629-302">You should see the diagram similar to the following image:</span></span>

    ![Diagram View](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="f6629-304">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span><span class="sxs-lookup"><span data-stu-id="f6629-304">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="f6629-305">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span><span class="sxs-lookup"><span data-stu-id="f6629-305">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="f6629-306">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="f6629-306">Monitor pipeline</span></span>
<span data-ttu-id="f6629-307">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="f6629-307">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="f6629-308">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span><span class="sxs-lookup"><span data-stu-id="f6629-308">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span></span> <span data-ttu-id="f6629-309">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f6629-309">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="f6629-310">In the diagram, double-click **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="f6629-310">In the diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![EmpOnPremSQLTable slices](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="f6629-312">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span><span class="sxs-lookup"><span data-stu-id="f6629-312">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span></span> <span data-ttu-id="f6629-313">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span><span class="sxs-lookup"><span data-stu-id="f6629-313">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span></span> <span data-ttu-id="f6629-314">Confirm that no slices show up in the **Problem slices** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f6629-314">Confirm that no slices show up in the **Problem slices** section at the bottom.</span></span> <span data-ttu-id="f6629-315">To view all the slices, click **See More** at the bottom of the list of slices.</span><span class="sxs-lookup"><span data-stu-id="f6629-315">To view all the slices, click **See More** at the bottom of the list of slices.</span></span>
3. <span data-ttu-id="f6629-316">Now, In the **Datasets** page, click **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="f6629-316">Now, In the **Datasets** page, click **OutputBlobTable**.</span></span>

    ![OputputBlobTable slices](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="f6629-318">Click any data slice from the list and you should see the **Data Slice** page.</span><span class="sxs-lookup"><span data-stu-id="f6629-318">Click any data slice from the list and you should see the **Data Slice** page.</span></span> <span data-ttu-id="f6629-319">You see activity runs for the slice.</span><span class="sxs-lookup"><span data-stu-id="f6629-319">You see activity runs for the slice.</span></span> <span data-ttu-id="f6629-320">You see only one activity run usually.</span><span class="sxs-lookup"><span data-stu-id="f6629-320">You see only one activity run usually.</span></span>  

    ![Data Slice Blade](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="f6629-322">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span><span class="sxs-lookup"><span data-stu-id="f6629-322">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="f6629-323">Click the **activity run** from the list at the bottom to see **activity run details**.</span><span class="sxs-lookup"><span data-stu-id="f6629-323">Click the **activity run** from the list at the bottom to see **activity run details**.</span></span>

   ![Activity Run Details page](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="f6629-325">You would see information such as throughput, duration, and the gateway used to transfer the data.</span><span class="sxs-lookup"><span data-stu-id="f6629-325">You would see information such as throughput, duration, and the gateway used to transfer the data.</span></span>
6. <span data-ttu-id="f6629-326">Click **X** to close all the pages until you</span><span class="sxs-lookup"><span data-stu-id="f6629-326">Click **X** to close all the pages until you</span></span>
7. <span data-ttu-id="f6629-327">get back to the home page for the **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="f6629-327">get back to the home page for the **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="f6629-328">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span><span class="sxs-lookup"><span data-stu-id="f6629-328">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="f6629-329">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span><span class="sxs-lookup"><span data-stu-id="f6629-329">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span></span>

   ![Azure Storage Explorer](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="f6629-331">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6629-331">Next steps</span></span>
* <span data-ttu-id="f6629-332">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="f6629-332">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span></span>
* <span data-ttu-id="f6629-333">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span><span class="sxs-lookup"><span data-stu-id="f6629-333">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span></span>
