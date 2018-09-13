---
title: Changes made to an ASP.NET project when you connec to Azure Key Vault | Microsoft Docs
description: Describes what happens to your ASP.NET project when you connect toKey Vault by using Visual Studio connected services.
services: key-vault
author: ghogen
manager: douge
tags: azure-resource-manager
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.topic: conceptual
ms.date: 04/15/2018
ms.author: ghogen
ms.openlocfilehash: a15f9c41c5af8803bfb230b19cbbf2f1bdbc2686
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865017"
---
# <a name="what-happened-to-my-aspnet-project-visual-studio-key-vault-connected-service"></a><span data-ttu-id="ee3b0-103">What happened to my ASP.NET project (Visual Studio Key Vault connected service)?</span><span class="sxs-lookup"><span data-stu-id="ee3b0-103">What happened to my ASP.NET project (Visual Studio Key Vault connected service)?</span></span>

> [!div class="op_single_selector"]
> - [Getting Started](vs-key-vault-aspnet-get-started.md)
> - [What Happened](vs-key-vault-aspnet-what-happened.md)

<span data-ttu-id="ee3b0-106">This article identifies the exact changes made to an ASP.NET project when adding the [Key Vault connected service using Visual Studio](vs-key-vault-add-connected-service.md).</span><span class="sxs-lookup"><span data-stu-id="ee3b0-106">This article identifies the exact changes made to an ASP.NET project when adding the [Key Vault connected service using Visual Studio](vs-key-vault-add-connected-service.md).</span></span>

<span data-ttu-id="ee3b0-107">For information on working with the connected service, see [Getting Started](vs-key-vault-aspnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ee3b0-107">For information on working with the connected service, see [Getting Started](vs-key-vault-aspnet-get-started.md).</span></span>

## <a name="added-references"></a><span data-ttu-id="ee3b0-108">Added references</span><span class="sxs-lookup"><span data-stu-id="ee3b0-108">Added references</span></span>

<span data-ttu-id="ee3b0-109">Affects the project file \*.NET references and `packages.config` (NuGet references).</span><span class="sxs-lookup"><span data-stu-id="ee3b0-109">Affects the project file \*.NET references and `packages.config` (NuGet references).</span></span>

| <span data-ttu-id="ee3b0-110">Type</span><span class="sxs-lookup"><span data-stu-id="ee3b0-110">Type</span></span> | <span data-ttu-id="ee3b0-111">Reference</span><span class="sxs-lookup"><span data-stu-id="ee3b0-111">Reference</span></span> |
| --- | --- |
| <span data-ttu-id="ee3b0-112">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="ee3b0-112">.NET; NuGet</span></span> | <span data-ttu-id="ee3b0-113">Microsoft.Azure.KeyVault</span><span class="sxs-lookup"><span data-stu-id="ee3b0-113">Microsoft.Azure.KeyVault</span></span> |
| <span data-ttu-id="ee3b0-114">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="ee3b0-114">.NET; NuGet</span></span> | <span data-ttu-id="ee3b0-115">Microsoft.Azure.KeyVault.WebKey</span><span class="sxs-lookup"><span data-stu-id="ee3b0-115">Microsoft.Azure.KeyVault.WebKey</span></span> |
| <span data-ttu-id="ee3b0-116">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="ee3b0-116">.NET; NuGet</span></span> | <span data-ttu-id="ee3b0-117">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="ee3b0-117">Microsoft.Rest.ClientRuntime</span></span> |
| <span data-ttu-id="ee3b0-118">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="ee3b0-118">.NET; NuGet</span></span> | <span data-ttu-id="ee3b0-119">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="ee3b0-119">Microsoft.Rest.ClientRuntime.Azure</span></span> |

## <a name="added-files"></a><span data-ttu-id="ee3b0-120">Added files</span><span class="sxs-lookup"><span data-stu-id="ee3b0-120">Added files</span></span>

- <span data-ttu-id="ee3b0-121">ConnectedService.json added, which records some information about the Connected Service provider, version, and a link to the documentation.</span><span class="sxs-lookup"><span data-stu-id="ee3b0-121">ConnectedService.json added, which records some information about the Connected Service provider, version, and a link to the documentation.</span></span>

## <a name="project-file-changes"></a><span data-ttu-id="ee3b0-122">Project file changes</span><span class="sxs-lookup"><span data-stu-id="ee3b0-122">Project file changes</span></span>

- <span data-ttu-id="ee3b0-123">Added the Connected Services ItemGroup and ConnectedServices.json file.</span><span class="sxs-lookup"><span data-stu-id="ee3b0-123">Added the Connected Services ItemGroup and ConnectedServices.json file.</span></span>
- <span data-ttu-id="ee3b0-124">References to the .NET assemblies described in the [Added references](#added-references) section.</span><span class="sxs-lookup"><span data-stu-id="ee3b0-124">References to the .NET assemblies described in the [Added references](#added-references) section.</span></span>

## <a name="webconfig-or-appconfig-changes"></a><span data-ttu-id="ee3b0-125">web.config or app.config changes</span><span class="sxs-lookup"><span data-stu-id="ee3b0-125">web.config or app.config changes</span></span>

- <span data-ttu-id="ee3b0-126">Added the following configuration entries:</span><span class="sxs-lookup"><span data-stu-id="ee3b0-126">Added the following configuration entries:</span></span>

    ```xml
    <configSections>
      <section
           name="configBuilders"
           type="System.Configuration.ConfigurationBuildersSection, System.Configuration, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" 
           restartOnExternalChanges="false"
           requirePermission="false" />
    </configSections>
    <configBuilders>
      <builders>
        <add 
             name="AzureKeyVault"
             vaultName="vaultname"
             type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder, Microsoft.Configuration.ConfigurationBuilders.Azure, Version=1.0.0.0, Culture=neutral" 
             vaultUri="https://vaultname.vault.azure.net" />
      </builders>
    </configBuilders>
    ```

## <a name="changes-on-azure"></a><span data-ttu-id="ee3b0-127">Changes on Azure</span><span class="sxs-lookup"><span data-stu-id="ee3b0-127">Changes on Azure</span></span>

- <span data-ttu-id="ee3b0-128">Created a resource group (or used an existing one).</span><span class="sxs-lookup"><span data-stu-id="ee3b0-128">Created a resource group (or used an existing one).</span></span>
- <span data-ttu-id="ee3b0-129">Created a Key Vault in the specified resource group.</span><span class="sxs-lookup"><span data-stu-id="ee3b0-129">Created a Key Vault in the specified resource group.</span></span>

