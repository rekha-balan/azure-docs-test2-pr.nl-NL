---
title: Evaluate the Azure Stack Development Kit | Microsoft Docs
description: Learn how to deploy the Azure Stack Development Kit for evaluation purposes.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/04/2018
ms.author: jeffgilb
ms.custom: mvc
ms.openlocfilehash: a0e742ab3ac43cc7977761dd94c9689e3a7c2e0b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869249"
---
# <a name="quickstart-evaluate-the-azure-stack-development-kit"></a><span data-ttu-id="49ae9-103">Quickstart: evaluate the Azure Stack Development Kit</span><span class="sxs-lookup"><span data-stu-id="49ae9-103">Quickstart: evaluate the Azure Stack Development Kit</span></span>

<span data-ttu-id="49ae9-104">The [Azure Stack Development Kit (ASDK)](.\asdk\asdk-what-is.md) is a testing and development environment that you can deploy to evaluate and demonstrate Azure Stack features and services.</span><span class="sxs-lookup"><span data-stu-id="49ae9-104">The [Azure Stack Development Kit (ASDK)](.\asdk\asdk-what-is.md) is a testing and development environment that you can deploy to evaluate and demonstrate Azure Stack features and services.</span></span> <span data-ttu-id="49ae9-105">To get started with the ASDK, you need to prepare the host computer hardware and then run some scripts (installation takes several hours).</span><span class="sxs-lookup"><span data-stu-id="49ae9-105">To get started with the ASDK, you need to prepare the host computer hardware and then run some scripts (installation takes several hours).</span></span> <span data-ttu-id="49ae9-106">After that, you can sign in to the administrator or user portals to start using Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="49ae9-106">After that, you can sign in to the administrator or user portals to start using Azure Stack.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49ae9-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="49ae9-107">Prerequisites</span></span>

### <a name="asdk-host-computer-requirements"></a><span data-ttu-id="49ae9-108">ASDK host computer requirements</span><span class="sxs-lookup"><span data-stu-id="49ae9-108">ASDK host computer requirements</span></span>

<span data-ttu-id="49ae9-109">Before installing the ASDK, you need to prepare the computer that will host the development kit.</span><span class="sxs-lookup"><span data-stu-id="49ae9-109">Before installing the ASDK, you need to prepare the computer that will host the development kit.</span></span> <span data-ttu-id="49ae9-110">The development kit host computer must meet the hardware, software, and network requirements described in **[Review the ASDK deployment planning considerations](.\asdk\asdk-deploy-considerations.md)**.</span><span class="sxs-lookup"><span data-stu-id="49ae9-110">The development kit host computer must meet the hardware, software, and network requirements described in **[Review the ASDK deployment planning considerations](.\asdk\asdk-deploy-considerations.md)**.</span></span>

> [!TIP]
> <span data-ttu-id="49ae9-111">You can use the [Azure Stack deployment requirements check tool](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) after installing the operating system on the development kit host computer to confirm that your hardware meets all requirements.</span><span class="sxs-lookup"><span data-stu-id="49ae9-111">You can use the [Azure Stack deployment requirements check tool](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) after installing the operating system on the development kit host computer to confirm that your hardware meets all requirements.</span></span>

### <a name="account-requirements"></a><span data-ttu-id="49ae9-112">Account requirements</span><span class="sxs-lookup"><span data-stu-id="49ae9-112">Account requirements</span></span>

