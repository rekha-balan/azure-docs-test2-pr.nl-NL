---
title: Develop apps for Azure Stack | Microsoft Docs
description: Development considerations for prototyping applications on Azure Stack
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: d3ebc6b1-0ffe-4d3e-ba4a-388239d6cdc3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: ''
ms.openlocfilehash: a6f89f9a7e5960e4749c14fc9a4adb648f6781f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855981"
---
# <a name="develop-for-azure-stack"></a><span data-ttu-id="ddc9e-103">Develop for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ddc9e-103">Develop for Azure Stack</span></span>

<span data-ttu-id="ddc9e-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="ddc9e-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="ddc9e-105">You can get started developing applications today, even if you don't have access to an Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="ddc9e-105">You can get started developing applications today, even if you don't have access to an Azure Stack environment.</span></span> <span data-ttu-id="ddc9e-106">Because Azure Stack delivers Microsoft Azure services that run in your datacenter, you can use similar tools and processes to develop against Azure Stack as you would with Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc9e-106">Because Azure Stack delivers Microsoft Azure services that run in your datacenter, you can use similar tools and processes to develop against Azure Stack as you would with Azure.</span></span> <span data-ttu-id="ddc9e-107">With some preparation, and using the guidance in the following topics, you can use Azure to emulate an Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="ddc9e-107">With some preparation, and using the guidance in the following topics, you can use Azure to emulate an Azure Stack environment.</span></span>

* <span data-ttu-id="ddc9e-108">In Azure, you can create Azure Resource Manager templates that are deployable to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ddc9e-108">In Azure, you can create Azure Resource Manager templates that are deployable to Azure Stack.</span></span> <span data-ttu-id="ddc9e-109">See [template considerations](azure-stack-develop-templates.md) for guidance on developing templates to ensure portability.</span><span class="sxs-lookup"><span data-stu-id="ddc9e-109">See [template considerations](azure-stack-develop-templates.md) for guidance on developing templates to ensure portability.</span></span>
* <span data-ttu-id="ddc9e-110">There are differences in service availability and service versioning between Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ddc9e-110">There are differences in service availability and service versioning between Azure and Azure Stack.</span></span> <span data-ttu-id="ddc9e-111">You can use the [Azure Stack policy module](azure-stack-policy-module.md) to restrict Azure service availability and resource types to what's available in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ddc9e-111">You can use the [Azure Stack policy module](azure-stack-policy-module.md) to restrict Azure service availability and resource types to what's available in Azure Stack.</span></span> <span data-ttu-id="ddc9e-112">Constraining services ensures that your applications rely on services available to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ddc9e-112">Constraining services ensures that your applications rely on services available to Azure Stack.</span></span>
* <span data-ttu-id="ddc9e-113">The [Azure Stack Quickstart Templates](https://github.com/Azure/AzureStack-QuickStart-Templates) are common scenario examples that show how to develop templates that can be deployed to Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ddc9e-113">The [Azure Stack Quickstart Templates](https://github.com/Azure/AzureStack-QuickStart-Templates) are common scenario examples that show how to develop templates that can be deployed to Azure and Azure Stack.</span></span>
