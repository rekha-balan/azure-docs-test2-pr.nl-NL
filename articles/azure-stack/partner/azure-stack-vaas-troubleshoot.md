---
title: Troubleshoot Azure Stack validation as a service | Microsoft Docs
description: Troubleshoot validation as a service for Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2018
ms.author: mabrigg
ms.reviewer: johnhas
ms.openlocfilehash: ed070ac4fdf9ccca1b1b4b99b8031bc3fd035779
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864490"
---
# <a name="troubleshoot-validation-as-a-service"></a><span data-ttu-id="daf52-103">Troubleshoot validation as a service</span><span class="sxs-lookup"><span data-stu-id="daf52-103">Troubleshoot validation as a service</span></span>

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

<span data-ttu-id="daf52-104">The following are common problems unrelated to software releases and their solutions.</span><span class="sxs-lookup"><span data-stu-id="daf52-104">The following are common problems unrelated to software releases and their solutions.</span></span>

## <a name="the-portal-shows-local-agent-in-debug-mode"></a><span data-ttu-id="daf52-105">The portal shows local agent in debug mode</span><span class="sxs-lookup"><span data-stu-id="daf52-105">The portal shows local agent in debug mode</span></span>

<span data-ttu-id="daf52-106">This is likely because the agent is unable to send heartbeats to the service because of an unstable network connection.</span><span class="sxs-lookup"><span data-stu-id="daf52-106">This is likely because the agent is unable to send heartbeats to the service because of an unstable network connection.</span></span> <span data-ttu-id="daf52-107">A heartbeat is sent every five minutes.</span><span class="sxs-lookup"><span data-stu-id="daf52-107">A heartbeat is sent every five minutes.</span></span> <span data-ttu-id="daf52-108">If the service does not receive a heartbeat for 15 minutes, then the service considers the agent inactive and tests will no longer be scheduled on it.</span><span class="sxs-lookup"><span data-stu-id="daf52-108">If the service does not receive a heartbeat for 15 minutes, then the service considers the agent inactive and tests will no longer be scheduled on it.</span></span> <span data-ttu-id="daf52-109">Check the error message in the *Agenthost.log* file located in the directory where the agent was started.</span><span class="sxs-lookup"><span data-stu-id="daf52-109">Check the error message in the *Agenthost.log* file located in the directory where the agent was started.</span></span>

> [!Note] 
> <span data-ttu-id="daf52-110">Any tests already running on the agent will continue to run, but if the heartbeat is not restored before the test ends, then the agent will fail to update the test status or upload logs.</span><span class="sxs-lookup"><span data-stu-id="daf52-110">Any tests already running on the agent will continue to run, but if the heartbeat is not restored before the test ends, then the agent will fail to update the test status or upload logs.</span></span> <span data-ttu-id="daf52-111">The test will always show up as **running** and will need to be canceled.</span><span class="sxs-lookup"><span data-stu-id="daf52-111">The test will always show up as **running** and will need to be canceled.</span></span>

## <a name="agent-process-on-machine-was-shut-down-while-executing-test-what-to-expect"></a><span data-ttu-id="daf52-112">Agent process on machine was shut down while executing test.</span><span class="sxs-lookup"><span data-stu-id="daf52-112">Agent process on machine was shut down while executing test.</span></span> <span data-ttu-id="daf52-113">What to expect?</span><span class="sxs-lookup"><span data-stu-id="daf52-113">What to expect?</span></span>

<span data-ttu-id="daf52-114">If the agent process is shut down ungracefully for example, machine restarted, process killed (CTRL+C on the agent window is considered graceful shutdown) then the test that was running on it will continue to show as **running**.</span><span class="sxs-lookup"><span data-stu-id="daf52-114">If the agent process is shut down ungracefully for example, machine restarted, process killed (CTRL+C on the agent window is considered graceful shutdown) then the test that was running on it will continue to show as **running**.</span></span> <span data-ttu-id="daf52-115">If the agent is restarted, then the agent will update the status of the test to **canceled**.</span><span class="sxs-lookup"><span data-stu-id="daf52-115">If the agent is restarted, then the agent will update the status of the test to **canceled**.</span></span> <span data-ttu-id="daf52-116">If the agent is not restarted, then the test appears as **running** and you must manually cancel the test</span><span class="sxs-lookup"><span data-stu-id="daf52-116">If the agent is not restarted, then the test appears as **running** and you must manually cancel the test</span></span>

