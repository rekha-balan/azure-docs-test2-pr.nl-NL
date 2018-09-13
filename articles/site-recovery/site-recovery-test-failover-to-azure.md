---
title: Test failover to Azure in Site Recovery | Microsoft Docs
description: Learn about running a test failover from on-premises to Azure
services: site-recovery
documentationcenter: ''
author: prateek9us
manager: gauravd
editor: ''
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 2/15/2017
ms.author: pratshar
ms.openlocfilehash: 708158e17bab7c779f03fd36600a09b5fcc00ee7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553780"
---
# <a name="test--failover-to-azure-in-site-recovery"></a>Test  Failover to Azure in Site Recovery
> [!div class="op_single_selector"]
> * [Test Failover to Azure](./site-recovery-test-failover-to-azure.md)
> * [Test Failover (VMM to VMM)](./site-recovery-test-failover-vmm-to-vmm.md)


This article provides information and instructions for doing a test failover or a DR drill of virtual machines and physical servers that are protected with Site Recovery using Azure as the recovery site.

Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Test failover is run to validate your replication strategy or perform a disaster recovery drill without any data loss or downtime. Doing a test failover doesn't have any impact on the ongoing replication or on your production environment. Test failover can be done either on a virtual machine or a [recovery plan](site-recovery-create-recovery-plans.md). When triggering a test failover, you need to specify the network to which test virtual machines would connect to. Once a test failover is triggered, you can track progress in the **Jobs** page.  


## <a name="supported-scenarios"></a>Supported scenarios
Test failover is supported in all deployment scenarios other than [legacy VMware site to Azure](site-recovery-vmware-to-azure-classic-legacy.md). Test failover is also not supported when virtual machine has been failed over to Azure.  


## <a name="run-a-test-failover"></a>Run a test failover
This procedure describes how to run a test failover for a recovery plan. Alternatively you can also run test failover for a single machine by using the appropriate option on it.

![Test Failover](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-test-failover-to-azure/TestFailover.png)


1. Select **Recovery Plans** > *recoveryplan_name*. Click **Test Failover**.
1. Select a **Recovery Point** to failover to. You can use one of the following options:
    1.  **Latest processed**: This option fails over all virtual machines of the recovery plan to the latest recovery point that has already been processed by Site Recovery service. When you are doing test failover of a virtual machine, time stamp of the latest processed recovery point is also shown. If you are doing failover of a recovery plan, you can go to individual virtual machine and look at **Latest Recovery Points** tile to get this information. As no time is spent to process the unprocessed data, this option provides a low RTO (Recovery Time Objective) failover option.
    1.    **Latest app-consistent**: This option fails over all virtual machines of the recovery plan to the latest application consistent recovery point that has already been processed by Site Recovery service. When you are doing test failover of a virtual machine, time stamp of the latest app-consistent recovery point is also shown. If you are doing failover of a recovery plan, you can go to individual virtual machine and look at **Latest Recovery Points** tile to get this information.
    1.    **Latest**: This option first processes all the data that has been sent to Site Recovery service to create a recovery point for each virtual machine before failing them over to it. This option provides the lowest RPO (Recovery Point Objective) as the virtual machine created after failover will have all the data that has been replicated to Site Recovery service when the failover was triggered.
    1.  **Custom**: If you are doing test failover of a virtual machine, then you can use this option to failover to a particular recovery point.
