---
title: Logging for Machine Learning web services | Microsoft Docs
description: Learn how to enable logging for Machine Learning web services. Logging provides additional information to help troubleshoot the APIs.
services: machine-learning
documentationcenter: ''
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 7476617233e953077a158d9780f6942036b43e09
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670418"
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="660f8-104">Enable logging for Machine Learning web services</span><span class="sxs-lookup"><span data-stu-id="660f8-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="660f8-105">This document provides information on the logging capability of Classic Web services.</span><span class="sxs-lookup"><span data-stu-id="660f8-105">This document provides information on the logging capability of Classic Web services.</span></span> <span data-ttu-id="660f8-106">Enabling logging in Web services provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span><span class="sxs-lookup"><span data-stu-id="660f8-106">Enabling logging in Web services provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

<span data-ttu-id="660f8-107">To enable logging in Web Services in the Azure classic portal:</span><span class="sxs-lookup"><span data-stu-id="660f8-107">To enable logging in Web Services in the Azure classic portal:</span></span>   

1. <span data-ttu-id="660f8-108">Sign in to [Azure classic portal](https://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="660f8-108">Sign in to [Azure classic portal](https://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="660f8-109">In the left features column, click **MACHINE LEARNING**.</span><span class="sxs-lookup"><span data-stu-id="660f8-109">In the left features column, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="660f8-110">Click your workspace, then **WEB SERVICES**.</span><span class="sxs-lookup"><span data-stu-id="660f8-110">Click your workspace, then **WEB SERVICES**.</span></span>
4. <span data-ttu-id="660f8-111">In the Web services list, click the name of the Web service.</span><span class="sxs-lookup"><span data-stu-id="660f8-111">In the Web services list, click the name of the Web service.</span></span>
5. <span data-ttu-id="660f8-112">In the endpoints list, click the endpoint name.</span><span class="sxs-lookup"><span data-stu-id="660f8-112">In the endpoints list, click the endpoint name.</span></span>
6. <span data-ttu-id="660f8-113">Click **CONFIGURE**.</span><span class="sxs-lookup"><span data-stu-id="660f8-113">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="660f8-114">Set **DIAGNOSTICS TRACE LEVEL** to *Error* or *All*, then click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="660f8-114">Set **DIAGNOSTICS TRACE LEVEL** to *Error* or *All*, then click **SAVE**.</span></span>

<span data-ttu-id="660f8-115">To enable logging in the Azure Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="660f8-115">To enable logging in the Azure Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="660f8-116">Sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="660f8-116">Sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>
2. <span data-ttu-id="660f8-117">Click Classic Web Services.</span><span class="sxs-lookup"><span data-stu-id="660f8-117">Click Classic Web Services.</span></span>
3. <span data-ttu-id="660f8-118">In the Web services list, click the name of the Web service.</span><span class="sxs-lookup"><span data-stu-id="660f8-118">In the Web services list, click the name of the Web service.</span></span>
4. <span data-ttu-id="660f8-119">In the endpoints list, click the endpoint name.</span><span class="sxs-lookup"><span data-stu-id="660f8-119">In the endpoints list, click the endpoint name.</span></span>
5. <span data-ttu-id="660f8-120">Click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="660f8-120">Click **Configure**.</span></span>
6. <span data-ttu-id="660f8-121">Set **Logging** to *Error* or *All*, then click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="660f8-121">Set **Logging** to *Error* or *All*, then click **SAVE**.</span></span>

## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="660f8-122">The effects of enabling logging</span><span class="sxs-lookup"><span data-stu-id="660f8-122">The effects of enabling logging</span></span>
<span data-ttu-id="660f8-123">When logging is enabled, all the diagnostics and errors from the selected endpoint are logged to the Azure Storage Account linked with the user’s workspace.</span><span class="sxs-lookup"><span data-stu-id="660f8-123">When logging is enabled, all the diagnostics and errors from the selected endpoint are logged to the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="660f8-124">You can see this storage account in the Azure classic portal Dashboard view (bottom of the Quick Glance section) of their workspace.</span><span class="sxs-lookup"><span data-stu-id="660f8-124">You can see this storage account in the Azure classic portal Dashboard view (bottom of the Quick Glance section) of their workspace.</span></span>  

<span data-ttu-id="660f8-125">The logs can be viewed using any of the several tools available to 'explore' an Azure Storage Account.</span><span class="sxs-lookup"><span data-stu-id="660f8-125">The logs can be viewed using any of the several tools available to 'explore' an Azure Storage Account.</span></span> <span data-ttu-id="660f8-126">The easiest may be to simply navigate to the Storage Account in the Azure classic portal and then click **CONTAINERS**.</span><span class="sxs-lookup"><span data-stu-id="660f8-126">The easiest may be to simply navigate to the Storage Account in the Azure classic portal and then click **CONTAINERS**.</span></span> <span data-ttu-id="660f8-127">You would then see a Container named **ml-diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="660f8-127">You would then see a Container named **ml-diagnostics**.</span></span> <span data-ttu-id="660f8-128">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this Storage account.</span><span class="sxs-lookup"><span data-stu-id="660f8-128">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this Storage account.</span></span> 

## <a name="log-blob-detail-information"></a><span data-ttu-id="660f8-129">Log blob detail information</span><span class="sxs-lookup"><span data-stu-id="660f8-129">Log blob detail information</span></span>
<span data-ttu-id="660f8-130">Each blob in the container holds the diagnostics info for exactly one of the following:</span><span class="sxs-lookup"><span data-stu-id="660f8-130">Each blob in the container holds the diagnostics info for exactly one of the following:</span></span>

* <span data-ttu-id="660f8-131">An execution of the Batch-Execution method</span><span class="sxs-lookup"><span data-stu-id="660f8-131">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="660f8-132">An execution of the Request-Response method</span><span class="sxs-lookup"><span data-stu-id="660f8-132">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="660f8-133">Initialization of a Request-Response container</span><span class="sxs-lookup"><span data-stu-id="660f8-133">Initialization of a Request-Response container</span></span>

<span data-ttu-id="660f8-134">The name of each blob has a prefix of the following form:</span><span class="sxs-lookup"><span data-stu-id="660f8-134">The name of each blob has a prefix of the following form:</span></span> 

<span data-ttu-id="660f8-135">{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}</span><span class="sxs-lookup"><span data-stu-id="660f8-135">{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}</span></span>  

<span data-ttu-id="660f8-136">Where Log type is one of the following values:</span><span class="sxs-lookup"><span data-stu-id="660f8-136">Where Log type is one of the following values:</span></span>  

* <span data-ttu-id="660f8-137">batch</span><span class="sxs-lookup"><span data-stu-id="660f8-137">batch</span></span>  
* <span data-ttu-id="660f8-138">score/requests</span><span class="sxs-lookup"><span data-stu-id="660f8-138">score/requests</span></span>  
* <span data-ttu-id="660f8-139">score/init</span><span class="sxs-lookup"><span data-stu-id="660f8-139">score/init</span></span>  

