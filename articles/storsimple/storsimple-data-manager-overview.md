---
title: Microsoft Azure StorSimple Data Manager overview | Microsoft Docs
description: Provides an overview of the StorSimple Data Manager serivce (private preview)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 624084ecf9a83f32711d7aa0dca040c1327f30fb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549628"
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="4326c-103">StorSimple Data Manager overview (Private Preview)</span><span class="sxs-lookup"><span data-stu-id="4326c-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="4326c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4326c-104">Overview</span></span>

<span data-ttu-id="4326c-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses the complexities of unstructured data commonly associated with file shares.</span><span class="sxs-lookup"><span data-stu-id="4326c-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses the complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="4326c-106">StorSimple uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span><span class="sxs-lookup"><span data-stu-id="4326c-106">StorSimple uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="4326c-107">Integrated data protection, with local and cloud snapshots, eliminates the need for a sprawling storage infrastructure.</span><span class="sxs-lookup"><span data-stu-id="4326c-107">Integrated data protection, with local and cloud snapshots, eliminates the need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="4326c-108">Archival and disaster recovery is also seamless with the cloud acting as an offsite location.</span><span class="sxs-lookup"><span data-stu-id="4326c-108">Archival and disaster recovery is also seamless with the cloud acting as an offsite location.</span></span>

<span data-ttu-id="4326c-109">The data transformation service that we are introducing in this document, allows you to seamlessly access the StorSimple data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4326c-109">The data transformation service that we are introducing in this document, allows you to seamlessly access the StorSimple data in the cloud.</span></span> <span data-ttu-id="4326c-110">This service provides APIs to extract data from StorSimple and present it to other Azure services in formats that can be readily consumed.</span><span class="sxs-lookup"><span data-stu-id="4326c-110">This service provides APIs to extract data from StorSimple and present it to other Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="4326c-111">The formats supported in this preview are Azure blobs and Azure Media Services assets.</span><span class="sxs-lookup"><span data-stu-id="4326c-111">The formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="4326c-112">This transformation enables you to easily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search to operate data on StorSimple 8000 series on-premises device.</span><span class="sxs-lookup"><span data-stu-id="4326c-112">This transformation enables you to easily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search to operate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="4326c-113">A high-level block diagram illustrating this is shown below.</span><span class="sxs-lookup"><span data-stu-id="4326c-113">A high-level block diagram illustrating this is shown below.</span></span>

![High-level diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="4326c-115">This document explains how you can sign up for a private preview of this service.</span><span class="sxs-lookup"><span data-stu-id="4326c-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="4326c-116">It also explains how you can use this service to write applications that use StorSimple data and other Azure services in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4326c-116">It also explains how you can use this service to write applications that use StorSimple data and other Azure services in the cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="4326c-117">Sign up for Data Manager preview</span><span class="sxs-lookup"><span data-stu-id="4326c-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="4326c-118">Before you sign up for the Data Manager service, review the following prerequisites.</span><span class="sxs-lookup"><span data-stu-id="4326c-118">Before you sign up for the Data Manager service, review the following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4326c-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4326c-119">Prerequisites</span></span>

<span data-ttu-id="4326c-120">This exercise assumes that you have</span><span class="sxs-lookup"><span data-stu-id="4326c-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="4326c-121">an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4326c-121">an active Azure subscription.</span></span>
* <span data-ttu-id="4326c-122">access to a registered StorSimple 8000 series device</span><span class="sxs-lookup"><span data-stu-id="4326c-122">access to a registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="4326c-123">all the keys associated with the StorSimple 8000 series device.</span><span class="sxs-lookup"><span data-stu-id="4326c-123">all the keys associated with the StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="4326c-124">Sign up</span><span class="sxs-lookup"><span data-stu-id="4326c-124">Sign up</span></span>

<span data-ttu-id="4326c-125">The StorSimple Data Manager is in private preview.</span><span class="sxs-lookup"><span data-stu-id="4326c-125">The StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="4326c-126">Perform the following steps to sign up for a private preview of this service:</span><span class="sxs-lookup"><span data-stu-id="4326c-126">Perform the following steps to sign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="4326c-127">Log into the Azure portal with the StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="4326c-127">Log into the Azure portal with the StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="4326c-128">Use your Azure credentials to log in.</span><span class="sxs-lookup"><span data-stu-id="4326c-128">Use your Azure credentials to log in.</span></span>

2.  <span data-ttu-id="4326c-129">Click the **+** icon to create a service.</span><span class="sxs-lookup"><span data-stu-id="4326c-129">Click the **+** icon to create a service.</span></span> <span data-ttu-id="4326c-130">Click **Storage** and then click **See All** in the blade that opens up.</span><span class="sxs-lookup"><span data-stu-id="4326c-130">Click **Storage** and then click **See All** in the blade that opens up.</span></span>

    ![Search StorSimple Data Manager Icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="4326c-132">You see the StorSimple Data Manager icon.</span><span class="sxs-lookup"><span data-stu-id="4326c-132">You see the StorSimple Data Manager icon.</span></span>

    ![Select StorSimple Data Manager Icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-overview/select-data-manager-Icon.png)

4. <span data-ttu-id="4326c-134">Click StorSimple Data Manager icon and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4326c-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="4326c-135">Pick the subscription that you want to enable for the private preview and then click **Sign me up!**</span><span class="sxs-lookup"><span data-stu-id="4326c-135">Pick the subscription that you want to enable for the private preview and then click **Sign me up!**</span></span>

    ![Sign me up](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="4326c-137">This sends a request to onboard you.</span><span class="sxs-lookup"><span data-stu-id="4326c-137">This sends a request to onboard you.</span></span> <span data-ttu-id="4326c-138">We will onboard you as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="4326c-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="4326c-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span><span class="sxs-lookup"><span data-stu-id="4326c-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="4326c-140">To easily access the StorSimple Data Manager service, click the star icon to pin it to your favorites.</span><span class="sxs-lookup"><span data-stu-id="4326c-140">To easily access the StorSimple Data Manager service, click the star icon to pin it to your favorites.</span></span>

    ![Access StorSimple Data Managers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="4326c-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="4326c-142">Next steps</span></span>

<span data-ttu-id="4326c-143">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="4326c-143">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>