1. Select an **Azure virtual network**: Provide an Azure virtual network where the test virtual machines would be created. Site Recovery attempts to create test virtual machines in a subnet of same name and using the same IP as that provided in **Compute and Network** settings of the virtual machine. If subnet of same name is not available in the Azure virtual network provided for test failover, then test virtual machine is created in the first subnet alphabetically. If same IP is not available in the subnet, then virtual machine gets another IP address available in the subnet. Read this section for [more details](#creating-a-network-for-test-failover)
1. If you're failing over to Azure and data encryption is enabled, in **Encryption Key** select the certificate that was issued when you enabled data encryption during Provider installation. You can ignore this step if you have not enabled encryption on the virtual machine.
1. Track failover progress on the **Jobs** tab. You should be able to see the test replica machine in the Azure portal.
1. To initiate an RDP connection on the virtual machine, you will need to [add a public ip](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) on the network interface of the failed over virtual machine. If you are failing over to a Classic virtual machine, then you need to [add an endpoint](../virtual-machines/windows/classic/setup-endpoints.md) on port 3389
1. Once you're done, click **Cleanup test failover** on the recovery plan. In **Notes** record and save any observations associated with the test failover. This deletes the virtual machines that were created during test failover.


> [!TIP]
> Site Recovery attempts to create test virtual machines in a subnet of same name and using the same IP as that provided in **Compute and Network** settings of the virtual machine. If subnet of same name is not available in the Azure virtual network provided for test failover, then test virtual machine is created in the first subnet alphabetically. If the target IP is part of the chosen subnet, then site recovery tries to create the test failover virtual machine using the target IP. If the target IP is not part of the chosen subnet then test failover virtual machine gets created using any available IP in the chosen subnet. 
>
>

## <a name="test-failover-job"></a>Test failover job

![Test Failover](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

When a test failover is triggered, it involves following steps:

1. Prerequisites check: This step ensures that all conditions required for failover are met
1. Failover: This step processes the data and makes it ready so that an Azure virtual machine can be created out of it. If you have chosen **Latest** recovery point, this step creates a recovery point from the data that has been sent to the service.
1. Start: This step creates an Azure virtual machine using the data processed in the previous step.


## <a name="creating-a-network-for-test-failover"></a>Creating a network for test failover
It is recommended that when you are doing a test failover you choose a network that is isolated from your production recovery site network that you provided in **Compute and Network** settings for the virtual machine. By default when you create an Azure virtual network, it is isolated from other networks. This network should mimic your production network:

1. Test network should have same number of subnets as that in your production network and with the same name as those of the subnets in your production network.
1. Test network should use the same IP range as that of your production network.
1. Update the DNS of the Test Network as the IP that you gave as target IP for the DNS virtual machine under **Compute and Network** settings. Go through [test failover considerations for active directory](site-recovery-active-directory.md#test-failover-considerations) section for more details.


## <a name="test-failover-to-a-production-network-on-recovery-site"></a>Test failover to a production network on recovery site
It is recommended that when you are doing a test failover you choose a network that is different from your production recovery site network that you provided in **Compute and Network** settings for the virtual machine. But if you really want to validate end to end network connectivity in a failed over virtual machine, note the following points:

1. Make sure that the primary virtual machine is shutdown when you are doing the test failover. If you don't do so, there will be two virtual machines with the same identity running in the same network at the same time and that can lead to undesired consequences.
1. Any changes that you make into the test failover virtual machines would be lost when you cleanup the test failover virtual machines. These changes will not be replicated back to the primary virtual machine.
1. This way of doing testing leads to a downtime of your production application. Users of the application should be asked to not use the application when the DR drill is in progress.  



## <a name="prepare-active-directory-and-dns"></a>Prepare Active Directory and DNS
To run a test failover for application testing, you need a copy of the production Active Directory environment in your test environment. Go through [test failover considerations for active directory](site-recovery-active-directory.md#test-failover-considerations) section for more details.

## <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Prepare to connect to Azure VMs after failover

If you want to connect to Azure VMs using RDP after failover, make sure you do the actions summarized in the table.

**Failover** | **Location** | **Actions**
--- | --- | ---
**Azure VM running Windows** | On on-premises machine before failover | To access the Azure VM over the internet, enable RDP, make sure TCP, and UDP rules are added for the **Public**, and that RDP is allowed in **Windows Firewall** > **Allowed Apps**, for all profiles.<br/><br/> To access over a site-to-site connection, enable RDP on the machine, and ensure that RDP is allowed in the **Windows Firewall** -> **Allowed apps and features** for **Domain and Private** networks.<br/><br/>  Make sure the operating system's SAN policy is set to **OnlineAll**. [Learn more](https://support.microsoft.com/kb/3031135).<br/><br/> Make sure there are no Windows updates pending on the virtual machine when you trigger a failover. Windows update might start when you failover and you will not be able to login to the virtual machine until the update completes. <br/><br/>
**Azure VM running Windows** | On Azure VM after failover | For a classic virtual machine, [add a public endpoint](../virtual-machines/windows/classic/setup-endpoints.md) for the RDP protocol (port 3389)<br/><br/>  For a Resource Manager virtual machine, [add a public IP](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) on it.<br/><br/> The network security group rules on the failed over VM, and the Azure subnet to which it is connected, need to allow incoming connections to the RDP port.<br/><br/> For a Resource Manager virtual machine, you can check **Boot diagnostics** to look at a screenshot of the virtual machine<br/><br/> If you can't connect, check that the VM is running and then look at these [troubleshooting tips](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).<br/><br/>
**Azure VM running Linux** | On on-premises machine before failover | Ensure that the Secure Shell service on the Azure VM is set to start automatically on system boot.<br/><br/> Check that firewall rules allow an SSH connection to it.
**Azure VM running Linux** | Azure VM after failover | The network security group rules on the failed over VM, and the Azure subnet to which it is connected, need to allow incoming connections to the SSH port.<br/><br/> For  a classic virtual machine, [add a public endpoint](../virtual-machines/windows/classic/setup-endpoints.md) should be created, to allow incoming connections on the SSH port (TCP port 22 by default).<br/><br/> For a Resource Manager virtual machine, [add a public IP](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) on it.<br/><br/> For a Resource Manager virtual machine, you can check **Boot diagnostics** to look at a screenshot of the virtual machine<br/><br/>



## <a name="next-steps"></a>Next Steps
Once you have successfully tried a test failover you can try doing a [failover](site-recovery-failover.md).


