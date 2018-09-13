---
title: Azure resource provider registration errors | Microsoft Docs
description: Describes how to resolve Azure resource provider registration errors.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 03/09/2018
ms.author: tomfitz
ms.openlocfilehash: b90009c1cd08a1004e58c4b9f25cd6350712fbcd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856993"
---
# <a name="resolve-errors-for-resource-provider-registration"></a><span data-ttu-id="ae658-103">Resolve errors for resource provider registration</span><span class="sxs-lookup"><span data-stu-id="ae658-103">Resolve errors for resource provider registration</span></span>

<span data-ttu-id="ae658-104">This article describes the errors you may encounter when using a resource provider that you have not previously used in your subscription.</span><span class="sxs-lookup"><span data-stu-id="ae658-104">This article describes the errors you may encounter when using a resource provider that you have not previously used in your subscription.</span></span>

## <a name="symptom"></a><span data-ttu-id="ae658-105">Symptom</span><span class="sxs-lookup"><span data-stu-id="ae658-105">Symptom</span></span>

<span data-ttu-id="ae658-106">When deploying resource, you may receive the following error code and message:</span><span class="sxs-lookup"><span data-stu-id="ae658-106">When deploying resource, you may receive the following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="ae658-107">Or, you may receive a similar message that states:</span><span class="sxs-lookup"><span data-stu-id="ae658-107">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

<span data-ttu-id="ae658-108">The error message should give you suggestions for the supported locations and API versions.</span><span class="sxs-lookup"><span data-stu-id="ae658-108">The error message should give you suggestions for the supported locations and API versions.</span></span> <span data-ttu-id="ae658-109">You can change your template to one of the suggested values.</span><span class="sxs-lookup"><span data-stu-id="ae658-109">You can change your template to one of the suggested values.</span></span> <span data-ttu-id="ae658-110">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span><span class="sxs-lookup"><span data-stu-id="ae658-110">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span></span> <span data-ttu-id="ae658-111">If you have not used a particular resource provider before, you may need to register that provider.</span><span class="sxs-lookup"><span data-stu-id="ae658-111">If you have not used a particular resource provider before, you may need to register that provider.</span></span>

## <a name="cause"></a><span data-ttu-id="ae658-112">Cause</span><span class="sxs-lookup"><span data-stu-id="ae658-112">Cause</span></span>

<span data-ttu-id="ae658-113">You receive these errors for one of three reasons:</span><span class="sxs-lookup"><span data-stu-id="ae658-113">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="ae658-114">The resource provider has not been registered for your subscription</span><span class="sxs-lookup"><span data-stu-id="ae658-114">The resource provider has not been registered for your subscription</span></span>
1. <span data-ttu-id="ae658-115">API version not supported for the resource type</span><span class="sxs-lookup"><span data-stu-id="ae658-115">API version not supported for the resource type</span></span>
1. <span data-ttu-id="ae658-116">Location not supported for the resource type</span><span class="sxs-lookup"><span data-stu-id="ae658-116">Location not supported for the resource type</span></span>

## <a name="solution-1---powershell"></a><span data-ttu-id="ae658-117">Solution 1 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae658-117">Solution 1 - PowerShell</span></span>

<span data-ttu-id="ae658-118">For PowerShell, use **Get-AzureRmResourceProvider** to see your registration status.</span><span class="sxs-lookup"><span data-stu-id="ae658-118">For PowerShell, use **Get-AzureRmResourceProvider** to see your registration status.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="ae658-119">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span><span class="sxs-lookup"><span data-stu-id="ae658-119">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="ae658-120">To get the supported locations for a particular type of resource, use:</span><span class="sxs-lookup"><span data-stu-id="ae658-120">To get the supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="ae658-121">To get the supported API versions for a particular type of resource, use:</span><span class="sxs-lookup"><span data-stu-id="ae658-121">To get the supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

## <a name="solution-2---azure-cli"></a><span data-ttu-id="ae658-122">Solution 2 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ae658-122">Solution 2 - Azure CLI</span></span>

<span data-ttu-id="ae658-123">To see whether the provider is registered, use the `az provider list` command.</span><span class="sxs-lookup"><span data-stu-id="ae658-123">To see whether the provider is registered, use the `az provider list` command.</span></span>

```azurecli-interactive
az provider list
```

<span data-ttu-id="ae658-124">To register a resource provider, use the `az provider register` command, and specify the *namespace* to register.</span><span class="sxs-lookup"><span data-stu-id="ae658-124">To register a resource provider, use the `az provider register` command, and specify the *namespace* to register.</span></span>

```azurecli-interactive
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="ae658-125">To see the supported locations and API versions for a resource type, use:</span><span class="sxs-lookup"><span data-stu-id="ae658-125">To see the supported locations and API versions for a resource type, use:</span></span>

```azurecli-interactive
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="solution-3---azure-portal"></a><span data-ttu-id="ae658-126">Solution 3 - Azure portal</span><span class="sxs-lookup"><span data-stu-id="ae658-126">Solution 3 - Azure portal</span></span>

<span data-ttu-id="ae658-127">You can see the registration status and register a resource provider namespace through the portal.</span><span class="sxs-lookup"><span data-stu-id="ae658-127">You can see the registration status and register a resource provider namespace through the portal.</span></span>

1. <span data-ttu-id="ae658-128">For your subscription, select **Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="ae658-128">For your subscription, select **Resource providers**.</span></span>

   ![select resource providers](./media/resource-manager-register-provider-errors/select-resource-provider.png)

1. <span data-ttu-id="ae658-130">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span><span class="sxs-lookup"><span data-stu-id="ae658-130">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span></span>

   ![list resource providers](./media/resource-manager-register-provider-errors/list-resource-providers.png)