> [!Note] 
> <span data-ttu-id="daf52-117">Tests within a workflow are scheduled to run sequentially.</span><span class="sxs-lookup"><span data-stu-id="daf52-117">Tests within a workflow are scheduled to run sequentially.</span></span> <span data-ttu-id="daf52-118">**Pending** tests will not get executed until tests in the **running** state in the same workflow complete.</span><span class="sxs-lookup"><span data-stu-id="daf52-118">**Pending** tests will not get executed until tests in the **running** state in the same workflow complete.</span></span>

## <a name="handle-slow-network-connectivity"></a><span data-ttu-id="daf52-119">Handle slow network connectivity</span><span class="sxs-lookup"><span data-stu-id="daf52-119">Handle slow network connectivity</span></span>

<span data-ttu-id="daf52-120">You can download the PIR image to a share in your local datacenter.</span><span class="sxs-lookup"><span data-stu-id="daf52-120">You can download the PIR image to a share in your local datacenter.</span></span> <span data-ttu-id="daf52-121">And then you can verify the image.</span><span class="sxs-lookup"><span data-stu-id="daf52-121">And then you can verify the image.</span></span>

<!-- This is from the appendix to the Deploy local agent topic. -->

### <a name="download-pir-image-to-local-share-in-case-of-slow-network-traffic"></a><span data-ttu-id="daf52-122">Download PIR image to local share in case of slow network traffic</span><span class="sxs-lookup"><span data-stu-id="daf52-122">Download PIR image to local share in case of slow network traffic</span></span>

