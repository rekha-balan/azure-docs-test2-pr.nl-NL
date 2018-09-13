---
title: Multi-tenant support for VMware VM replication to Azure (CSP program) | Microsoft Docs
description: Describes how to deploy Azure Site Recovery in a multi-tenant environment to orchestrate replication, failover and recovery of on-premises VMware virtual machines to Azure through the CSP Program using the Azure portal
services: site-recovery
documentationcenter: ''
author: mayanknayar
manager: jwhit
editor: ''
ms.assetid: ''
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: manayar
ms.openlocfilehash: c10f51e012c3af7ceafd54dd420690e296cf4a72
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549940"
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-to-azure-through-the-csp-program"></a>Multi-tenant support in Azure Site Recovery for replicating VMware virtual machines to Azure through the CSP Program

Azure Site Recovery supports multi-tenant environments for tenant subscriptions. Multi-tenancy is also supported for tenant subscriptions created and managed through the CSP program. This article details the guidance for implementing and managing multi-tenant VMware-to-Azure scenarios. Creating and managing tenant subscriptions through CSP is also detailed.

Note that this guidance draws heavily from the existing documentation for replicating VMware virtual machines to Azure. This guidance should be used in conjunction with that [documentation](site-recovery-vmware-to-azure.md).

## <a name="multi-tenant-environments"></a>Multi-tenant environments
There are three major multi-tenant models:

1.  **Shared Hosting Services Provider (HSP)** – Here the partner owns the physical infrastructure and uses shared resources (vCenter, datacenters, physical storage, etc.) to host multiple tenants’ VMs on the same infrastructure. DR management can be provided by partner as a managed service or be owned by the tenant as a self-service DR solution.
2.  **Dedicated Hosting Services Provider** – Here the partner owns the physical infrastructure but uses dedicated resources (multiple vCenters, physical datastores, etc) to host each tenant’s VMs on separate infrastructure. DR management can again be managed by partner or self-service by the tenant.
3.  **Managed Services Provider (MSP)** – Here the customer owns the physical infrastructure that hosts the VMs and the partners provides DR enablement and management.

## <a name="shared-hosting-multi-tenant-guidance"></a>Shared hosting multi-tenant guidance
This guidance covers the shared hosting scenario in detail. The other two scenarios are subsets of the shared hosting scenario and use the same principles. The differences are described at the end of the shared hosting guidance.

The basic requirement in a multi-tenant scenario is isolating the different tenants that is, one tenant should not be able to observe what another tenant has hosted. In a completely partner-managed environment, this requirement is not as important as it for a self-service environment, where it can be critical. This guidance assumes that tenant isolation is required.

The architecture looks as follows:

![architecture-shared-hsp](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)

**Figure 1: Shared hosting scenario with one vCenter**

As seen from the above representation, each customer will have a separate Management Server. This is done to limit tenant access to tenant-specific VMs to enable tenant isolation. VMware virtual machine replication scenario uses the configuration server to manage accounts to discover VMs and install agents. We follow the same principles for multi-tenant environments, with the addition of restricting VM discovery through vCenter access control.

The data isolation requirement necessitates that all sensitive infrastructure information (such as access credentials) remains disclosed from tenants. For this reason, we recommend that all the components of the management server (Configuration Server (CS), Process Server (PS) and Master Target Server (MT)) remain under the exclusive control of the partner. This includes scale-out PS.

### <a name="every-cs-under-the-multi-tenant-scenario-uses-two-accounts"></a>Every CS under the multi-tenant scenario uses two accounts:

- **vCenter access account**: This account is used to discover tenant VMs and is the account has the vCenter access permissions assigned to it (described in the next section). It is recommended that the partner enters these credentials him/herself on the config tool to avoid accidental access leaks.
- **Virtual machine access account**: This account is used to install the mobility agent on the tenant VMs through automatic push. This is usually a domain account that a tenant might provide to partner or can alternatively be managed by partner directly. In case the tenant doesn’t wish to share the details to partner directly, the tenant can be allowed to enter the credentials through a limited-time access to CS, or alternatively the tenant can install mobility agents manually with the partner’s assistance.

### <a name="requirements-for-vcenter-access-account"></a>Requirements for vCenter access account

As detailed in the earlier section, the CS requires to be configured with an account that has a special role assigned to it. It is important to note that this role assignment needs to be done to the vCenter access account for each vCenter object and not propagated to the child objects. This is done to ensure tenant isolation since access propagation can result in accidental access to other objects also

