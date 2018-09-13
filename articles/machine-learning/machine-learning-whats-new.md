---
title: What's new in Azure Machine Learning | Microsoft Docs
description: New features that are available in Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondl
editor: ''
ms.assetid: ddc716ed-2615-4806-bf27-6c9a5662a7f2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 551b977b90612ddbfa1514a9c2358ebf8179c385
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556015"
---
# <a name="whats-new-in-azure-machine-learning"></a><span data-ttu-id="d70ac-103">What's New in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d70ac-103">What's New in Azure Machine Learning</span></span>

### <a name="the-march-2017-release-of-microsoft-azure-machine-learning-updates-provides-the-following-feature"></a><span data-ttu-id="d70ac-104">The March 2017 release of Microsoft Azure Machine Learning updates provides the following feature:</span><span class="sxs-lookup"><span data-stu-id="d70ac-104">The March 2017 release of Microsoft Azure Machine Learning updates provides the following feature:</span></span>



* <span data-ttu-id="d70ac-105">Dedicated Capacity for Azure Machine Learning BES Jobs</span><span class="sxs-lookup"><span data-stu-id="d70ac-105">Dedicated Capacity for Azure Machine Learning BES Jobs</span></span>

    <span data-ttu-id="d70ac-106">Machine Learning Batch Pool processing uses the [Azure Batch](../batch/batch-technical-overview.md) service to provide customer-managed scale for the Azure Machine Learning Batch Execution Service.</span><span class="sxs-lookup"><span data-stu-id="d70ac-106">Machine Learning Batch Pool processing uses the [Azure Batch](../batch/batch-technical-overview.md) service to provide customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="d70ac-107">Batch Pool processing allows you to create Azure Batch pools on which you can submit batch jobs and have them execute in a predictable manner.</span><span class="sxs-lookup"><span data-stu-id="d70ac-107">Batch Pool processing allows you to create Azure Batch pools on which you can submit batch jobs and have them execute in a predictable manner.</span></span>

    <span data-ttu-id="d70ac-108">For more information, see [Azure Batch service for Machine Learning jobs](machine-learning-dedicated-capacity-for-bes-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="d70ac-108">For more information, see [Azure Batch service for Machine Learning jobs](machine-learning-dedicated-capacity-for-bes-jobs.md).</span></span>


### <a name="the-august-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="d70ac-109">The August 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span><span class="sxs-lookup"><span data-stu-id="d70ac-109">The August 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="d70ac-110">Classic Web services can now be managed in the new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span><span class="sxs-lookup"><span data-stu-id="d70ac-110">Classic Web services can now be managed in the new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>    
  * <span data-ttu-id="d70ac-111">Which provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="d70ac-111">Which provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
  * <span data-ttu-id="d70ac-112">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span><span class="sxs-lookup"><span data-stu-id="d70ac-112">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
  * <span data-ttu-id="d70ac-113">Provides a new Batch Execution Service test page with sample data and job submission history.</span><span class="sxs-lookup"><span data-stu-id="d70ac-113">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>
  * <span data-ttu-id="d70ac-114">Provides easier endpoint management.</span><span class="sxs-lookup"><span data-stu-id="d70ac-114">Provides easier endpoint management.</span></span>

### <a name="the-july-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="d70ac-115">The July 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span><span class="sxs-lookup"><span data-stu-id="d70ac-115">The July 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="d70ac-116">Web services are now managed as Azure resources managed through [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) interfaces, allowing for the following enhancements:</span><span class="sxs-lookup"><span data-stu-id="d70ac-116">Web services are now managed as Azure resources managed through [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) interfaces, allowing for the following enhancements:</span></span>
  * <span data-ttu-id="d70ac-117">There are new [REST APIs](https://msdn.microsoft.com/library/azure/Dn950030.aspx) to deploy and manage your Resource Manager based Web services.</span><span class="sxs-lookup"><span data-stu-id="d70ac-117">There are new [REST APIs](https://msdn.microsoft.com/library/azure/Dn950030.aspx) to deploy and manage your Resource Manager based Web services.</span></span>
  * <span data-ttu-id="d70ac-118">There is a new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span><span class="sxs-lookup"><span data-stu-id="d70ac-118">There is a new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>
* <span data-ttu-id="d70ac-119">Incorporates a new subscription-based, multi-region web service deployment model using Resource Manager based APIs leveraging the Resource Manager Resource Provider for Web Services.</span><span class="sxs-lookup"><span data-stu-id="d70ac-119">Incorporates a new subscription-based, multi-region web service deployment model using Resource Manager based APIs leveraging the Resource Manager Resource Provider for Web Services.</span></span>
* <span data-ttu-id="d70ac-120">Introduces new [pricing plans](https://azure.microsoft.com/pricing/details/machine-learning/) and plan management capabilities using the new Resource Manager RP for Billing.</span><span class="sxs-lookup"><span data-stu-id="d70ac-120">Introduces new [pricing plans](https://azure.microsoft.com/pricing/details/machine-learning/) and plan management capabilities using the new Resource Manager RP for Billing.</span></span>
  * <span data-ttu-id="d70ac-121">You can now [deploy your web service to multiple regions](machine-learning-how-to-deploy-to-multiple-regions.md) without needing to create a subscription in each region.</span><span class="sxs-lookup"><span data-stu-id="d70ac-121">You can now [deploy your web service to multiple regions](machine-learning-how-to-deploy-to-multiple-regions.md) without needing to create a subscription in each region.</span></span>
* <span data-ttu-id="d70ac-122">Provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="d70ac-122">Provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
* <span data-ttu-id="d70ac-123">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span><span class="sxs-lookup"><span data-stu-id="d70ac-123">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
* <span data-ttu-id="d70ac-124">Provides a new Batch Execution Service test page with sample data and job submission history.</span><span class="sxs-lookup"><span data-stu-id="d70ac-124">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>

<span data-ttu-id="d70ac-125">In addition, the Machine Learning Studio has been updated to allow you to deploy to the new Web service model or continue to deploy to the classic Web service model.</span><span class="sxs-lookup"><span data-stu-id="d70ac-125">In addition, the Machine Learning Studio has been updated to allow you to deploy to the new Web service model or continue to deploy to the classic Web service model.</span></span> 