1. <span data-ttu-id="daf52-123">Download AzCopy from: [vaasexternaldependencies(AzCopy)](https://vaasexternaldependencies.blob.core.windows.net/prereqcomponents/AzCopy.zip)</span><span class="sxs-lookup"><span data-stu-id="daf52-123">Download AzCopy from: [vaasexternaldependencies(AzCopy)](https://vaasexternaldependencies.blob.core.windows.net/prereqcomponents/AzCopy.zip)</span></span>

2. <span data-ttu-id="daf52-124">Extract AzCopy.zip and change to the directory containing AzCopy.exe</span><span class="sxs-lookup"><span data-stu-id="daf52-124">Extract AzCopy.zip and change to the directory containing AzCopy.exe</span></span>

3. <span data-ttu-id="daf52-125">Open Windows PowerShell from an elevated prompt.</span><span class="sxs-lookup"><span data-stu-id="daf52-125">Open Windows PowerShell from an elevated prompt.</span></span> <span data-ttu-id="daf52-126">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="daf52-126">Run the following commands:</span></span>

```PowerShell  
    .\azcopy.exe /Source:'https://azurestacktemplate.blob.core.windows.net/azurestacktemplate-public-container' /Dest:'<LocalFileShare>' /Pattern:'Server2016DatacenterFullBYOL.vhd' /NC:12 /V:azcopylog.log /Y
    .\azcopy.exe /Source:'https://azurestacktemplate.blob.core.windows.net/azurestacktemplate-public-container' /Dest:'<LocalFileShare>' /Pattern:'Server2016DatacenterCoreBYOL.vhd' /NC:12 /V:azcopylog.log /Y
    .\azcopy.exe /Source:'https://azurestacktemplate.blob.core.windows.net/azurestacktemplate-public-container' /Dest:'<LocalFileShare>' /Pattern:'WindowsServer2012R2DatacenterBYOL.vhd' /NC:12 /V:azcopylog.log /Y
    .\azcopy.exe /Source:'https://azurestacktemplate.blob.core.windows.net/azurestacktemplate-public-container' /Dest:'<LocalFileShare>' /Pattern:'Ubuntu1404LTS.vhd' /NC:12 /V:azcopylog.log /Y
    .\azcopy.exe /Source:'https://azurestacktemplate.blob.core.windows.net/azurestacktemplate-public-container' /Dest:'<LocalFileShare>' /Pattern:'Ubuntu1604-20170619.1.vhd' /NC:12 /V:azcopylog.log /Y
```

> [!Note]  
> <span data-ttu-id="daf52-127">LocalFileShare is the share path or local path.</span><span class="sxs-lookup"><span data-stu-id="daf52-127">LocalFileShare is the share path or local path.</span></span>

### <a name="verifying-pir-image-file-hash-value"></a><span data-ttu-id="daf52-128">Verifying PIR Image file hash value</span><span class="sxs-lookup"><span data-stu-id="daf52-128">Verifying PIR Image file hash value</span></span>

<span data-ttu-id="daf52-129">You can use **Get-HashFile** cmdlet to get the hash value for the downloaded public image repository image files to check the integrity of the images.</span><span class="sxs-lookup"><span data-stu-id="daf52-129">You can use **Get-HashFile** cmdlet to get the hash value for the downloaded public image repository image files to check the integrity of the images.</span></span>

| <span data-ttu-id="daf52-130">File Name</span><span class="sxs-lookup"><span data-stu-id="daf52-130">File Name</span></span> | <span data-ttu-id="daf52-131">SHA256</span><span class="sxs-lookup"><span data-stu-id="daf52-131">SHA256</span></span> |
|---------------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="daf52-132">Server2016DatacenterFullBYOL.vhd</span><span class="sxs-lookup"><span data-stu-id="daf52-132">Server2016DatacenterFullBYOL.vhd</span></span> | <span data-ttu-id="daf52-133">6ED58DCA666D530811A1EA563BA509BF9C29182B902D18FCA03C7E0868F733E9</span><span class="sxs-lookup"><span data-stu-id="daf52-133">6ED58DCA666D530811A1EA563BA509BF9C29182B902D18FCA03C7E0868F733E9</span></span> |
| <span data-ttu-id="daf52-134">WindowsServer2012R2DatacenterBYOL.vhd</span><span class="sxs-lookup"><span data-stu-id="daf52-134">WindowsServer2012R2DatacenterBYOL.vhd</span></span> | <span data-ttu-id="daf52-135">9792CBF742870B1730B9B16EA814C683A8415EFD7601DDB6D5A76D0964767028</span><span class="sxs-lookup"><span data-stu-id="daf52-135">9792CBF742870B1730B9B16EA814C683A8415EFD7601DDB6D5A76D0964767028</span></span> |
| <span data-ttu-id="daf52-136">Server2016DatacenterCoreBYOL.vhd</span><span class="sxs-lookup"><span data-stu-id="daf52-136">Server2016DatacenterCoreBYOL.vhd</span></span> | <span data-ttu-id="daf52-137">5E80E1A6721A48A10655E6154C1B90E320DF5558487D6A0D7BFC7DCD32C4D9A5</span><span class="sxs-lookup"><span data-stu-id="daf52-137">5E80E1A6721A48A10655E6154C1B90E320DF5558487D6A0D7BFC7DCD32C4D9A5</span></span> |
| <span data-ttu-id="daf52-138">Ubuntu1404LTS.vhd</span><span class="sxs-lookup"><span data-stu-id="daf52-138">Ubuntu1404LTS.vhd</span></span> | <span data-ttu-id="daf52-139">B24CDD12352AAEBC612A4558AB9E80F031A2190E46DCB459AF736072742E20E0</span><span class="sxs-lookup"><span data-stu-id="daf52-139">B24CDD12352AAEBC612A4558AB9E80F031A2190E46DCB459AF736072742E20E0</span></span> |
| <span data-ttu-id="daf52-140">Ubuntu1604-20170619.1.vhd</span><span class="sxs-lookup"><span data-stu-id="daf52-140">Ubuntu1604-20170619.1.vhd</span></span> | <span data-ttu-id="daf52-141">C481B88B60A01CBD5119A3F56632A2203EE5795678D3F3B9B764FFCA885E26CB</span><span class="sxs-lookup"><span data-stu-id="daf52-141">C481B88B60A01CBD5119A3F56632A2203EE5795678D3F3B9B764FFCA885E26CB</span></span> |

## <a name="next-steps"></a><span data-ttu-id="daf52-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="daf52-142">Next steps</span></span>

- <span data-ttu-id="daf52-143">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span><span class="sxs-lookup"><span data-stu-id="daf52-143">To learn more about [Azure Stack validation as a service](https://docs.microsoft.com/azure/azure-stack/partner).</span></span>
