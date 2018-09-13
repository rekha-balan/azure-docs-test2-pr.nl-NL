---
title: Deploy a VM with securely stored password on Azure Stack | Microsoft Docs
description: Learn how to deploy a VM using a password stored in Azure Stack Key Vault
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: 23322a49-fb7e-4dc2-8d0e-43de8cd41f80
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/15/2017
ms.author: sngun
ms.openlocfilehash: 8c95c08fd55b98b1e25f7168b406536af71e57f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551637"
---
# <a name="deploy-a-vm-by-retrieving-the-password-stored-in-key-vault"></a><span data-ttu-id="6a9d0-103">Deploy a VM by retrieving the password stored in Key Vault</span><span class="sxs-lookup"><span data-stu-id="6a9d0-103">Deploy a VM by retrieving the password stored in Key Vault</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6a9d0-104">This topic applies only to Azure Stack Technical Preview 2.</span><span class="sxs-lookup"><span data-stu-id="6a9d0-104">This topic applies only to Azure Stack Technical Preview 2.</span></span>
>

<span data-ttu-id="6a9d0-105">When you need to pass a secure value (like a password) as a parameter during deployment, you can store that value as a secret in an Azure Stack key vault and reference the value in other Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="6a9d0-105">When you need to pass a secure value (like a password) as a parameter during deployment, you can store that value as a secret in an Azure Stack key vault and reference the value in other Azure Resource Manager templates.</span></span> <span data-ttu-id="6a9d0-106">You include only a reference to the secret in your template so the secret is never exposed.</span><span class="sxs-lookup"><span data-stu-id="6a9d0-106">You include only a reference to the secret in your template so the secret is never exposed.</span></span> <span data-ttu-id="6a9d0-107">You do not need to manually enter the value for the secret each time you deploy the resources.</span><span class="sxs-lookup"><span data-stu-id="6a9d0-107">You do not need to manually enter the value for the secret each time you deploy the resources.</span></span> <span data-ttu-id="6a9d0-108">You specify which users or service principals can access the secret.</span><span class="sxs-lookup"><span data-stu-id="6a9d0-108">You specify which users or service principals can access the secret.</span></span>

## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="6a9d0-109">Reference a secret with static ID</span><span class="sxs-lookup"><span data-stu-id="6a9d0-109">Reference a secret with static ID</span></span>
<span data-ttu-id="6a9d0-110">You reference the secret from within a parameters file, which passes values to your template.</span><span class="sxs-lookup"><span data-stu-id="6a9d0-110">You reference the secret from within a parameters file, which passes values to your template.</span></span> <span data-ttu-id="6a9d0-111">You reference the secret by passing the resource identifier of the key vault and the name of the secret.</span><span class="sxs-lookup"><span data-stu-id="6a9d0-111">You reference the secret by passing the resource identifier of the key vault and the name of the secret.</span></span> <span data-ttu-id="6a9d0-112">In this example, the key vault secret must already exist.</span><span class="sxs-lookup"><span data-stu-id="6a9d0-112">In this example, the key vault secret must already exist.</span></span> <span data-ttu-id="6a9d0-113">You use a static value for its resource ID.</span><span class="sxs-lookup"><span data-stu-id="6a9d0-113">You use a static value for its resource ID.</span></span>

    "parameters": {
    "adminPassword": {
    "reference": {
    "keyVault": {
    "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
    },
    "secretName": "{Secret name}"


> [!NOTE]
> <span data-ttu-id="6a9d0-114">The parameter that accepts the secret should be a *securestring*.</span><span class="sxs-lookup"><span data-stu-id="6a9d0-114">The parameter that accepts the secret should be a *securestring*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6a9d0-115">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6a9d0-115">Next Steps</span></span>
[<span data-ttu-id="6a9d0-116">Deploy a sample app with Key Vault</span><span class="sxs-lookup"><span data-stu-id="6a9d0-116">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="6a9d0-117">Deploy a VM with a Key Vault certificate</span><span class="sxs-lookup"><span data-stu-id="6a9d0-117">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

