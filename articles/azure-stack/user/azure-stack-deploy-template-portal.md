---
title: Deploy templates using the portal in Azure Stack | Microsoft Docs
description: Learn how to use the Azure Stack portal to deploy templates.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: eafa60f2-16c9-4ef1-b724-47709e9ea29e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: ''
ms.openlocfilehash: 931c3d8beb9f2ed12228c74f09f84bbdee1798b8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870107"
---
# <a name="deploy-templates-using-the-azure-stack-portal"></a><span data-ttu-id="3ad24-103">Deploy templates using the Azure Stack portal</span><span class="sxs-lookup"><span data-stu-id="3ad24-103">Deploy templates using the Azure Stack portal</span></span>

<span data-ttu-id="3ad24-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="3ad24-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="3ad24-105">You can use the portal to deploy Azure Resource Manager templates to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3ad24-105">You can use the portal to deploy Azure Resource Manager templates to Azure Stack.</span></span>

## <a name="to-deploy-a-template"></a><span data-ttu-id="3ad24-106">To deploy a template</span><span class="sxs-lookup"><span data-stu-id="3ad24-106">To deploy a template</span></span>

1. <span data-ttu-id="3ad24-107">Sign in to the portal, select **New**, and then select **Custom**.</span><span class="sxs-lookup"><span data-stu-id="3ad24-107">Sign in to the portal, select **New**, and then select **Custom**.</span></span>
2. <span data-ttu-id="3ad24-108">Select **Template deployment**.</span><span class="sxs-lookup"><span data-stu-id="3ad24-108">Select **Template deployment**.</span></span>
3. <span data-ttu-id="3ad24-109">Select **Edit template**, and then paste your JSON template code into the code window.</span><span class="sxs-lookup"><span data-stu-id="3ad24-109">Select **Edit template**, and then paste your JSON template code into the code window.</span></span> <span data-ttu-id="3ad24-110">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="3ad24-110">Select **Save**.</span></span>
4. <span data-ttu-id="3ad24-111">Select **Edit parameters**, provide values for the parameters that are shown, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ad24-111">Select **Edit parameters**, provide values for the parameters that are shown, and then select **OK**.</span></span>
5. <span data-ttu-id="3ad24-112">Select **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="3ad24-112">Select **Subscription**.</span></span> <span data-ttu-id="3ad24-113">Choose the subscription you want to use, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ad24-113">Choose the subscription you want to use, and then select **OK**.</span></span>
6. <span data-ttu-id="3ad24-114">Select **Resource group**.</span><span class="sxs-lookup"><span data-stu-id="3ad24-114">Select **Resource group**.</span></span> <span data-ttu-id="3ad24-115">Choose an existing resource group or create a new one, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ad24-115">Choose an existing resource group or create a new one, and then select **OK**.</span></span>
7. <span data-ttu-id="3ad24-116">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="3ad24-116">Select **Create**.</span></span> <span data-ttu-id="3ad24-117">A new tile on the dashboard tracks the progress of your template deployment.</span><span class="sxs-lookup"><span data-stu-id="3ad24-117">A new tile on the dashboard tracks the progress of your template deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ad24-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ad24-118">Next steps</span></span>

* [<span data-ttu-id="3ad24-119">Deploy templates with PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ad24-119">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
