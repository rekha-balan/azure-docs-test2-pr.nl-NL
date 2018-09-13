---
title: Prepare Azure Stack Public Key Infrastructure certificates for Azure Stack integrated systems deployment | Microsoft Docs
description: Describes how to prepare the Azure Stack PKI certificates for Azure Stack integrated systems.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: mabrigg
ms.reviewer: ppacent
ms.openlocfilehash: ef9fe0e05343f9c99656634a075b1bd464a13c7e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968247"
---
# <a name="prepare-azure-stack-pki-certificates-for-deployment"></a><span data-ttu-id="7f5fb-103">Prepare Azure Stack PKI certificates for deployment</span><span class="sxs-lookup"><span data-stu-id="7f5fb-103">Prepare Azure Stack PKI certificates for deployment</span></span>
<span data-ttu-id="7f5fb-104">The certificate files [obtained from your CA of choice](azure-stack-get-pki-certs.md) must be imported and exported with properties matching Azure Stack’s certificate requirements.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-104">The certificate files [obtained from your CA of choice](azure-stack-get-pki-certs.md) must be imported and exported with properties matching Azure Stack’s certificate requirements.</span></span>


## <a name="prepare-certificates-for-deployment"></a><span data-ttu-id="7f5fb-105">Prepare certificates for deployment</span><span class="sxs-lookup"><span data-stu-id="7f5fb-105">Prepare certificates for deployment</span></span>
<span data-ttu-id="7f5fb-106">Use these steps to prepare and validate the Azure Stack PKI certificates:</span><span class="sxs-lookup"><span data-stu-id="7f5fb-106">Use these steps to prepare and validate the Azure Stack PKI certificates:</span></span> 

### <a name="import-the-certificate"></a><span data-ttu-id="7f5fb-107">Import the certificate</span><span class="sxs-lookup"><span data-stu-id="7f5fb-107">Import the certificate</span></span>

1.  <span data-ttu-id="7f5fb-108">Copy the original certificate versions [obtained from your CA of choice](azure-stack-get-pki-certs.md) into a directory on the deployment host.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-108">Copy the original certificate versions [obtained from your CA of choice](azure-stack-get-pki-certs.md) into a directory on the deployment host.</span></span> 
  > [!WARNING]
  > <span data-ttu-id="7f5fb-109">Do not copy files that have already been imported, exported, or altered in any way from the files provided directly by the CA.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-109">Do not copy files that have already been imported, exported, or altered in any way from the files provided directly by the CA.</span></span>

1.  <span data-ttu-id="7f5fb-110">Right-click on the certificate and select **Install Certificate** or **Install PFX** depending on how the certificate was delivered from your CA.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-110">Right-click on the certificate and select **Install Certificate** or **Install PFX** depending on how the certificate was delivered from your CA.</span></span>

1. <span data-ttu-id="7f5fb-111">In the **Certificate Import Wizard**, select **Local Machine** as the import location.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-111">In the **Certificate Import Wizard**, select **Local Machine** as the import location.</span></span> <span data-ttu-id="7f5fb-112">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-112">Select **Next**.</span></span> <span data-ttu-id="7f5fb-113">On the following screen, click next again.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-113">On the following screen, click next again.</span></span>

    ![Local machine import location](.\media\prepare-pki-certs\1.png)

1.  <span data-ttu-id="7f5fb-115">Choose **Place all certificate in the following store** and then select **Enterprise Trust** as the location.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-115">Choose **Place all certificate in the following store** and then select **Enterprise Trust** as the location.</span></span> <span data-ttu-id="7f5fb-116">Click **OK** to close the certificate store selection dialog box and then **Next**.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-116">Click **OK** to close the certificate store selection dialog box and then **Next**.</span></span>

    ![Configure the certificate store](.\media\prepare-pki-certs\3.png)

    <span data-ttu-id="7f5fb-118">a.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-118">a.</span></span> <span data-ttu-id="7f5fb-119">If you are importing a PFX, you will be presented with an additional dialog.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-119">If you are importing a PFX, you will be presented with an additional dialog.</span></span> <span data-ttu-id="7f5fb-120">On the **Private key protection** page, enter the password for your certificate files and then enable the **Mark this key as exportable. This allows you to back up or transport your keys at a later time** option.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-120">On the **Private key protection** page, enter the password for your certificate files and then enable the **Mark this key as exportable. This allows you to back up or transport your keys at a later time** option.</span></span> <span data-ttu-id="7f5fb-121">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-121">Select **Next**.</span></span>

    ![Mark key as exportable](.\media\prepare-pki-certs\2.png)

