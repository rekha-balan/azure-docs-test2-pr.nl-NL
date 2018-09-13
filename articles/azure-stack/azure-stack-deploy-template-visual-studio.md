---
title: Deploy templates with Visual Studio in Azure Stack | Microsoft Docs
description: Learn how to deploy templates with Visual Studio in Azure Stack.
services: azure-stack
documentationcenter: ''
author: HeathL17
manager: byronr
editor: ''
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/13/2017
ms.author: helaw
ms.openlocfilehash: 225f73442480849662c8c0b535230d18781e19dc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552566"
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a><span data-ttu-id="d71e1-103">Deploy templates in Azure Stack using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d71e1-103">Deploy templates in Azure Stack using Visual Studio</span></span>

<span data-ttu-id="d71e1-104">Use Visual Studio to deploy Azure Resource Manager templates to the Azure Stack POC.</span><span class="sxs-lookup"><span data-stu-id="d71e1-104">Use Visual Studio to deploy Azure Resource Manager templates to the Azure Stack POC.</span></span>

1. <span data-ttu-id="d71e1-105">[Install and connect](azure-stack-install-visual-studio.md) to Azure Stack with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d71e1-105">[Install and connect](azure-stack-install-visual-studio.md) to Azure Stack with Visual Studio.</span></span>
2. <span data-ttu-id="d71e1-106">Open Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d71e1-106">Open Visual Studio 2015.</span></span>
3. <span data-ttu-id="d71e1-107">Click **File**, click **New**, and in the **New Project** dialog box click **Azure Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="d71e1-107">Click **File**, click **New**, and in the **New Project** dialog box click **Azure Resource Group**.</span></span>
4. <span data-ttu-id="d71e1-108">Enter a **Name** for the new project, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d71e1-108">Enter a **Name** for the new project, and then click **OK**.</span></span>
5. <span data-ttu-id="d71e1-109">In the **Select Azure Template** dialog box, change the *Show templates from this location* drop-down to **Azure Stack Quickstart**</span><span class="sxs-lookup"><span data-stu-id="d71e1-109">In the **Select Azure Template** dialog box, change the *Show templates from this location* drop-down to **Azure Stack Quickstart**</span></span>
6. <span data-ttu-id="d71e1-110">Click **101-create-storage-account**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d71e1-110">Click **101-create-storage-account**, and then click **OK**.</span></span>  
7. <span data-ttu-id="d71e1-111">In your new project, you can see a list of the templates available by expanding the **Templates** node in the **Solution Explorer** pane.</span><span class="sxs-lookup"><span data-stu-id="d71e1-111">In your new project, you can see a list of the templates available by expanding the **Templates** node in the **Solution Explorer** pane.</span></span>
8. <span data-ttu-id="d71e1-112">In the **Solution Explorer** pane, right-click the name of your project, click **Deploy**, then click **New Deployment**.</span><span class="sxs-lookup"><span data-stu-id="d71e1-112">In the **Solution Explorer** pane, right-click the name of your project, click **Deploy**, then click **New Deployment**.</span></span>
9. <span data-ttu-id="d71e1-113">In the **Deploy to Resource Group** dialog box, in the **Subscription** drop-down, select your Microsoft Azure Stack subscription.</span><span class="sxs-lookup"><span data-stu-id="d71e1-113">In the **Deploy to Resource Group** dialog box, in the **Subscription** drop-down, select your Microsoft Azure Stack subscription.</span></span>
10. <span data-ttu-id="d71e1-114">In the **Resource Group** list, choose an existing resource group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="d71e1-114">In the **Resource Group** list, choose an existing resource group or create a new one.</span></span>
11. <span data-ttu-id="d71e1-115">In the **Resource group location** list, choose a location, and then click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="d71e1-115">In the **Resource group location** list, choose a location, and then click **Deploy**.</span></span>
12. <span data-ttu-id="d71e1-116">In the **Edit Parameters** dialog box, enter values for the parameters (which vary by template), and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d71e1-116">In the **Edit Parameters** dialog box, enter values for the parameters (which vary by template), and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d71e1-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="d71e1-117">Next steps</span></span>
[<span data-ttu-id="d71e1-118">Deploy templates with the command line</span><span class="sxs-lookup"><span data-stu-id="d71e1-118">Deploy templates with the command line</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="d71e1-119">Develop templates for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d71e1-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)

