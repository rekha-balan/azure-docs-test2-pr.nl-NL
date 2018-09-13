---
title: Logging for Machine Learning web services | Microsoft Docs
description: Learn how to enable logging for Machine Learning web services. Logging provides additional information to help troubleshoot the APIs.
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.component: studio
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.openlocfilehash: 4e1545c8fd05795c683b24c029376a3d1e6d85b8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857118"
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="6fa95-104">Enable logging for Machine Learning web services</span><span class="sxs-lookup"><span data-stu-id="6fa95-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="6fa95-105">This document provides information on the logging capability of Machine Learning web services.</span><span class="sxs-lookup"><span data-stu-id="6fa95-105">This document provides information on the logging capability of Machine Learning web services.</span></span> <span data-ttu-id="6fa95-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span><span class="sxs-lookup"><span data-stu-id="6fa95-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

## <a name="how-to-enable-logging-for-a-web-service"></a><span data-ttu-id="6fa95-107">How to enable logging for a Web service</span><span class="sxs-lookup"><span data-stu-id="6fa95-107">How to enable logging for a Web service</span></span>

<span data-ttu-id="6fa95-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="6fa95-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="6fa95-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="6fa95-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="6fa95-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="6fa95-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![New Web Services Experience link](./media/web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="6fa95-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span><span class="sxs-lookup"><span data-stu-id="6fa95-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Select New or Classic web services](./media/web-services-logging/select-web-service.png)

3. <span data-ttu-id="6fa95-114">For a New web service, click the web service name.</span><span class="sxs-lookup"><span data-stu-id="6fa95-114">For a New web service, click the web service name.</span></span> <span data-ttu-id="6fa95-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span><span class="sxs-lookup"><span data-stu-id="6fa95-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span></span>

4. <span data-ttu-id="6fa95-116">On the top menu bar, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="6fa95-116">On the top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="6fa95-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span><span class="sxs-lookup"><span data-stu-id="6fa95-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span></span>

   ![Select logging level](./media/web-services-logging/enable-logging.png)

6. <span data-ttu-id="6fa95-119">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6fa95-119">Click **Save**.</span></span>

7. <span data-ttu-id="6fa95-120">For Classic web services, create the **ml-diagnostics** container.</span><span class="sxs-lookup"><span data-stu-id="6fa95-120">For Classic web services, create the **ml-diagnostics** container.</span></span>

   <span data-ttu-id="6fa95-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span><span class="sxs-lookup"><span data-stu-id="6fa95-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span></span> <span data-ttu-id="6fa95-122">For New web services, this container is created the first time you access the web service.</span><span class="sxs-lookup"><span data-stu-id="6fa95-122">For New web services, this container is created the first time you access the web service.</span></span> <span data-ttu-id="6fa95-123">For Classic web services, you need to create the container if it doesn't already exist.</span><span class="sxs-lookup"><span data-stu-id="6fa95-123">For Classic web services, you need to create the container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="6fa95-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span><span class="sxs-lookup"><span data-stu-id="6fa95-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span></span>

   2. <span data-ttu-id="6fa95-125">Under **Blob Service**, click **Containers**.</span><span class="sxs-lookup"><span data-stu-id="6fa95-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="6fa95-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span><span class="sxs-lookup"><span data-stu-id="6fa95-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span></span> <span data-ttu-id="6fa95-127">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fa95-127">Click **OK**.</span></span>

      ![Select logging level](./media/web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="6fa95-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span><span class="sxs-lookup"><span data-stu-id="6fa95-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span></span> <span data-ttu-id="6fa95-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span><span class="sxs-lookup"><span data-stu-id="6fa95-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span></span> <span data-ttu-id="6fa95-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span><span class="sxs-lookup"><span data-stu-id="6fa95-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span></span>


## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="6fa95-132">The effects of enabling logging</span><span class="sxs-lookup"><span data-stu-id="6fa95-132">The effects of enabling logging</span></span>
<span data-ttu-id="6fa95-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span><span class="sxs-lookup"><span data-stu-id="6fa95-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="6fa95-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span><span class="sxs-lookup"><span data-stu-id="6fa95-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span></span>

<span data-ttu-id="6fa95-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span><span class="sxs-lookup"><span data-stu-id="6fa95-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span></span> <span data-ttu-id="6fa95-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="6fa95-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="6fa95-137">Log blob detail information</span><span class="sxs-lookup"><span data-stu-id="6fa95-137">Log blob detail information</span></span>
<span data-ttu-id="6fa95-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span><span class="sxs-lookup"><span data-stu-id="6fa95-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span></span>

* <span data-ttu-id="6fa95-139">An execution of the Batch-Execution method</span><span class="sxs-lookup"><span data-stu-id="6fa95-139">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="6fa95-140">An execution of the Request-Response method</span><span class="sxs-lookup"><span data-stu-id="6fa95-140">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="6fa95-141">Initialization of a Request-Response container</span><span class="sxs-lookup"><span data-stu-id="6fa95-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="6fa95-142">The name of each blob has a prefix of the following form:</span><span class="sxs-lookup"><span data-stu-id="6fa95-142">The name of each blob has a prefix of the following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="6fa95-143">Where _Log type_ is one of the following values:</span><span class="sxs-lookup"><span data-stu-id="6fa95-143">Where _Log type_ is one of the following values:</span></span>  

* <span data-ttu-id="6fa95-144">batch</span><span class="sxs-lookup"><span data-stu-id="6fa95-144">batch</span></span>  
* <span data-ttu-id="6fa95-145">score/requests</span><span class="sxs-lookup"><span data-stu-id="6fa95-145">score/requests</span></span>  
* <span data-ttu-id="6fa95-146">score/init</span><span class="sxs-lookup"><span data-stu-id="6fa95-146">score/init</span></span>  