1. <span data-ttu-id="7f5fb-123">Click Finish to complete the import.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-123">Click Finish to complete the import.</span></span>

### <a name="export-the-certificate"></a><span data-ttu-id="7f5fb-124">Export the certificate</span><span class="sxs-lookup"><span data-stu-id="7f5fb-124">Export the certificate</span></span>

<span data-ttu-id="7f5fb-125">Open Certificate Manager MMC console and connect to the Local Machine certificate store.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-125">Open Certificate Manager MMC console and connect to the Local Machine certificate store.</span></span>

1. <span data-ttu-id="7f5fb-126">Open the Microsoft Management Console, in Windows 10 right click on Start Menu, then click Run.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-126">Open the Microsoft Management Console, in Windows 10 right click on Start Menu, then click Run.</span></span> <span data-ttu-id="7f5fb-127">Type **mmc** click ok.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-127">Type **mmc** click ok.</span></span>

1. <span data-ttu-id="7f5fb-128">Click File, Add/Remove Snap-In then select Certificates click Add.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-128">Click File, Add/Remove Snap-In then select Certificates click Add.</span></span>

    ![Add Certificates Snap-in](.\media\prepare-pki-certs\mmc-2.png)
 
1. <span data-ttu-id="7f5fb-130">Select Computer account, click next then select Local computer then finish.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-130">Select Computer account, click next then select Local computer then finish.</span></span> <span data-ttu-id="7f5fb-131">Click ok to close the Add/Remove Snap-In page.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-131">Click ok to close the Add/Remove Snap-In page.</span></span>

    ![Add Certificates Snap-in](.\media\prepare-pki-certs\mmc-3.png)

1. <span data-ttu-id="7f5fb-133">Browse to Certificates > Enterprise Trust > Certificate location.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-133">Browse to Certificates > Enterprise Trust > Certificate location.</span></span> <span data-ttu-id="7f5fb-134">Verify that you see your certificate on the right.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-134">Verify that you see your certificate on the right.</span></span>

1. <span data-ttu-id="7f5fb-135">From the task bar of Certificate Manager console, select **Actions** > **All Tasks** > **Export**.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-135">From the task bar of Certificate Manager console, select **Actions** > **All Tasks** > **Export**.</span></span> <span data-ttu-id="7f5fb-136">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-136">Select **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7f5fb-137">Depending on how many Azure Stack certificates you have you may need to complete this process more than once.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-137">Depending on how many Azure Stack certificates you have you may need to complete this process more than once.</span></span>

1. <span data-ttu-id="7f5fb-138">Select **Yes, Export the Private Key**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-138">Select **Yes, Export the Private Key**, and then click **Next**.</span></span>

1. <span data-ttu-id="7f5fb-139">In the Export File Format section, select **Export all Extended Properties** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-139">In the Export File Format section, select **Export all Extended Properties** and then click **Next**.</span></span>

1. <span data-ttu-id="7f5fb-140">Select **Password** and provide a password for the certificates.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-140">Select **Password** and provide a password for the certificates.</span></span> <span data-ttu-id="7f5fb-141">Remember this password as it is used as a deployment parameter.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-141">Remember this password as it is used as a deployment parameter.</span></span> <span data-ttu-id="7f5fb-142">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-142">Select **Next**.</span></span>

1. <span data-ttu-id="7f5fb-143">Choose a file name and location for the pfx file to export.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-143">Choose a file name and location for the pfx file to export.</span></span> <span data-ttu-id="7f5fb-144">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-144">Select **Next**.</span></span>

1. <span data-ttu-id="7f5fb-145">Select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="7f5fb-145">Select **Finish**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f5fb-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f5fb-146">Next steps</span></span>
[<span data-ttu-id="7f5fb-147">Validate PKI certificates</span><span class="sxs-lookup"><span data-stu-id="7f5fb-147">Validate PKI certificates</span></span>](azure-stack-validate-pki-certs.md)