<span data-ttu-id="49ae9-113">You also need to choose between using Azure Active Directory (Azure AD) or Active Directory Federation Services (AD FS) as the identity solution for your deployment.</span><span class="sxs-lookup"><span data-stu-id="49ae9-113">You also need to choose between using Azure Active Directory (Azure AD) or Active Directory Federation Services (AD FS) as the identity solution for your deployment.</span></span> <span data-ttu-id="49ae9-114">Review the account requirements in **[deployment planning considerations](.\asdk\asdk-deploy-considerations.md#account-requirements)**</span><span class="sxs-lookup"><span data-stu-id="49ae9-114">Review the account requirements in **[deployment planning considerations](.\asdk\asdk-deploy-considerations.md#account-requirements)**</span></span>

## <a name="download-and-extract-the-deployment-package"></a><span data-ttu-id="49ae9-115">Download and extract the deployment package</span><span class="sxs-lookup"><span data-stu-id="49ae9-115">Download and extract the deployment package</span></span>

<span data-ttu-id="49ae9-116">After preparing your development kit host computer, download and extract the ASDK deployment package.</span><span class="sxs-lookup"><span data-stu-id="49ae9-116">After preparing your development kit host computer, download and extract the ASDK deployment package.</span></span> <span data-ttu-id="49ae9-117">The deployment package includes the Cloudbuilder.vhdx file, which is a virtual hard drive (VHD) with a bootable operating system, and the Azure Stack installation files.</span><span class="sxs-lookup"><span data-stu-id="49ae9-117">The deployment package includes the Cloudbuilder.vhdx file, which is a virtual hard drive (VHD) with a bootable operating system, and the Azure Stack installation files.</span></span>

<span data-ttu-id="49ae9-118">You can download the deployment package to the development kit host or to another computer.</span><span class="sxs-lookup"><span data-stu-id="49ae9-118">You can download the deployment package to the development kit host or to another computer.</span></span> <span data-ttu-id="49ae9-119">The extracted deployment files take up 60 GB of free disk space, so using another computer can help reduce the storage requirements on the development kit host.</span><span class="sxs-lookup"><span data-stu-id="49ae9-119">The extracted deployment files take up 60 GB of free disk space, so using another computer can help reduce the storage requirements on the development kit host.</span></span>

<span data-ttu-id="49ae9-120">**[Download and extract the Azure Stack Development Kit (ASDK)](.\asdk\asdk-download.md)**</span><span class="sxs-lookup"><span data-stu-id="49ae9-120">**[Download and extract the Azure Stack Development Kit (ASDK)](.\asdk\asdk-download.md)**</span></span>

## <a name="prepare-the-host-computer"></a><span data-ttu-id="49ae9-121">Prepare the host computer</span><span class="sxs-lookup"><span data-stu-id="49ae9-121">Prepare the host computer</span></span>

<span data-ttu-id="49ae9-122">Before you can install the ASDK, the host environment must be prepared and the system configured to boot from the development kit VHD.</span><span class="sxs-lookup"><span data-stu-id="49ae9-122">Before you can install the ASDK, the host environment must be prepared and the system configured to boot from the development kit VHD.</span></span> <span data-ttu-id="49ae9-123">When you restart the host, it boots from CloudBuilder.vhdx and you can start deploying the ASDK.</span><span class="sxs-lookup"><span data-stu-id="49ae9-123">When you restart the host, it boots from CloudBuilder.vhdx and you can start deploying the ASDK.</span></span>

<span data-ttu-id="49ae9-124">**[Prepare the ASDK host computer](.\asdk\asdk-prepare-host.md)**</span><span class="sxs-lookup"><span data-stu-id="49ae9-124">**[Prepare the ASDK host computer](.\asdk\asdk-prepare-host.md)**</span></span>

## <a name="install-the-asdk-on-the-host-computer"></a><span data-ttu-id="49ae9-125">Install the ASDK on the host computer</span><span class="sxs-lookup"><span data-stu-id="49ae9-125">Install the ASDK on the host computer</span></span>

<span data-ttu-id="49ae9-126">After the host computer boots from the VHD, you can deploy the development kit to the Cloudbuilder virtual environment.</span><span class="sxs-lookup"><span data-stu-id="49ae9-126">After the host computer boots from the VHD, you can deploy the development kit to the Cloudbuilder virtual environment.</span></span> <span data-ttu-id="49ae9-127">You can deploy the ASDK using the graphical user interface (GUI), provided by running the asdk-installer.ps1 PowerShell script, or from [the PowerShell command line](.\asdk\asdk-deploy-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="49ae9-127">You can deploy the ASDK using the graphical user interface (GUI), provided by running the asdk-installer.ps1 PowerShell script, or from [the PowerShell command line](.\asdk\asdk-deploy-powershell.md)</span></span>

> [!NOTE]
> <span data-ttu-id="49ae9-128">After the host boots from the Cloudbuilder.vhdx image, you have the option of configuring [Azure Stack telemetry settings](.\asdk\asdk-telemetry.md#set-telemetry-level-in-the-windows-registry) *before* installing the ASDK.</span><span class="sxs-lookup"><span data-stu-id="49ae9-128">After the host boots from the Cloudbuilder.vhdx image, you have the option of configuring [Azure Stack telemetry settings](.\asdk\asdk-telemetry.md#set-telemetry-level-in-the-windows-registry) *before* installing the ASDK.</span></span>

<span data-ttu-id="49ae9-129">**[Install the Azure Stack Development Kit (ASDK)](.\asdk\asdk-install.md)**</span><span class="sxs-lookup"><span data-stu-id="49ae9-129">**[Install the Azure Stack Development Kit (ASDK)](.\asdk\asdk-install.md)**</span></span>

## <a name="perform-post-deployment-configurations"></a><span data-ttu-id="49ae9-130">Perform post-deployment configurations</span><span class="sxs-lookup"><span data-stu-id="49ae9-130">Perform post-deployment configurations</span></span>

<span data-ttu-id="49ae9-131">After installing the ASDK, there are a few recommended post-installation checks and configuration changes that should be made.</span><span class="sxs-lookup"><span data-stu-id="49ae9-131">After installing the ASDK, there are a few recommended post-installation checks and configuration changes that should be made.</span></span>

<span data-ttu-id="49ae9-132">**Tools**</span><span class="sxs-lookup"><span data-stu-id="49ae9-132">**Tools**</span></span>

<span data-ttu-id="49ae9-133">Install Azure Stack PowerShell and GitHub tools, and check the success of your installation using the test-AzureStack cmdlet.</span><span class="sxs-lookup"><span data-stu-id="49ae9-133">Install Azure Stack PowerShell and GitHub tools, and check the success of your installation using the test-AzureStack cmdlet.</span></span>

<span data-ttu-id="49ae9-134">**Identity solution**</span><span class="sxs-lookup"><span data-stu-id="49ae9-134">**Identity solution**</span></span>

<span data-ttu-id="49ae9-135">For a deployment that uses Azure AD, you must activate both the Azure Stack administrator and tenant portals.</span><span class="sxs-lookup"><span data-stu-id="49ae9-135">For a deployment that uses Azure AD, you must activate both the Azure Stack administrator and tenant portals.</span></span> <span data-ttu-id="49ae9-136">This activation consents to giving the Azure Stack portal and Azure Resource Manager the correct permissions (listed on the consent page) for all users of the directory.</span><span class="sxs-lookup"><span data-stu-id="49ae9-136">This activation consents to giving the Azure Stack portal and Azure Resource Manager the correct permissions (listed on the consent page) for all users of the directory.</span></span>

<span data-ttu-id="49ae9-137">**Password expiration**</span><span class="sxs-lookup"><span data-stu-id="49ae9-137">**Password expiration**</span></span>

<span data-ttu-id="49ae9-138">You should reset the password expiration policy to make sure that the password for the development kit host doesn't expire before your evaluation period ends.</span><span class="sxs-lookup"><span data-stu-id="49ae9-138">You should reset the password expiration policy to make sure that the password for the development kit host doesn't expire before your evaluation period ends.</span></span>

> [!NOTE]
> <span data-ttu-id="49ae9-139">You also have the option of configuring [Azure Stack telemetry settings](.\asdk\asdk-telemetry.md#enable-or-disable-telemetry-after-deployment) *after* installing the ASDK.</span><span class="sxs-lookup"><span data-stu-id="49ae9-139">You also have the option of configuring [Azure Stack telemetry settings](.\asdk\asdk-telemetry.md#enable-or-disable-telemetry-after-deployment) *after* installing the ASDK.</span></span>

<span data-ttu-id="49ae9-140">**[Post-ASDK deployment tasks](.\asdk\asdk-post-deploy.md)**</span><span class="sxs-lookup"><span data-stu-id="49ae9-140">**[Post-ASDK deployment tasks](.\asdk\asdk-post-deploy.md)**</span></span>

## <a name="register-with-azure"></a><span data-ttu-id="49ae9-141">Register with Azure</span><span class="sxs-lookup"><span data-stu-id="49ae9-141">Register with Azure</span></span>

<span data-ttu-id="49ae9-142">You must register Azure Stack with Azure so that you can [download Azure marketplace items](.\asdk\asdk-marketplace-item.md) to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="49ae9-142">You must register Azure Stack with Azure so that you can [download Azure marketplace items](.\asdk\asdk-marketplace-item.md) to Azure Stack.</span></span>

<span data-ttu-id="49ae9-143">**[Register Azure Stack with Azure](.\asdk\asdk-register.md)**</span><span class="sxs-lookup"><span data-stu-id="49ae9-143">**[Register Azure Stack with Azure](.\asdk\asdk-register.md)**</span></span>

## <a name="next-steps"></a><span data-ttu-id="49ae9-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="49ae9-144">Next steps</span></span>

<span data-ttu-id="49ae9-145">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="49ae9-145">Congratulations!</span></span> <span data-ttu-id="49ae9-146">By completing the steps in this quickstart you have an ASDK environment with an [administrator](https://adminportal.local.azurestack.external) portal and a [user](https://portal.local.azurestack.external) portal.</span><span class="sxs-lookup"><span data-stu-id="49ae9-146">By completing the steps in this quickstart you have an ASDK environment with an [administrator](https://adminportal.local.azurestack.external) portal and a [user](https://portal.local.azurestack.external) portal.</span></span>
