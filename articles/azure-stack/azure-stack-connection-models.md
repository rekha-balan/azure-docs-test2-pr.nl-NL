---
title: Azure Stack integrated systems connection models | Microsoft Docs
description: Determine deployment planning decisions for multi-node Azure Stack.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2018
ms.author: jeffgilb
ms.reviewer: wfayed
ms.openlocfilehash: e6c94ef1172ea6380a94d5907c24069ed8c48ff5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867921"
---
# <a name="azure-stack-integrated-systems-connection-models"></a><span data-ttu-id="712a1-103">Azure Stack integrated systems connection models</span><span class="sxs-lookup"><span data-stu-id="712a1-103">Azure Stack integrated systems connection models</span></span>
<span data-ttu-id="712a1-104">If you’re interested in an Azure Stack integrated system, you’ll need to understand [several datacenter integration considerations](azure-stack-datacenter-integration.md) for Azure Stack deployment to determine how the system will fit into your datacenter.</span><span class="sxs-lookup"><span data-stu-id="712a1-104">If you’re interested in an Azure Stack integrated system, you’ll need to understand [several datacenter integration considerations](azure-stack-datacenter-integration.md) for Azure Stack deployment to determine how the system will fit into your datacenter.</span></span> <span data-ttu-id="712a1-105">In addition, you'll need to decide exactly how you will integrate Azure Stack into your hybrid cloud environment.</span><span class="sxs-lookup"><span data-stu-id="712a1-105">In addition, you'll need to decide exactly how you will integrate Azure Stack into your hybrid cloud environment.</span></span> <span data-ttu-id="712a1-106">This article provides an overview of these major decisions including Azure connection, identity store, and billing model decisions.</span><span class="sxs-lookup"><span data-stu-id="712a1-106">This article provides an overview of these major decisions including Azure connection, identity store, and billing model decisions.</span></span>

<span data-ttu-id="712a1-107">If you decide to purchase an integrated system, your original equipment manufacturer (OEM) hardware vendor helps guide you through much of the planning process in more detail.</span><span class="sxs-lookup"><span data-stu-id="712a1-107">If you decide to purchase an integrated system, your original equipment manufacturer (OEM) hardware vendor helps guide you through much of the planning process in more detail.</span></span> <span data-ttu-id="712a1-108">They will also perform the actual deployment.</span><span class="sxs-lookup"><span data-stu-id="712a1-108">They will also perform the actual deployment.</span></span>

## <a name="choose-an-azure-stack-deployment-connection-model"></a><span data-ttu-id="712a1-109">Choose an Azure Stack deployment connection model</span><span class="sxs-lookup"><span data-stu-id="712a1-109">Choose an Azure Stack deployment connection model</span></span>
<span data-ttu-id="712a1-110">You can choose to deploy Azure Stack either connected to the internet (and to Azure) or disconnected.</span><span class="sxs-lookup"><span data-stu-id="712a1-110">You can choose to deploy Azure Stack either connected to the internet (and to Azure) or disconnected.</span></span> <span data-ttu-id="712a1-111">To get the most benefit from Azure Stack, including hybrid scenarios between Azure Stack and Azure, you'd want to deploy connected to Azure.</span><span class="sxs-lookup"><span data-stu-id="712a1-111">To get the most benefit from Azure Stack, including hybrid scenarios between Azure Stack and Azure, you'd want to deploy connected to Azure.</span></span> <span data-ttu-id="712a1-112">This choice defines which options are available for your identity store (Azure Active Directory or Active Directory Federation Services) and billing model (Pay as you use-based billing or capacity-based billing) as summarized in the following diagram and table:</span><span class="sxs-lookup"><span data-stu-id="712a1-112">This choice defines which options are available for your identity store (Azure Active Directory or Active Directory Federation Services) and billing model (Pay as you use-based billing or capacity-based billing) as summarized in the following diagram and table:</span></span> 

![Azure Stack deployment and billing scenarios](media/azure-stack-connection-models/azure-stack-scenarios.png)  
  
> [!IMPORTANT]
> <span data-ttu-id="712a1-114">This is a key decision point!</span><span class="sxs-lookup"><span data-stu-id="712a1-114">This is a key decision point!</span></span> <span data-ttu-id="712a1-115">Choosing Active Directory Federation Services (AD FS) or Azure Active Directory (Azure AD) is a one-time decision that you must make at deployment time.</span><span class="sxs-lookup"><span data-stu-id="712a1-115">Choosing Active Directory Federation Services (AD FS) or Azure Active Directory (Azure AD) is a one-time decision that you must make at deployment time.</span></span> <span data-ttu-id="712a1-116">You can’t change this later without re-deploying the entire system.</span><span class="sxs-lookup"><span data-stu-id="712a1-116">You can’t change this later without re-deploying the entire system.</span></span>  


|<span data-ttu-id="712a1-117">Options</span><span class="sxs-lookup"><span data-stu-id="712a1-117">Options</span></span>|<span data-ttu-id="712a1-118">Connected to Azure</span><span class="sxs-lookup"><span data-stu-id="712a1-118">Connected to Azure</span></span>|<span data-ttu-id="712a1-119">Disconnected from Azure</span><span class="sxs-lookup"><span data-stu-id="712a1-119">Disconnected from Azure</span></span>|
|-----|-----|-----|
|<span data-ttu-id="712a1-120">Azure AD</span><span class="sxs-lookup"><span data-stu-id="712a1-120">Azure AD</span></span>|![Supported](media/azure-stack-connection-models/check.png)| |
|<span data-ttu-id="712a1-122">AD FS</span><span class="sxs-lookup"><span data-stu-id="712a1-122">AD FS</span></span>|![Supported](media/azure-stack-connection-models/check.png)|![Supported](media/azure-stack-connection-models/check.png)|
|<span data-ttu-id="712a1-125">Consumption-based billing</span><span class="sxs-lookup"><span data-stu-id="712a1-125">Consumption-based billing</span></span>|![Supported](media/azure-stack-connection-models/check.png)| |
|<span data-ttu-id="712a1-127">Capacity-based billing</span><span class="sxs-lookup"><span data-stu-id="712a1-127">Capacity-based billing</span></span>|![Supported](media/azure-stack-connection-models/check.png)|![Supported](media/azure-stack-connection-models/check.png)|
|<span data-ttu-id="712a1-130">Download update packages directly to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="712a1-130">Download update packages directly to Azure Stack</span></span>|![Supported](media/azure-stack-connection-models/check.png)|  |

<span data-ttu-id="712a1-132">After you've decided on the Azure connection model to be used for Azure Stack deployment, additional, connection-dependent decisions must be made for the identity store and billing method.</span><span class="sxs-lookup"><span data-stu-id="712a1-132">After you've decided on the Azure connection model to be used for Azure Stack deployment, additional, connection-dependent decisions must be made for the identity store and billing method.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="712a1-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="712a1-133">Next steps</span></span>

[<span data-ttu-id="712a1-134">Azure connected Azure Stack deployment decisions</span><span class="sxs-lookup"><span data-stu-id="712a1-134">Azure connected Azure Stack deployment decisions</span></span>](azure-stack-connected-deployment.md)

[<span data-ttu-id="712a1-135">Azure disconnected Azure Stack deployment decisions</span><span class="sxs-lookup"><span data-stu-id="712a1-135">Azure disconnected Azure Stack deployment decisions</span></span>](azure-stack-disconnected-deployment.md)
