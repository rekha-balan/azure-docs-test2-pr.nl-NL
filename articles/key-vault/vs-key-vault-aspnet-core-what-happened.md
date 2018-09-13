---
title: Changes made to an ASP.NET Core project when you connec to Azure Key Vault | Microsoft Docs
description: Describes what happens to your ASP.NET Core project when you connect toKey Vault by using Visual Studio connected services.
services: key-vault
author: ghogen
manager: douge
tags: azure-resource-manager
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 04/15/2018
ms.author: ghogen
ms.openlocfilehash: b7cbe55fa3a524965e0ebc16c5ff350a60d6e440
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867125"
---
# <a name="what-happened-to-my-aspnet-core-project-visual-studio-key-vault-connected-service"></a><span data-ttu-id="34004-103">What happened to my ASP.NET Core project (Visual Studio Key Vault connected service)?</span><span class="sxs-lookup"><span data-stu-id="34004-103">What happened to my ASP.NET Core project (Visual Studio Key Vault connected service)?</span></span>

> [!div class="op_single_selector"]
> - [Getting Started](vs-key-vault-aspnet-core-get-started.md)
> - [What Happened](vs-key-vault-aspnet-core-what-happened.md)

<span data-ttu-id="34004-106">This article identifies the exact changes made to an ASP.NET project when adding the [Key Vault connected service using Visual Studio](vs-key-vault-add-connected-service.md).</span><span class="sxs-lookup"><span data-stu-id="34004-106">This article identifies the exact changes made to an ASP.NET project when adding the [Key Vault connected service using Visual Studio](vs-key-vault-add-connected-service.md).</span></span>

<span data-ttu-id="34004-107">For information on working with the connected service, see [Getting Started](vs-key-vault-aspnet-core-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="34004-107">For information on working with the connected service, see [Getting Started](vs-key-vault-aspnet-core-get-started.md).</span></span>

## <a name="added-references"></a><span data-ttu-id="34004-108">Added references</span><span class="sxs-lookup"><span data-stu-id="34004-108">Added references</span></span>

<span data-ttu-id="34004-109">Affects the project file \*.NET references and NuGet package references.</span><span class="sxs-lookup"><span data-stu-id="34004-109">Affects the project file \*.NET references and NuGet package references.</span></span>

| <span data-ttu-id="34004-110">Type</span><span class="sxs-lookup"><span data-stu-id="34004-110">Type</span></span> | <span data-ttu-id="34004-111">Reference</span><span class="sxs-lookup"><span data-stu-id="34004-111">Reference</span></span> |
| --- | --- |
| <span data-ttu-id="34004-112">NuGet</span><span class="sxs-lookup"><span data-stu-id="34004-112">NuGet</span></span> | <span data-ttu-id="34004-113">Microsoft.AspNetCore.AzureKeyVault.HostingStartup</span><span class="sxs-lookup"><span data-stu-id="34004-113">Microsoft.AspNetCore.AzureKeyVault.HostingStartup</span></span> |

## <a name="added-files"></a><span data-ttu-id="34004-114">Added files</span><span class="sxs-lookup"><span data-stu-id="34004-114">Added files</span></span>

- <span data-ttu-id="34004-115">ConnectedService.json added, which records some information about the Connected Service provider, version, and a link the documentation.</span><span class="sxs-lookup"><span data-stu-id="34004-115">ConnectedService.json added, which records some information about the Connected Service provider, version, and a link the documentation.</span></span>

## <a name="project-file-changes"></a><span data-ttu-id="34004-116">Project file changes</span><span class="sxs-lookup"><span data-stu-id="34004-116">Project file changes</span></span>

- <span data-ttu-id="34004-117">Added the Connected Services ItemGroup and ConnectedServices.json file.</span><span class="sxs-lookup"><span data-stu-id="34004-117">Added the Connected Services ItemGroup and ConnectedServices.json file.</span></span>

## <a name="launchsettingsjson-changes"></a><span data-ttu-id="34004-118">launchsettings.json changes</span><span class="sxs-lookup"><span data-stu-id="34004-118">launchsettings.json changes</span></span>

- <span data-ttu-id="34004-119">Added the following environment variable entries to both the IIS Express profile and the profile that matches your web project name:</span><span class="sxs-lookup"><span data-stu-id="34004-119">Added the following environment variable entries to both the IIS Express profile and the profile that matches your web project name:</span></span>

    ```json
      "environmentVariables": {
        "ASPNETCORE_HOSTINGSTARTUP__KEYVAULT__CONFIGURATIONENABLED": "true",
        "ASPNETCORE_HOSTINGSTARTUP__KEYVAULT__CONFIGURATIONVAULT": "<your keyvault URL>"
      }
    ```

## <a name="changes-on-azure"></a><span data-ttu-id="34004-120">Changes on Azure</span><span class="sxs-lookup"><span data-stu-id="34004-120">Changes on Azure</span></span>

- <span data-ttu-id="34004-121">Created a resource group (or used an existing one).</span><span class="sxs-lookup"><span data-stu-id="34004-121">Created a resource group (or used an existing one).</span></span>
- <span data-ttu-id="34004-122">Created a Key Vault in the specified resource group.</span><span class="sxs-lookup"><span data-stu-id="34004-122">Created a Key Vault in the specified resource group.</span></span>

