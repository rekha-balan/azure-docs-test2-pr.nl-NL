---
title: Set up PowerShell to create a VM for the Marketplace | Microsoft Docs
description: Instructions for setting up Azure PowerShell and using it as an optional process flow to create VM images to deploy to, and sell on, the Azure Marketplace
services: marketplace-publishing
documentationcenter: ''
author: HannibalSII
manager: hascipio
editor: ''
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: 68be118bc40e3a62aad73cb43119f49415f5b6a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671870"
---
# <a name="set-up-azure-powershell-to-create-an-offer-for-the-azure-marketplace"></a><span data-ttu-id="394d9-103">Set up Azure PowerShell to create an offer for the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="394d9-103">Set up Azure PowerShell to create an offer for the Azure Marketplace</span></span>
<span data-ttu-id="394d9-104">For detailed information on how to set up PowerShell in Azure, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="394d9-104">For detailed information on how to set up PowerShell in Azure, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="394d9-105">A simple approach is to use the certificate method, which downloads and imports a certificate needed for authentication.</span><span class="sxs-lookup"><span data-stu-id="394d9-105">A simple approach is to use the certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="394d9-106">To obtain the needed certificate, use the **Get-AzurePublishSettingsFile** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="394d9-106">To obtain the needed certificate, use the **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="394d9-107">Save the file when you're prompted.</span><span class="sxs-lookup"><span data-stu-id="394d9-107">Save the file when you're prompted.</span></span> <span data-ttu-id="394d9-108">To import the certificate into a PowerShell session, use the **Import-AzurePublishSettingsFile** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="394d9-108">To import the certificate into a PowerShell session, use the **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="394d9-109">To configure and store the common Microsoft Azure subscription settings for the PowerShell session, use the **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span><span class="sxs-lookup"><span data-stu-id="394d9-109">To configure and store the common Microsoft Azure subscription settings for the PowerShell session, use the **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="394d9-110">The first command associates a default storage account with the subscription (needed for some VM provisioning operations).</span><span class="sxs-lookup"><span data-stu-id="394d9-110">The first command associates a default storage account with the subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="394d9-111">The second makes the subscription the current one (recognized by other cmdlets).</span><span class="sxs-lookup"><span data-stu-id="394d9-111">The second makes the subscription the current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="394d9-112">See also</span><span class="sxs-lookup"><span data-stu-id="394d9-112">See also</span></span>
* [<span data-ttu-id="394d9-113">Getting started: How to publish an offer to the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="394d9-113">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="394d9-114">Creating a virtual machine image for the Marketplace</span><span class="sxs-lookup"><span data-stu-id="394d9-114">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

