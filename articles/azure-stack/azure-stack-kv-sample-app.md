---
title: Allow application to retrieve Azure Stack Key Vault secrets  | Microsoft Docs
description: Use a sample app to work with Azure Stack Key Vault
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: sngun
ms.openlocfilehash: 3d64805f30efe986c3be4408189ef823e5b72430
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671381"
---
# <a name="run-the-sample-application-for-key-vault"></a><span data-ttu-id="c0281-103">Run the sample application for Key Vault</span><span class="sxs-lookup"><span data-stu-id="c0281-103">Run the sample application for Key Vault</span></span>
<span data-ttu-id="c0281-104">In this guide, you'll use a sample application to retrieve secrets and passwords from Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c0281-104">In this guide, you'll use a sample application to retrieve secrets and passwords from Key Vault.</span></span>

> [!NOTE]
> <span data-ttu-id="c0281-105">In Technical Preview 3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only.</span><span class="sxs-lookup"><span data-stu-id="c0281-105">In Technical Preview 3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only.</span></span> <span data-ttu-id="c0281-106">If you are an administrator, sign in to the user portal to access and perform operations on a key vault.</span><span class="sxs-lookup"><span data-stu-id="c0281-106">If you are an administrator, sign in to the user portal to access and perform operations on a key vault.</span></span>

## <a name="download-the-samples-and-prepare"></a><span data-ttu-id="c0281-107">Download the samples and prepare</span><span class="sxs-lookup"><span data-stu-id="c0281-107">Download the samples and prepare</span></span>
<span data-ttu-id="c0281-108">Download the Azure Key Vault client samples from the [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="c0281-108">Download the Azure Key Vault client samples from the [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span>

<span data-ttu-id="c0281-109">Extract the contents of the .zip file to your local computer.</span><span class="sxs-lookup"><span data-stu-id="c0281-109">Extract the contents of the .zip file to your local computer.</span></span>

<span data-ttu-id="c0281-110">Read the **README.md** file (this is a text file), and then follow the instructions.</span><span class="sxs-lookup"><span data-stu-id="c0281-110">Read the **README.md** file (this is a text file), and then follow the instructions.</span></span>

## <a name="run-sample-1--hellokeyvault"></a><span data-ttu-id="c0281-111">Run Sample #1--HelloKeyVault</span><span class="sxs-lookup"><span data-stu-id="c0281-111">Run Sample #1--HelloKeyVault</span></span>
<span data-ttu-id="c0281-112">HelloKeyVault is a console application that walks through the key scenarios that are supported by Key Vault:</span><span class="sxs-lookup"><span data-stu-id="c0281-112">HelloKeyVault is a console application that walks through the key scenarios that are supported by Key Vault:</span></span>

1. <span data-ttu-id="c0281-113">Create/import a key (HSM or software key)</span><span class="sxs-lookup"><span data-stu-id="c0281-113">Create/import a key (HSM or software key)</span></span>
2. <span data-ttu-id="c0281-114">Encrypt a secret using a content key</span><span class="sxs-lookup"><span data-stu-id="c0281-114">Encrypt a secret using a content key</span></span>
3. <span data-ttu-id="c0281-115">Wrap the content key using a Key Vault key</span><span class="sxs-lookup"><span data-stu-id="c0281-115">Wrap the content key using a Key Vault key</span></span>
4. <span data-ttu-id="c0281-116">Unwrap the content key</span><span class="sxs-lookup"><span data-stu-id="c0281-116">Unwrap the content key</span></span>
5. <span data-ttu-id="c0281-117">Decrypt the secret</span><span class="sxs-lookup"><span data-stu-id="c0281-117">Decrypt the secret</span></span>
6. <span data-ttu-id="c0281-118">Set a secret</span><span class="sxs-lookup"><span data-stu-id="c0281-118">Set a secret</span></span>

<span data-ttu-id="c0281-119">That console application should run with no changes, except that the appropriate configuration settings in App.Config will be updated according to the following steps:</span><span class="sxs-lookup"><span data-stu-id="c0281-119">That console application should run with no changes, except that the appropriate configuration settings in App.Config will be updated according to the following steps:</span></span>

1. <span data-ttu-id="c0281-120">Update the app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret.</span><span class="sxs-lookup"><span data-stu-id="c0281-120">Update the app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret.</span></span> <span data-ttu-id="c0281-121">The information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.</span><span class="sxs-lookup"><span data-stu-id="c0281-121">The information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.</span></span>
2. <span data-ttu-id="c0281-122">Update the values of the mandatory variables in GetAppConfigSettings.ps1.</span><span class="sxs-lookup"><span data-stu-id="c0281-122">Update the values of the mandatory variables in GetAppConfigSettings.ps1.</span></span>
3. <span data-ttu-id="c0281-123">Launch the Windows PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="c0281-123">Launch the Windows PowerShell window.</span></span>
4. <span data-ttu-id="c0281-124">Run the GetAppConfigSettings.ps1 script within the PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="c0281-124">Run the GetAppConfigSettings.ps1 script within the PowerShell window.</span></span>
5. <span data-ttu-id="c0281-125">Copy the results of the script to the HelloKeyVault\App.config file.</span><span class="sxs-lookup"><span data-stu-id="c0281-125">Copy the results of the script to the HelloKeyVault\App.config file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0281-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0281-126">Next steps</span></span>
[<span data-ttu-id="c0281-127">Deploy a VM with a Key Vault password</span><span class="sxs-lookup"><span data-stu-id="c0281-127">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="c0281-128">Deploy a VM with a Key Vault certificate</span><span class="sxs-lookup"><span data-stu-id="c0281-128">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

