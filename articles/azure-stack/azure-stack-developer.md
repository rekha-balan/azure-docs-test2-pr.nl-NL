---
title: Develop apps for Azure Stack | Microsoft Docs
description: Learn development considerations for prototyping Azure Stack apps
services: azure-stack
documentationcenter: ''
author: HeathL17
manager: byronr
editor: ''
ms.assetid: d3ebc6b1-0ffe-4d3e-ba4a-388239d6cdc3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/1/2017
ms.author: helaw
ms.openlocfilehash: 08c1285ae0886e2777b355f82aac7d26e460a08a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551660"
---
# <a name="develop-for-azure-stack"></a><span data-ttu-id="5ed3a-103">Develop for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5ed3a-103">Develop for Azure Stack</span></span>
<span data-ttu-id="5ed3a-104">You can get started developing applications today, even if you don't have access to an Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="5ed3a-104">You can get started developing applications today, even if you don't have access to an Azure Stack environment.</span></span> <span data-ttu-id="5ed3a-105">Because Azure Stack delivers Microsoft Azure services that run in your datacenter, you can use similar tools and processes to develop against Azure Stack as you would with Azure.</span><span class="sxs-lookup"><span data-stu-id="5ed3a-105">Because Azure Stack delivers Microsoft Azure services that run in your datacenter, you can use similar tools and processes to develop against Azure Stack as you would with Azure.</span></span>  <span data-ttu-id="5ed3a-106">With a bit of preparation and guidance from the following topics, you can use Azure to emulate an Azure Stack environment:</span><span class="sxs-lookup"><span data-stu-id="5ed3a-106">With a bit of preparation and guidance from the following topics, you can use Azure to emulate an Azure Stack environment:</span></span>

* <span data-ttu-id="5ed3a-107">In Azure, you can create Azure Resource Manager templates that are also deployable to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5ed3a-107">In Azure, you can create Azure Resource Manager templates that are also deployable to Azure Stack.</span></span>  <span data-ttu-id="5ed3a-108">See [template considerations](azure-stack-develop-templates.md) for guidance on developing your templates to ensure portability.</span><span class="sxs-lookup"><span data-stu-id="5ed3a-108">See [template considerations](azure-stack-develop-templates.md) for guidance on developing your templates to ensure portability.</span></span>
* <span data-ttu-id="5ed3a-109">There is a delta in service availability and service versioning between Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5ed3a-109">There is a delta in service availability and service versioning between Azure and Azure Stack.</span></span> <span data-ttu-id="5ed3a-110">You can use the [Azure Stack policy module](azure-stack-policy-module.md) to restrict Azure service availability and resource types to what's available in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5ed3a-110">You can use the [Azure Stack policy module](azure-stack-policy-module.md) to restrict Azure service availability and resource types to what's available in Azure Stack.</span></span> <span data-ttu-id="5ed3a-111">Constraining available services will help your application rely on services available to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5ed3a-111">Constraining available services will help your application rely on services available to Azure Stack.</span></span>
* <span data-ttu-id="5ed3a-112">The [Azure Stack Quickstart Templates](https://github.com/Azure/AzureStack-QuickStart-Templates) are common scenario examples of how to develop your templates so they can be deployed to both Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5ed3a-112">The [Azure Stack Quickstart Templates](https://github.com/Azure/AzureStack-QuickStart-Templates) are common scenario examples of how to develop your templates so they can be deployed to both Azure and Azure Stack.</span></span>

