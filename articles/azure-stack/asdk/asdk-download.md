---
title: Download and extract the Azure Stack Development Kit (ASDK) | Microsoft Docs
description: Describes how to download and extract the Azure Stack Development Kit (ASDK).
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: a6ccfa439b58d36ee44d5f8441c2058622965653
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866239"
---
# <a name="download-and-extract-the-azure-stack-development-kit-asdk"></a><span data-ttu-id="c203a-103">Download and extract the Azure Stack Development Kit (ASDK)</span><span class="sxs-lookup"><span data-stu-id="c203a-103">Download and extract the Azure Stack Development Kit (ASDK)</span></span>
<span data-ttu-id="c203a-104">After ensuring that your development kit host computer meets the basic requirements for installing the ASDK, the next step is to download and extract the ASDK deployment package to get the Cloudbuilder.vhdx.</span><span class="sxs-lookup"><span data-stu-id="c203a-104">After ensuring that your development kit host computer meets the basic requirements for installing the ASDK, the next step is to download and extract the ASDK deployment package to get the Cloudbuilder.vhdx.</span></span>

## <a name="download-the-asdk"></a><span data-ttu-id="c203a-105">Download the ASDK</span><span class="sxs-lookup"><span data-stu-id="c203a-105">Download the ASDK</span></span>
1. <span data-ttu-id="c203a-106">Before you start the download, make sure that your computer meets the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="c203a-106">Before you start the download, make sure that your computer meets the following prerequisites:</span></span>

  - <span data-ttu-id="c203a-107">The computer must have at least 60 GB of free disk space available on four separate, identical logical hard drives in addition to the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="c203a-107">The computer must have at least 60 GB of free disk space available on four separate, identical logical hard drives in addition to the operating system disk.</span></span>
  - <span data-ttu-id="c203a-108">[.NET Framework 4.6 (or a later version)](https://aka.ms/r6mkiy) must be installed.</span><span class="sxs-lookup"><span data-stu-id="c203a-108">[.NET Framework 4.6 (or a later version)](https://aka.ms/r6mkiy) must be installed.</span></span>

2. <span data-ttu-id="c203a-109">[Go to the Get Started page](https://azure.microsoft.com/overview/azure-stack/try/?v=try) where you can download the Azure Stack Development Kit, provide your details, and then click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="c203a-109">[Go to the Get Started page](https://azure.microsoft.com/overview/azure-stack/try/?v=try) where you can download the Azure Stack Development Kit, provide your details, and then click **Submit**.</span></span>
3. <span data-ttu-id="c203a-110">Download and run the [Deployment Checker for Azure Stack Development Kit](https://go.microsoft.com/fwlink/?LinkId=828735&clcid=0x409) prerequisite checker script.</span><span class="sxs-lookup"><span data-stu-id="c203a-110">Download and run the [Deployment Checker for Azure Stack Development Kit](https://go.microsoft.com/fwlink/?LinkId=828735&clcid=0x409) prerequisite checker script.</span></span> <span data-ttu-id="c203a-111">This standalone script goes through the pre-requisites checks done by the setup for Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="c203a-111">This standalone script goes through the pre-requisites checks done by the setup for Azure Stack Development Kit.</span></span> <span data-ttu-id="c203a-112">It provides a way to confirm you are meeting the hardware and software requirements, before downloading the larger package for Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="c203a-112">It provides a way to confirm you are meeting the hardware and software requirements, before downloading the larger package for Azure Stack Development Kit.</span></span>
4. <span data-ttu-id="c203a-113">Under **Download the software**, click **Azure Stack Development Kit**.</span><span class="sxs-lookup"><span data-stu-id="c203a-113">Under **Download the software**, click **Azure Stack Development Kit**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c203a-114">The ASDK download (AzureStackDevelopmentKit.exe) is approximately 10GB.</span><span class="sxs-lookup"><span data-stu-id="c203a-114">The ASDK download (AzureStackDevelopmentKit.exe) is approximately 10GB.</span></span>

## <a name="extract-the-asdk"></a><span data-ttu-id="c203a-115">Extract the ASDK</span><span class="sxs-lookup"><span data-stu-id="c203a-115">Extract the ASDK</span></span>
1. <span data-ttu-id="c203a-116">After the download completes, click **Run** to launch the ASDK self-extractor (AzureStackDevelopmentKit.exe).</span><span class="sxs-lookup"><span data-stu-id="c203a-116">After the download completes, click **Run** to launch the ASDK self-extractor (AzureStackDevelopmentKit.exe).</span></span>
2. <span data-ttu-id="c203a-117">Review and accept the displayed license agreement from the **License Agreement** page of the Self-Extractor Wizard and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c203a-117">Review and accept the displayed license agreement from the **License Agreement** page of the Self-Extractor Wizard and then click **Next**.</span></span>
3. <span data-ttu-id="c203a-118">Review the privacy statement information displayed on the **Important Notice** page of the Self-Extractor Wizard and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c203a-118">Review the privacy statement information displayed on the **Important Notice** page of the Self-Extractor Wizard and then click **Next**.</span></span>
4. <span data-ttu-id="c203a-119">Select the location for Azure Stack setup files to be extracted to on the **Select Destination Location** page of the Self-Extractor Wizard and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c203a-119">Select the location for Azure Stack setup files to be extracted to on the **Select Destination Location** page of the Self-Extractor Wizard and then click **Next**.</span></span> <span data-ttu-id="c203a-120">The default location is *current folder*\Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="c203a-120">The default location is *current folder*\Azure Stack Development Kit.</span></span> 
5. <span data-ttu-id="c203a-121">Review the destination location summary on the **Ready to Extract** page of the Self-Extractor Wizard, and then click **Extract** to extract the CloudBuilder.vhdx (approximately 28GB) and ThirdPartyLicenses.rtf files.</span><span class="sxs-lookup"><span data-stu-id="c203a-121">Review the destination location summary on the **Ready to Extract** page of the Self-Extractor Wizard, and then click **Extract** to extract the CloudBuilder.vhdx (approximately 28GB) and ThirdPartyLicenses.rtf files.</span></span> <span data-ttu-id="c203a-122">This process takes some time to complete.</span><span class="sxs-lookup"><span data-stu-id="c203a-122">This process takes some time to complete.</span></span>
6. <span data-ttu-id="c203a-123">Copy or move the CloudBuilder.vhdx file to the root of the C:\ drive (C:\CloudBuilder.vhdx) on the ASDK host computer.</span><span class="sxs-lookup"><span data-stu-id="c203a-123">Copy or move the CloudBuilder.vhdx file to the root of the C:\ drive (C:\CloudBuilder.vhdx) on the ASDK host computer.</span></span>

> [!NOTE]
> <span data-ttu-id="c203a-124">After you extract the files, you can delete the .EXE and .BIN files to recover hard disk space.</span><span class="sxs-lookup"><span data-stu-id="c203a-124">After you extract the files, you can delete the .EXE and .BIN files to recover hard disk space.</span></span> <span data-ttu-id="c203a-125">Or, you can back up these files so that you don’t need to download the files again if you need to redeploy the ASDK.</span><span class="sxs-lookup"><span data-stu-id="c203a-125">Or, you can back up these files so that you don’t need to download the files again if you need to redeploy the ASDK.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c203a-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="c203a-126">Next steps</span></span>
[<span data-ttu-id="c203a-127">Prepare the ASDK host computer</span><span class="sxs-lookup"><span data-stu-id="c203a-127">Prepare the ASDK host computer</span></span>](asdk-prepare-host.md)