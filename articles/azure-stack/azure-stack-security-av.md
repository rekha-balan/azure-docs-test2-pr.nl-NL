---
title: Update Windows Defender Antivirus on Azure Stack
description: Details on how antivirus is kept up to date on Azure Stack
services: azure-stack
author: PatAltimore
manager: femila
ms.service: azure-stack
ms.topic: article
ms.date: 06/13/2018
ms.author: patricka
ms.reviewer: fiseraci
ms.openlocfilehash: 3c4be228442bf67ccf16236e36cbf015eca6d4e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871298"
---
# <a name="update-windows-defender-antivirus-on-azure-stack"></a><span data-ttu-id="41735-103">Update Windows Defender Antivirus on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="41735-103">Update Windows Defender Antivirus on Azure Stack</span></span>

<span data-ttu-id="41735-104">[Windows Defender Antivirus](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10) is an antimalware solution that provides security and virus protection.</span><span class="sxs-lookup"><span data-stu-id="41735-104">[Windows Defender Antivirus](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10) is an antimalware solution that provides security and virus protection.</span></span> <span data-ttu-id="41735-105">Every Azure Stack infrastructure component (Hyper-V hosts and virtual machines) is protected with Windows Defender Antivirus.</span><span class="sxs-lookup"><span data-stu-id="41735-105">Every Azure Stack infrastructure component (Hyper-V hosts and virtual machines) is protected with Windows Defender Antivirus.</span></span> <span data-ttu-id="41735-106">For up-to-date protection, Windows Defender Antivirus definitions, engine, and platform require periodic updates.</span><span class="sxs-lookup"><span data-stu-id="41735-106">For up-to-date protection, Windows Defender Antivirus definitions, engine, and platform require periodic updates.</span></span> <span data-ttu-id="41735-107">How updates are applied depends on your configuration.</span><span class="sxs-lookup"><span data-stu-id="41735-107">How updates are applied depends on your configuration.</span></span> 

## <a name="connected-scenario"></a><span data-ttu-id="41735-108">Connected scenario</span><span class="sxs-lookup"><span data-stu-id="41735-108">Connected scenario</span></span>

<span data-ttu-id="41735-109">For antimalware definition and engine updates, the Azure Stack [update resource provider](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-updates#the-update-resource-provider) downloads antimalware definitions and engine updates multiple times per day.</span><span class="sxs-lookup"><span data-stu-id="41735-109">For antimalware definition and engine updates, the Azure Stack [update resource provider](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-updates#the-update-resource-provider) downloads antimalware definitions and engine updates multiple times per day.</span></span> <span data-ttu-id="41735-110">Each Azure Stack infrastructure component gets the update from the update resource provider and applies the update automatically.</span><span class="sxs-lookup"><span data-stu-id="41735-110">Each Azure Stack infrastructure component gets the update from the update resource provider and applies the update automatically.</span></span>

<span data-ttu-id="41735-111">For antimalware platform updates, apply the [monthly Azure Stack update](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-apply-updates).</span><span class="sxs-lookup"><span data-stu-id="41735-111">For antimalware platform updates, apply the [monthly Azure Stack update](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-apply-updates).</span></span> <span data-ttu-id="41735-112">The monthly Azure Stack update includes Windows Defender Antivirus platform updates for the month.</span><span class="sxs-lookup"><span data-stu-id="41735-112">The monthly Azure Stack update includes Windows Defender Antivirus platform updates for the month.</span></span>

## <a name="disconnected-scenario"></a><span data-ttu-id="41735-113">Disconnected scenario</span><span class="sxs-lookup"><span data-stu-id="41735-113">Disconnected scenario</span></span>

 <span data-ttu-id="41735-114">Apply the [monthly Azure Stack update](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-apply-updates).</span><span class="sxs-lookup"><span data-stu-id="41735-114">Apply the [monthly Azure Stack update](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-apply-updates).</span></span> <span data-ttu-id="41735-115">The monthly Azure Stack update includes Windows Defender Antivirus definitions, engine, and platform updates for the month.</span><span class="sxs-lookup"><span data-stu-id="41735-115">The monthly Azure Stack update includes Windows Defender Antivirus definitions, engine, and platform updates for the month.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41735-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="41735-116">Next steps</span></span>

[<span data-ttu-id="41735-117">Learn more about Azure Stack security</span><span class="sxs-lookup"><span data-stu-id="41735-117">Learn more about Azure Stack security</span></span>](azure-stack-security-foundations.md)