![permissions-without-propagation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

The alternative is to assign the user account and role at the Datacenter object and propagate to child objects; following which that account has to be given a ‘No access’ role for every object (such as other tenants’ VMs) that should not be accessible to a particular tenant. This is both cumbersome and exposes accidental access controls, as every new child object created is also automatically granted access inherited from parent. It is hence suggested to go with the first approach.

The vCenter account access procedure is as follows:

1.  Create a new role by cloning the pre-defined ‘Read-only’ role and give it a convenient name (such as Azure_Site_Recovery used in this example).
2.  Assign the following permissions to this role:
 *  Datastore -> Allocate space, browse datastore, low-level file operations, remove file, update virtual machine files
 *  Network -> Network assign
 *  Resource -> Assign VM to resource pool, migrate powered off VM, migrate powered on VM
 *  Tasks -> Create task, update task
 *  Virtual machine -> Configuration
 *  Virtual machine -> Interact -> Answer question, device connection, configure CD media, configure floppy media, power off, power on, VMware tools install
 *  Virtual machine -> Inventory -> Create, register, unregister
 *  Virtual machine -> Provisioning -> Allow virtual machine download, allow virtual machine files upload
 *  Virtual machine -> Snapshots -> Remove snapshots.

    ![role-permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3.  Assign access level to the vCenter account (used in the tenant CS) for different objects as follows:

| **Object** | **Role** | **Remarks** |
| --- | --- | --- |
| vCenter | Read-Only | This is needed only to allow vCenter access for managing different objects. This permission can be removed if the account is never going to be provided to a tenant or used for any management operations on the vCenter. |
| Datacenter | Azure_Site_Recovery |  |
| Host and Host Cluster | Azure_Site_Recovery | Ensure again that access is at object level so only those hosts are accessible that will have tenant VMs before failover and after failback. |
| Datastore and Datastore Cluster | Azure_Site_Recovery | Same as above |
| Network | Azure_Site_Recovery |  |
| Management Server | Azure_Site_Recovery | This includes access to all components – CS, PS, and MT – if any are outside the CS machine. |
| Tenant VMs | Azure_Site_Recovery | Ensure that any new tenant VMs of a particular tenant also get this access else they will not be discoverable through the Azure portal. |

The vCenter account access is now complete. This fulfills the minimum permissions requirement to complete failback operations. Note that these access permissions can also be used with your existing policies. Just modify your existing permissions set to include role permissions from point 2 detailed above.

To restrict DR operations till the failover state that is, without failback capabilities, follow the above procedure but instead of assigning 'Azure_Site_Recovery' role to the vCenter access account, assign just a 'Read-Only' role to that account. This permission-set allows VM replication and failover and does not allow failback. Note that everything else in the above process remains as-is. Every permission is still assigned at the object level only and not propagated to child objects, to ensure tenant-isolation and restrict VM discovery.

## <a name="other-multi-tenant-environments"></a>Other multi-tenant environments

The above guidance described in detail how to set up a multi-tenant environment for a shared hosting solution. The other two major solutions are dedicated hosting and managed service. The architecture for these is as below:

### <a name="dedicated-hosting-solution"></a>Dedicated hosting solution

![architecture-shared-hsp](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)

**Figure 2: Dedicated hosting scenario with multiple vCenters**

The architectural difference here is that each tenant’s infrastructure is provisioned for that tenant only. The hosting provider still needs to follow the CSP steps detailed for shared hosting but does not need to worry about tenant isolation since tenants are isolated through separate vCenters. CSP provisioning remains unchanged.

### <a name="managed-service-solution"></a>Managed service solution

![architecture-shared-hsp](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)

**Figure 3: Managed service scenario with multiple vCenters**

The architectural difference here is that each tenant’s infrastructure is also physically separate from other tenants. This scenario usually exists when the tenant owns the infrastructure and just wants a solution provider to manage DR. The partner again needs to follow the CSP steps detailed for shared hosting but does not need to worry about tenant isolation since tenants are physically isolated through different infrastructures. CSP provisioning remains unchanged.


## <a name="csp-program-overview"></a>CSP program overview
Microsoft’s Cloud Solution Provider (CSP) [program](https://partner.microsoft.com/en-US/cloud-solution-provider) fosters better-together stories with partners for offering all Microsoft cloud services including O365, EMS, and Microsoft Azure. It enables our partners to own the end-to-end relationship with customers and become the primary relationship contact point. Through CSP, a partner can deploy Azure subscriptions for customers, and combine these subscriptions with their own value-added customized offerings.

In the case of Azure Site Recovery, partners can manage the complete Disaster Recovery solution for customers directly through CSP or use CSP to set up the Azure Site Recovery environments and let customers manage their own DR needs in a self-service manner. In both scenarios, the partner is the liaison between Azure Site Recovery and final customers, and the partner services the customer relationship and bills customers for Azure Site Recovery usage.

## <a name="creating-and-managing-tenant-accounts"></a>Creating and managing tenant accounts

### <a name="step-0-prerequisite-check"></a>Step 0: Prerequisite check

The VM prerequisites are the same as described in the Azure Site Recovery [documentation](site-recovery-vmware-to-azure.md). In addition to those prerequisites, the above access controls should be in place before proceeding with tenant management through CSP. Create a separate Management Server for each tenant that can communicate with the tenant VMs and partner’s vCenter. Only the partner has access rights to this server.

### <a name="step-1-create-tenant-account"></a>Step 1: Create tenant account

1.  Through [partner center](https://partnercenter.microsoft.com/) login to your CSP account. From the Dashboard menu on the left, select the ‘Customers’ option.

    ![csp-dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

2.  On the page that opens click on the ‘Add customer’ button.

    ![add-customer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

3.  On the New Customer page, fill in all the account information details for the tenant and click on ‘Next:Subscriptions’.

    ![fill-details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

4.  On the subscriptions selection page, scroll down to add the ‘Microsoft Azure’ subscription. Other subscriptions can be added now or at any other time in the future.

    ![add-subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

5.  Continue forward and on the next page review all the details entered for the tenant and click on the Submit button.

    ![customer-summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)

6.  After the customer is created you get a confirmation page with the details of the default account and password for that subscription. Save the information and change the password later as necessary through the Azure portal login. This information can be shared as-is with the tenant or a separate account can be also created and shared if required.

### <a name="step-2-access-tenant-account"></a>Step 2: Access tenant account

1.  You can access the tenant’s subscription from the ‘Customers’ page through your Dashboard as described in step 1. Navigate here and click on the name of the tenant account just created.
2.  This opens the Subscriptions section of the tenant account and from here you can monitor the existing subscriptions for the account and add more subscriptions as required. To manage the tenant’s DR operations, select the ‘All resources (Azure portal) option on the right side of the page.

    ![all-resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)

3.  Clicking the ‘All resources’ button grants you access to the tenant’s Azure subscriptions and you can verify the same by checking the AAD displayed on the top right corner of the Azure portal.

    ![aad-admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

You can now perform all Site Recovery operations for the tenant through the Azure portal and manage the DR operations. The process detailed above must be followed every time to access the tenant subscription through CSP for managed DR.

### <a name="step-3-deploy-resources-to-tenant-subscription"></a>Step 3: Deploy resources to tenant subscription
1.  On the Azure portal, create a Resource Group and deploy a Recovery Services vault per the usual process. Download the vault registration key.
2.  Register the CS for the tenant using the vault registration key.
3.  Enter the credentials for the two access accounts – vCenter access account and VM access account.

    ![config-accounts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-to-recovery-services-vault"></a>Step 4: Register site recovery infrastructure to Recovery Services vault
1.  Open the Azure portal and on the vault created earlier register the vCenter server to CS registered in the previous step. Use the vCenter access account for this purpose.
2.  Finish the ‘Prepare infrastructure’ process for Site Recovery per the usual process.
3.  The VMs are now ready to be replicated. Verify that only the tenant’s VMs are visible on the VM selection blade under the Replicate option.

    ![tenant-vms](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-to-subscription"></a>Step 5: Assign tenant access to subscription

For the case of self-service DR the account details as mentioned in item 6 of Step 1 must be provided to the tenant. This should be done after the partner sets up the DR infrastructure. Irrespective of DR type (managed or self-service) the partner is required to access tenant subscriptions through CSP portal only and setup the vault and register infrastructure owned by the partner to the tenant subscriptions.

A partner can also add a new user to the tenant subscription through the CSP portal as follows:

1.  Go to the particular tenant’s CSP subscription page and select the ‘Users and licenses’ option.

    ![user-licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    You can now create a new user by entering the relevant details and selecting permissions, or alternatively uploading the list of users though a CSV file.
2.  Once the users are created, go back to the Azure portal and under the Subscription blade select the relevant subscription.
3.  On the new blade that opens select Access Control (IAM) and click on +Add to add a user with the relevant access level. The users created through CSP portal will automatically be displayed on the blade that opens after clicking an access level.

    ![user-subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    For most management operations, the Contributor role is sufficient. A user with this access level can do everything on a subscription except change access levels (for which an Owner level access is required). You can also fine-tune the access levels as required.
















