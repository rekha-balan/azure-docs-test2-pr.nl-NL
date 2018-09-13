---
title: Deploy templates with Visual Studio in Azure Stack | Microsoft Docs
description: Learn how to deploy templates with Visual Studio in Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.custom: vs-azure
ms.workload: azure-vs
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: ''
ms.openlocfilehash: 585f890b11ab71f9c10479ff65aff74922a30ed1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871471"
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a><span data-ttu-id="6b6b2-103">Deploy templates in Azure Stack using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b6b2-103">Deploy templates in Azure Stack using Visual Studio</span></span>

<span data-ttu-id="6b6b2-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="6b6b2-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="6b6b2-105">You can use Visual Studio to deploy Azure Resource Manager templates to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-105">You can use Visual Studio to deploy Azure Resource Manager templates to Azure Stack.</span></span>

## <a name="to-deploy-a-template"></a><span data-ttu-id="6b6b2-106">To deploy a template</span><span class="sxs-lookup"><span data-stu-id="6b6b2-106">To deploy a template</span></span>

1. <span data-ttu-id="6b6b2-107">[Install and connect](azure-stack-install-visual-studio.md) to Azure Stack with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-107">[Install and connect](azure-stack-install-visual-studio.md) to Azure Stack with Visual Studio.</span></span>
2. <span data-ttu-id="6b6b2-108">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-108">Open Visual Studio.</span></span>
3. <span data-ttu-id="6b6b2-109">Select **File**, and then select **New**.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-109">Select **File**, and then select **New**.</span></span> <span data-ttu-id="6b6b2-110">In **New Project**, select **Azure Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-110">In **New Project**, select **Azure Resource Group**.</span></span>
4. <span data-ttu-id="6b6b2-111">Enter a **Name** for the new project, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-111">Enter a **Name** for the new project, and then select **OK**.</span></span>
5. <span data-ttu-id="6b6b2-112">In **Select Azure Template**, pick **Azure Stack Quickstart** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-112">In **Select Azure Template**, pick **Azure Stack Quickstart** from the drop-down list.</span></span>
6. <span data-ttu-id="6b6b2-113">Select **101-create-storage-account**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-113">Select **101-create-storage-account**, and then select **OK**.</span></span>
7. <span data-ttu-id="6b6b2-114">In your new project, expand the **Templates** node in **Solution Explorer** to see the available templates.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-114">In your new project, expand the **Templates** node in **Solution Explorer** to see the available templates.</span></span>
8. <span data-ttu-id="6b6b2-115">In **Solution Explorer**, pick the name of your project, and then select **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-115">In **Solution Explorer**, pick the name of your project, and then select **Deploy**.</span></span> <span data-ttu-id="6b6b2-116">Select **New Deployment**.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-116">Select **New Deployment**.</span></span>
9. <span data-ttu-id="6b6b2-117">In **Deploy to Resource Group**, use the **Subscription** drop-down list to select your Microsoft Azure Stack subscription.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-117">In **Deploy to Resource Group**, use the **Subscription** drop-down list to select your Microsoft Azure Stack subscription.</span></span>
10. <span data-ttu-id="6b6b2-118">From the **Resource Group** list, choose an existing resource group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-118">From the **Resource Group** list, choose an existing resource group or create a new one.</span></span>
11. <span data-ttu-id="6b6b2-119">From the **Resource group location** list, choose a location, and then select **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-119">From the **Resource group location** list, choose a location, and then select **Deploy**.</span></span>
12. <span data-ttu-id="6b6b2-120">In **Edit Parameters**, provide values for the parameters (which vary by template), and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="6b6b2-120">In **Edit Parameters**, provide values for the parameters (which vary by template), and then select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b6b2-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b6b2-121">Next steps</span></span>

* [<span data-ttu-id="6b6b2-122">Deploy templates with the command line</span><span class="sxs-lookup"><span data-stu-id="6b6b2-122">Deploy templates with the command line</span></span>](azure-stack-deploy-template-command-line.md)
* [<span data-ttu-id="6b6b2-123">Develop templates for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6b6b2-123">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
