---
title: Migrate VMs from AWS to Azure| Microsoft Docs
description: This article describes how to migrate virtual machines running in Amazon Web Services (AWS) to Azure using Azure Site Recovery.
services: site-recovery
documentationcenter: ''
author: bsiva
manager: jwhit
editor: ''
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 02/12/2017
ms.author: bsiva
ms.openlocfilehash: 43de90de9855964c314cff67637c2cbec868b896
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564695"
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-to-azure-with-azure-site-recovery"></a><span data-ttu-id="e0d6d-103">Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e0d6d-103">Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery</span></span>

<span data-ttu-id="e0d6d-104">This article describes how to migrate AWS Windows instances to Azure virtual machines with the [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-104">This article describes how to migrate AWS Windows instances to Azure virtual machines with the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="e0d6d-105">Migration is effectively a failover from AWS to Azure.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-105">Migration is effectively a failover from AWS to Azure.</span></span> <span data-ttu-id="e0d6d-106">You can't failback machines to AWS, and there's no ongoing replication.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-106">You can't failback machines to AWS, and there's no ongoing replication.</span></span> <span data-ttu-id="e0d6d-107">This article describes the steps for migration in the Azure portal, and are based on the instructions for [replicating a physical machine to Azure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e0d6d-107">This article describes the steps for migration in the Azure portal, and are based on the instructions for [replicating a physical machine to Azure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="e0d6d-108">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-108">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="e0d6d-109">Supported operating systems</span><span class="sxs-lookup"><span data-stu-id="e0d6d-109">Supported operating systems</span></span>

<span data-ttu-id="e0d6d-110">Site Recovery can be used to migrate EC2 instances running any of the following operating systems:</span><span class="sxs-lookup"><span data-stu-id="e0d6d-110">Site Recovery can be used to migrate EC2 instances running any of the following operating systems:</span></span>

- <span data-ttu-id="e0d6d-111">Windows(64 bit only)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="e0d6d-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="e0d6d-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e0d6d-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="e0d6d-114">Linux (64 bit only)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="e0d6d-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0d6d-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e0d6d-116">Prerequisites</span></span>

<span data-ttu-id="e0d6d-117">Here's what you need for this deployment</span><span class="sxs-lookup"><span data-stu-id="e0d6d-117">Here's what you need for this deployment</span></span>

* <span data-ttu-id="e0d6d-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as the configuration server.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as the configuration server.</span></span> <span data-ttu-id="e0d6d-119">By default, the other Azure Site Recovery components (process server and master target server) are installed when you deploy the configuration server.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-119">By default, the other Azure Site Recovery components (process server and master target server) are installed when you deploy the configuration server.</span></span> <span data-ttu-id="e0d6d-120">This article describes the steps for migration in the Azure portal, and are based on the instructions for  [Learn more](site-recovery-components.md#vmware-to-azure)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-120">This article describes the steps for migration in the Azure portal, and are based on the instructions for  [Learn more](site-recovery-components.md#vmware-to-azure)</span></span>

* <span data-ttu-id="e0d6d-121">**EC2 instances**: The Amazon EC2 virtual machines instances that you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-121">**EC2 instances**: The Amazon EC2 virtual machines instances that you want to migrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="e0d6d-122">Deployment steps</span><span class="sxs-lookup"><span data-stu-id="e0d6d-122">Deployment steps</span></span>

1. <span data-ttu-id="e0d6d-123">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="e0d6d-123">Create a Recovery Services vault</span></span>

2. <span data-ttu-id="e0d6d-124">The Security Group of your EC2 instances should have the following rules configured: ![Rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic1.png)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-124">The Security Group of your EC2 instances should have the following rules configured: ![Rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic1.png)</span></span>

3. <span data-ttu-id="e0d6d-125">On the same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-125">On the same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="e0d6d-126">Refer the VMware / Physical to Azure prerequisites for configuration server deployment requirements ![DeployCS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic2.png)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-126">Refer the VMware / Physical to Azure prerequisites for configuration server deployment requirements ![DeployCS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic2.png)</span></span>

4.  <span data-ttu-id="e0d6d-127">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see the configuration server and process server under Site Recovery infrastructure as shown below: ![CSinVault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic3.png)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-127">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see the configuration server and process server under Site Recovery infrastructure as shown below: ![CSinVault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic3.png)</span></span>
  >[!NOTE]
  ><span data-ttu-id="e0d6d-128">It may take up to 15 minutes for the configuration server and process server to show up</span><span class="sxs-lookup"><span data-stu-id="e0d6d-128">It may take up to 15 minutes for the configuration server and process server to show up</span></span>
  >

5. <span data-ttu-id="e0d6d-129">After you've deployed the configuration server, validate that it can communicate with the VMs that you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-129">After you've deployed the configuration server, validate that it can communicate with the VMs that you want to migrate.</span></span>

6. [<span data-ttu-id="e0d6d-130">Set up replication settings</span><span class="sxs-lookup"><span data-stu-id="e0d6d-130">Set up replication settings</span></span>](site-recovery-setup-replication-settings-vmware.md)

7. <span data-ttu-id="e0d6d-131">Enable replication: Enable replication for the VMs you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-131">Enable replication: Enable replication for the VMs you want to migrate.</span></span> <span data-ttu-id="e0d6d-132">You can discover the EC2 instances using the private IP addresses, which you can get from the EC2 console.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-132">You can discover the EC2 instances using the private IP addresses, which you can get from the EC2 console.</span></span>
<span data-ttu-id="e0d6d-133">![SelectVM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic4.PNG)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-133">![SelectVM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic4.PNG)</span></span>
8. <span data-ttu-id="e0d6d-134">Once the EC2 instances have been protected and the replication to Azure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) to validate your application's performance in Azure ![TFI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic5.PNG)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-134">Once the EC2 instances have been protected and the replication to Azure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) to validate your application's performance in Azure ![TFI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic5.PNG)</span></span>

9. <span data-ttu-id="e0d6d-135">Run a Failover from AWS to Azure for each VM.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-135">Run a Failover from AWS to Azure for each VM.</span></span> <span data-ttu-id="e0d6d-136">Optionally, you can create a recovery plan and run a Failover, to migrate multiple virtual machines from AWS to Azure.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-136">Optionally, you can create a recovery plan and run a Failover, to migrate multiple virtual machines from AWS to Azure.</span></span> <span data-ttu-id="e0d6d-137">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-137">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="e0d6d-138">For migration, you don't need to commit a failover.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-138">For migration, you don't need to commit a failover.</span></span> <span data-ttu-id="e0d6d-139">Instead, you select the Complete Migration option for each machine you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-139">Instead, you select the Complete Migration option for each machine you want to migrate.</span></span> <span data-ttu-id="e0d6d-140">The Complete Migration action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-140">The Complete Migration action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>![Migrate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic6.png)






