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
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-to-azure-with-azure-site-recovery"></a>Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery

This article describes how to migrate AWS Windows instances to Azure virtual machines with the [Azure Site Recovery](site-recovery-overview.md) service.

Migration is effectively a failover from AWS to Azure. You can't failback machines to AWS, and there's no ongoing replication. This article describes the steps for migration in the Azure portal, and are based on the instructions for [replicating a physical machine to Azure](site-recovery-vmware-to-azure.md).

Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>Supported operating systems

Site Recovery can be used to migrate EC2 instances running any of the following operating systems:

- Windows(64 bit only)
    - Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only. **Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2
- Linux (64 bit only)
    - Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)

## <a name="prerequisites"></a>Prerequisites

Here's what you need for this deployment

* **Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as the configuration server. By default, the other Azure Site Recovery components (process server and master target server) are installed when you deploy the configuration server. This article describes the steps for migration in the Azure portal, and are based on the instructions for  [Learn more](site-recovery-components.md#vmware-to-azure)

* **EC2 instances**: The Amazon EC2 virtual machines instances that you want to migrate.

## <a name="deployment-steps"></a>Deployment steps

1. Create a Recovery Services vault

2. The Security Group of your EC2 instances should have the following rules configured: ![Rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic1.png)

3. On the same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server. Refer the VMware / Physical to Azure prerequisites for configuration server deployment requirements ![DeployCS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see the configuration server and process server under Site Recovery infrastructure as shown below: ![CSinVault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic3.png)
  >[!NOTE]
  >It may take up to 15 minutes for the configuration server and process server to show up
  >

5. After you've deployed the configuration server, validate that it can communicate with the VMs that you want to migrate.

6. [Set up replication settings](site-recovery-setup-replication-settings-vmware.md)

7. Enable replication: Enable replication for the VMs you want to migrate. You can discover the EC2 instances using the private IP addresses, which you can get from the EC2 console.
![SelectVM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic4.PNG)
8. Once the EC2 instances have been protected and the replication to Azure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) to validate your application's performance in Azure ![TFI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic5.PNG)

9. Run a Failover from AWS to Azure for each VM. Optionally, you can create a recovery plan and run a Failover, to migrate multiple virtual machines from AWS to Azure. [Learn more](site-recovery-create-recovery-plans.md) about recovery plans.

10. For migration, you don't need to commit a failover. Instead, you select the Complete Migration option for each machine you want to migrate. The Complete Migration action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.![Migrate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-migrate-aws-to-azure/migration_pic6.png)






