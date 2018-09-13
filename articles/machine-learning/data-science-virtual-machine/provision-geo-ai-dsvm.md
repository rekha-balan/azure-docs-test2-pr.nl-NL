---
title: Provision a Geo Artificial Intelligence Virtual Machine on Azure - Azure | Microsoft Docs
description: How to provision a Geo AI Virtual Machine on Azure.
keywords: deep learning, AI, data science tools, data science virtual machine, Geospatial analytics
services: machine-learning
documentationcenter: ''
author: gopitk
manager: cgronlun
ms.assetid: ''
ms.service: machine-learning
ms.component: data-science-vm
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/05/2018
ms.author: gokuma
ms.openlocfilehash: 93dfe6594aeaf45a6905fe8cb55c98dd37cc9599
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865547"
---
# <a name="provision-a-geo-artificial-intelligence-virtual-machine-on-azure"></a><span data-ttu-id="391e6-104">Provision a Geo Artificial Intelligence Virtual Machine on Azure</span><span class="sxs-lookup"><span data-stu-id="391e6-104">Provision a Geo Artificial Intelligence Virtual Machine on Azure</span></span> 

<span data-ttu-id="391e6-105">The Geo AI Data Science Virtual Machine (Geo-DSVM) is an extension of the popular [Azure Data Science Virtual Machine](http://aka.ms/dsvm) that is specially configured to combine AI and geospatial analytics.</span><span class="sxs-lookup"><span data-stu-id="391e6-105">The Geo AI Data Science Virtual Machine (Geo-DSVM) is an extension of the popular [Azure Data Science Virtual Machine](http://aka.ms/dsvm) that is specially configured to combine AI and geospatial analytics.</span></span> <span data-ttu-id="391e6-106">The geospatial analytics in the VM are powered by [ArcGIS Pro](https://www.arcgis.com/features/index.html).</span><span class="sxs-lookup"><span data-stu-id="391e6-106">The geospatial analytics in the VM are powered by [ArcGIS Pro](https://www.arcgis.com/features/index.html).</span></span> <span data-ttu-id="391e6-107">The Data Science VM enables the rapid training of machine learning models, and even of deep learning models, on data that is enriched with geographic information.</span><span class="sxs-lookup"><span data-stu-id="391e6-107">The Data Science VM enables the rapid training of machine learning models, and even of deep learning models, on data that is enriched with geographic information.</span></span> <span data-ttu-id="391e6-108">It is supported on Windows 2016 DSVM only.</span><span class="sxs-lookup"><span data-stu-id="391e6-108">It is supported on Windows 2016 DSVM only.</span></span> 

<span data-ttu-id="391e6-109">The Geo-DSVM contains several tools for AI including:</span><span class="sxs-lookup"><span data-stu-id="391e6-109">The Geo-DSVM contains several tools for AI including:</span></span>

- <span data-ttu-id="391e6-110">GPU editions of popular deep learning frameworks like Microsoft Cognitive Toolkit, TensorFlow, Keras, Caffe2, Chainer;</span><span class="sxs-lookup"><span data-stu-id="391e6-110">GPU editions of popular deep learning frameworks like Microsoft Cognitive Toolkit, TensorFlow, Keras, Caffe2, Chainer;</span></span> 
- <span data-ttu-id="391e6-111">tools to acquire and pre-process image, textual data,</span><span class="sxs-lookup"><span data-stu-id="391e6-111">tools to acquire and pre-process image, textual data,</span></span> 
- <span data-ttu-id="391e6-112">tools for development activities such as Microsoft R Server Developer Edition, Anaconda Python, Jupyter notebooks for Python and R, IDEs for Python and R, SQL databases</span><span class="sxs-lookup"><span data-stu-id="391e6-112">tools for development activities such as Microsoft R Server Developer Edition, Anaconda Python, Jupyter notebooks for Python and R, IDEs for Python and R, SQL databases</span></span>
- <span data-ttu-id="391e6-113">ESRI's ArcGIS Pro desktop software along with Python and R interfaces that can work with the geospatial data from your AI applications.</span><span class="sxs-lookup"><span data-stu-id="391e6-113">ESRI's ArcGIS Pro desktop software along with Python and R interfaces that can work with the geospatial data from your AI applications.</span></span> 


## <a name="create-your-geo-ai-data-science-vm"></a><span data-ttu-id="391e6-114">Create your Geo AI Data Science VM</span><span class="sxs-lookup"><span data-stu-id="391e6-114">Create your Geo AI Data Science VM</span></span>

<span data-ttu-id="391e6-115">Here is the procedure to create an instance of the Geo AI Data Science VM:</span><span class="sxs-lookup"><span data-stu-id="391e6-115">Here is the procedure to create an instance of the Geo AI Data Science VM:</span></span> 


1. <span data-ttu-id="391e6-116">Navigate to the virtual machine listing on [Azure portal](https://ms.portal.azure.com/#create/microsoft-ads.geodsvmwindows).</span><span class="sxs-lookup"><span data-stu-id="391e6-116">Navigate to the virtual machine listing on [Azure portal](https://ms.portal.azure.com/#create/microsoft-ads.geodsvmwindows).</span></span>
2. <span data-ttu-id="391e6-117">Select the **Create** button at the bottom to be taken into a wizard.</span><span class="sxs-lookup"><span data-stu-id="391e6-117">Select the **Create** button at the bottom to be taken into a wizard.</span></span>
<span data-ttu-id="391e6-118">![create-geo-ai-dsvm](./media/provision-geo-ai-dsvm/Create-Geo-AI.png)</span><span class="sxs-lookup"><span data-stu-id="391e6-118">![create-geo-ai-dsvm](./media/provision-geo-ai-dsvm/Create-Geo-AI.png)</span></span>
3. <span data-ttu-id="391e6-119">The wizard used to create the Geo-DSVM requires **inputs** for each of the **four steps** enumerated on the right of this figure.</span><span class="sxs-lookup"><span data-stu-id="391e6-119">The wizard used to create the Geo-DSVM requires **inputs** for each of the **four steps** enumerated on the right of this figure.</span></span> <span data-ttu-id="391e6-120">Here are the inputs needed to configure each of these steps:</span><span class="sxs-lookup"><span data-stu-id="391e6-120">Here are the inputs needed to configure each of these steps:</span></span>



   - <span data-ttu-id="391e6-121">**Basics**</span><span class="sxs-lookup"><span data-stu-id="391e6-121">**Basics**</span></span>

      1. <span data-ttu-id="391e6-122">**Name**: Name of the data science server you are creating.</span><span class="sxs-lookup"><span data-stu-id="391e6-122">**Name**: Name of the data science server you are creating.</span></span>

      2. <span data-ttu-id="391e6-123">**User Name**: Admin account login id.</span><span class="sxs-lookup"><span data-stu-id="391e6-123">**User Name**: Admin account login id.</span></span>

      3. <span data-ttu-id="391e6-124">**Password**: Admin account password.</span><span class="sxs-lookup"><span data-stu-id="391e6-124">**Password**: Admin account password.</span></span>

      4. <span data-ttu-id="391e6-125">**Subscription**: If you have more than one subscription, select the one on which the machine is to be created and billed.</span><span class="sxs-lookup"><span data-stu-id="391e6-125">**Subscription**: If you have more than one subscription, select the one on which the machine is to be created and billed.</span></span>

      5. <span data-ttu-id="391e6-126">**Resource Group**: You can create a new one or use an **empty** existing Azure resource group in your subscription.</span><span class="sxs-lookup"><span data-stu-id="391e6-126">**Resource Group**: You can create a new one or use an **empty** existing Azure resource group in your subscription.</span></span>

      6. <span data-ttu-id="391e6-127">**Location**: Select the data center that is most appropriate.</span><span class="sxs-lookup"><span data-stu-id="391e6-127">**Location**: Select the data center that is most appropriate.</span></span> <span data-ttu-id="391e6-128">Usually it is the data center that has most of your data or is closest to your physical location for fastest network access.</span><span class="sxs-lookup"><span data-stu-id="391e6-128">Usually it is the data center that has most of your data or is closest to your physical location for fastest network access.</span></span> <span data-ttu-id="391e6-129">If you need to do deep learning on GPU, you must choose one of the locations in Azure that has the NC-Series GPU VM instances.</span><span class="sxs-lookup"><span data-stu-id="391e6-129">If you need to do deep learning on GPU, you must choose one of the locations in Azure that has the NC-Series GPU VM instances.</span></span> <span data-ttu-id="391e6-130">Currently the locations that have GPU VMs are: **East US, North Central US, South Central US, West US 2, North Europe, West Europe**.</span><span class="sxs-lookup"><span data-stu-id="391e6-130">Currently the locations that have GPU VMs are: **East US, North Central US, South Central US, West US 2, North Europe, West Europe**.</span></span> <span data-ttu-id="391e6-131">For the latest list, check the [Azure Products by Region Page](https://azure.microsoft.com/regions/services/) and look for **NC-Series** under **Compute**.</span><span class="sxs-lookup"><span data-stu-id="391e6-131">For the latest list, check the [Azure Products by Region Page](https://azure.microsoft.com/regions/services/) and look for **NC-Series** under **Compute**.</span></span> 


   - <span data-ttu-id="391e6-132">**Settings**: Select one of the NC-Series GPU virtual machine size if you plan to run deep learning on  GPU on your Geo DSVM.</span><span class="sxs-lookup"><span data-stu-id="391e6-132">**Settings**: Select one of the NC-Series GPU virtual machine size if you plan to run deep learning on  GPU on your Geo DSVM.</span></span> <span data-ttu-id="391e6-133">Otherwise, you can choose one of the CPU based instance.</span><span class="sxs-lookup"><span data-stu-id="391e6-133">Otherwise, you can choose one of the CPU based instance.</span></span>  <span data-ttu-id="391e6-134">Create a storage account for your VM.</span><span class="sxs-lookup"><span data-stu-id="391e6-134">Create a storage account for your VM.</span></span> 
   
   - <span data-ttu-id="391e6-135">**Summary**: Verify that all information you entered is correct.</span><span class="sxs-lookup"><span data-stu-id="391e6-135">**Summary**: Verify that all information you entered is correct.</span></span>

   - <span data-ttu-id="391e6-136">**Buy**: Click **Buy** to start the provisioning.</span><span class="sxs-lookup"><span data-stu-id="391e6-136">**Buy**: Click **Buy** to start the provisioning.</span></span> <span data-ttu-id="391e6-137">A link is provided to the terms of the service.</span><span class="sxs-lookup"><span data-stu-id="391e6-137">A link is provided to the terms of the service.</span></span> <span data-ttu-id="391e6-138">The VM does not have any additional charges beyond the compute for the server size you chose in the **Size** step.</span><span class="sxs-lookup"><span data-stu-id="391e6-138">The VM does not have any additional charges beyond the compute for the server size you chose in the **Size** step.</span></span> 

>[!NOTE]
> <span data-ttu-id="391e6-139">The provisioning should take about 20-30 minutes.</span><span class="sxs-lookup"><span data-stu-id="391e6-139">The provisioning should take about 20-30 minutes.</span></span> <span data-ttu-id="391e6-140">The status of the provisioning is displayed on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="391e6-140">The status of the provisioning is displayed on the Azure portal.</span></span>


## <a name="how-to-access-the-geo-ai-data-science-virtual-machine"></a><span data-ttu-id="391e6-141">How to access the Geo AI Data Science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="391e6-141">How to access the Geo AI Data Science Virtual Machine</span></span>

<span data-ttu-id="391e6-142">Once your VM is created, you are ready to start using the tools that are installed and pre-configured on it.</span><span class="sxs-lookup"><span data-stu-id="391e6-142">Once your VM is created, you are ready to start using the tools that are installed and pre-configured on it.</span></span> <span data-ttu-id="391e6-143">There are start menu tiles and desktop icons for many of the tools.</span><span class="sxs-lookup"><span data-stu-id="391e6-143">There are start menu tiles and desktop icons for many of the tools.</span></span> <span data-ttu-id="391e6-144">You can remote desktop into it using the Admin account credentials that you configured in the preceding **Basics** section.</span><span class="sxs-lookup"><span data-stu-id="391e6-144">You can remote desktop into it using the Admin account credentials that you configured in the preceding **Basics** section.</span></span> 


## <a name="using-arcgis-pro-installed-in-the-vm"></a><span data-ttu-id="391e6-145">Using ArcGIS Pro installed in the VM</span><span class="sxs-lookup"><span data-stu-id="391e6-145">Using ArcGIS Pro installed in the VM</span></span>

<span data-ttu-id="391e6-146">The Geo-DSVM already has ArcGIS Pro desktop pre-installed and the environment pre-configured to work with all the tools in the DSVM.</span><span class="sxs-lookup"><span data-stu-id="391e6-146">The Geo-DSVM already has ArcGIS Pro desktop pre-installed and the environment pre-configured to work with all the tools in the DSVM.</span></span> <span data-ttu-id="391e6-147">When you start ArcGIS it prompts you for a login to your ArcGIS account.</span><span class="sxs-lookup"><span data-stu-id="391e6-147">When you start ArcGIS it prompts you for a login to your ArcGIS account.</span></span> <span data-ttu-id="391e6-148">If you already have an ArcGIS account and have licenses for the software, you can use your existing credentials.</span><span class="sxs-lookup"><span data-stu-id="391e6-148">If you already have an ArcGIS account and have licenses for the software, you can use your existing credentials.</span></span>  

![Arc-GIS-Logon](./media/provision-geo-ai-dsvm/ArcGISLogon.png)

<span data-ttu-id="391e6-150">Otherwise, you can sign up for new ArcGIS account and license or get a [free trial](https://www.arcgis.com/features/free-trial.html).</span><span class="sxs-lookup"><span data-stu-id="391e6-150">Otherwise, you can sign up for new ArcGIS account and license or get a [free trial](https://www.arcgis.com/features/free-trial.html).</span></span> 

![ArcGIS-Free-Trial](./media/provision-geo-ai-dsvm/ArcGIS-Free-Trial.png)

<span data-ttu-id="391e6-152">Once you have signup for a either a paid or a free trial ArcGIS account, you can authorize ArcGIS Pro for your account by following the instructions in the [Getting Started with ArcGIS Pro documentation](http://www.esri.com/library/brochures/getting-started-with-arcgis-pro.pdf).</span><span class="sxs-lookup"><span data-stu-id="391e6-152">Once you have signup for a either a paid or a free trial ArcGIS account, you can authorize ArcGIS Pro for your account by following the instructions in the [Getting Started with ArcGIS Pro documentation](http://www.esri.com/library/brochures/getting-started-with-arcgis-pro.pdf).</span></span> 

<span data-ttu-id="391e6-153">After you sign in to ArcGIS Pro desktop with your ArcGIS account, you are ready to begin using the data science tools that are installed and configured on the VM for your Geospatial analytics and machine learning projects.</span><span class="sxs-lookup"><span data-stu-id="391e6-153">After you sign in to ArcGIS Pro desktop with your ArcGIS account, you are ready to begin using the data science tools that are installed and configured on the VM for your Geospatial analytics and machine learning projects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="391e6-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="391e6-154">Next steps</span></span>

<span data-ttu-id="391e6-155">Get started using the Geo AI Data Science VM with guidance from the following topics:</span><span class="sxs-lookup"><span data-stu-id="391e6-155">Get started using the Geo AI Data Science VM with guidance from the following topics:</span></span>

* [<span data-ttu-id="391e6-156">Use the Geo AI Data Science VM</span><span class="sxs-lookup"><span data-stu-id="391e6-156">Use the Geo AI Data Science VM</span></span>](use-geo-ai-dsvm.md)