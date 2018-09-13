---
title: Get started with Key Vault Connected Service in Visual Studio (ASP.NET Core Projects) | Microsoft Docs
description: Use this tutorial to help you learn how to add Key Vault support to an ASP.NET or ASP.NET Core web application.
services: key-vault
author: ghogen
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 04/15/2018
ms.author: ghogen
ms.openlocfilehash: e591771ee9c9cb12d9ec2ff61ec7f5a76691c8c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869049"
---
# <a name="get-started-with-key-vault-connected-service-in-visual-studio-aspnet-core-projects"></a><span data-ttu-id="45aa8-103">Get started with Key Vault Connected Service in Visual Studio (ASP.NET Core Projects)</span><span class="sxs-lookup"><span data-stu-id="45aa8-103">Get started with Key Vault Connected Service in Visual Studio (ASP.NET Core Projects)</span></span>

> [!div class="op_single_selector"]
> - [Getting Started](vs-key-vault-aspnet-core-get-started.md)
> - [What Happened](vs-key-vault-aspnet-core-what-happened.md)

<span data-ttu-id="45aa8-106">This article provides additional guidance after you've added Key Vault to an ASP.NET Core project through the **Add Connected Services** command in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45aa8-106">This article provides additional guidance after you've added Key Vault to an ASP.NET Core project through the **Add Connected Services** command in Visual Studio.</span></span> <span data-ttu-id="45aa8-107">If you've not already added the service to your project, you can do so at any time by following the instructions in [Add Key Vault to your web application by using Visual Studio Connected Services](vs-key-vault-add-connected-service.md).</span><span class="sxs-lookup"><span data-stu-id="45aa8-107">If you've not already added the service to your project, you can do so at any time by following the instructions in [Add Key Vault to your web application by using Visual Studio Connected Services](vs-key-vault-add-connected-service.md).</span></span>

<span data-ttu-id="45aa8-108">See [What happened to my ASP.NET Core project?](vs-key-vault-aspnet-core-what-happened.md) for the changes made to your project when adding the connected service.</span><span class="sxs-lookup"><span data-stu-id="45aa8-108">See [What happened to my ASP.NET Core project?](vs-key-vault-aspnet-core-what-happened.md) for the changes made to your project when adding the connected service.</span></span>

## <a name="after-you-connect"></a><span data-ttu-id="45aa8-109">After you connect</span><span class="sxs-lookup"><span data-stu-id="45aa8-109">After you connect</span></span>

1. <span data-ttu-id="45aa8-110">Add a secret in your Key Vault in Azure.</span><span class="sxs-lookup"><span data-stu-id="45aa8-110">Add a secret in your Key Vault in Azure.</span></span> <span data-ttu-id="45aa8-111">To get to the right place in the portal, click on the link for Manage secrets stored in this Key Vault.</span><span class="sxs-lookup"><span data-stu-id="45aa8-111">To get to the right place in the portal, click on the link for Manage secrets stored in this Key Vault.</span></span> <span data-ttu-id="45aa8-112">If you closed the page or the project, you can navigate to it in the [Azure portal](https://portal.azure.com) by choosing **All Services**, under **Security**, choose **Key Vault**, then choose the Key Vault you just created.</span><span class="sxs-lookup"><span data-stu-id="45aa8-112">If you closed the page or the project, you can navigate to it in the [Azure portal](https://portal.azure.com) by choosing **All Services**, under **Security**, choose **Key Vault**, then choose the Key Vault you just created.</span></span>

   ![Navigating to the portal](media/vs-key-vault-add-connected-service/manage-secrets-link.jpg)

1. <span data-ttu-id="45aa8-114">In the Key Vault section for the key vault you created, choose **Secrets**, then **Generate/Import**.</span><span class="sxs-lookup"><span data-stu-id="45aa8-114">In the Key Vault section for the key vault you created, choose **Secrets**, then **Generate/Import**.</span></span>

   ![Generate/Import a secret](media/vs-key-vault-add-connected-service/generate-secrets.jpg)

1. <span data-ttu-id="45aa8-116">Enter a secret, such as "MySecret", and give it any string value as a test, then choose the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="45aa8-116">Enter a secret, such as "MySecret", and give it any string value as a test, then choose the **Create** button.</span></span>

   ![Create a secret](media/vs-key-vault-add-connected-service/create-a-secret.jpg)
 
1. <span data-ttu-id="45aa8-118">(optional) Enter another secret, but this time put it into a category by naming it **Secrets--MySecret**.</span><span class="sxs-lookup"><span data-stu-id="45aa8-118">(optional) Enter another secret, but this time put it into a category by naming it **Secrets--MySecret**.</span></span> <span data-ttu-id="45aa8-119">This syntax specifies a category **Secrets** that contains a secret **MySecret.**</span><span class="sxs-lookup"><span data-stu-id="45aa8-119">This syntax specifies a category **Secrets** that contains a secret **MySecret.**</span></span>
1. <span data-ttu-id="45aa8-120">In your Visual Studio project, you can now reference these secrets by using the following expressions in code:</span><span class="sxs-lookup"><span data-stu-id="45aa8-120">In your Visual Studio project, you can now reference these secrets by using the following expressions in code:</span></span>
 
   ```csharp
      config["MySecret"] // Access a secret without a section
      config["Secrets:MySecret"] // Access a secret in a section
      config.GetSection("Secrets")["MySecret"] // Get the configuration section and access a secret in it.
   ```

<span data-ttu-id="45aa8-121">Congratulations, you have now enabled your web app to use Key Vault to access securely stored secrets.</span><span class="sxs-lookup"><span data-stu-id="45aa8-121">Congratulations, you have now enabled your web app to use Key Vault to access securely stored secrets.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="45aa8-122">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="45aa8-122">Clean up resources</span></span>

<span data-ttu-id="45aa8-123">When no longer needed, delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="45aa8-123">When no longer needed, delete the resource group.</span></span> <span data-ttu-id="45aa8-124">This deletes the Key Vault and related resources.</span><span class="sxs-lookup"><span data-stu-id="45aa8-124">This deletes the Key Vault and related resources.</span></span> <span data-ttu-id="45aa8-125">To delete the resource group through the portal:</span><span class="sxs-lookup"><span data-stu-id="45aa8-125">To delete the resource group through the portal:</span></span>

1. <span data-ttu-id="45aa8-126">Enter the name of your resource group in the Search box at the top of the portal.</span><span class="sxs-lookup"><span data-stu-id="45aa8-126">Enter the name of your resource group in the Search box at the top of the portal.</span></span> <span data-ttu-id="45aa8-127">When you see the resource group used in this QuickStart in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="45aa8-127">When you see the resource group used in this QuickStart in the search results, select it.</span></span>
2. <span data-ttu-id="45aa8-128">Select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="45aa8-128">Select **Delete resource group**.</span></span>
3. <span data-ttu-id="45aa8-129">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="45aa8-129">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span></span>

# <a name="next-steps"></a><span data-ttu-id="45aa8-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="45aa8-130">Next steps</span></span>

<span data-ttu-id="45aa8-131">Learn more about developing with Key Vault in the [Key Vault Developer's Guide](key-vault-developers-guide.md)</span><span class="sxs-lookup"><span data-stu-id="45aa8-131">Learn more about developing with Key Vault in the [Key Vault Developer's Guide](key-vault-developers-guide.md)</span></span>