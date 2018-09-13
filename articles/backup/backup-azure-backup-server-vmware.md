---
title: Use Azure Backup Server to protect VMware Server | Microsoft Docs
description: Back up a VMware Server to Azure or disk, with Azure Backup Server. Use this article to protect your VMware workload.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/28/2017
ms.author: markgal;
ms.openlocfilehash: 4e599fed44bf46a29b12e1ca96e60355782080dd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551655"
---
# <a name="back-up-vmware-server-to-azure"></a><span data-ttu-id="7fc48-104">Back up VMware server to Azure</span><span class="sxs-lookup"><span data-stu-id="7fc48-104">Back up VMware server to Azure</span></span>

<span data-ttu-id="7fc48-105">This article explains how to connect a VMware server to an Azure Backup Server so you can back up VMware server contents to the cloud.</span><span class="sxs-lookup"><span data-stu-id="7fc48-105">This article explains how to connect a VMware server to an Azure Backup Server so you can back up VMware server contents to the cloud.</span></span> <span data-ttu-id="7fc48-106">This article assumes you already have Azure Backup Server installed.</span><span class="sxs-lookup"><span data-stu-id="7fc48-106">This article assumes you already have Azure Backup Server installed.</span></span>

## <a name="create-secure-connection-to-vmware-server"></a><span data-ttu-id="7fc48-107">Create secure connection to VMware server</span><span class="sxs-lookup"><span data-stu-id="7fc48-107">Create secure connection to VMware server</span></span>

<span data-ttu-id="7fc48-108">To protect a VMware Server, Azure Backup Server must be able to securely connect to the VMware Server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-108">To protect a VMware Server, Azure Backup Server must be able to securely connect to the VMware Server.</span></span> <span data-ttu-id="7fc48-109">To enable the secure connection, install a valid certificate on the VMware Server and Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-109">To enable the secure connection, install a valid certificate on the VMware Server and Azure Backup Server.</span></span>

<span data-ttu-id="7fc48-110">When you connect to the VMware server, if the URL is not secure, then you need to export the certificate so the connection to the site is secure.</span><span class="sxs-lookup"><span data-stu-id="7fc48-110">When you connect to the VMware server, if the URL is not secure, then you need to export the certificate so the connection to the site is secure.</span></span>
<span data-ttu-id="7fc48-111">![example of unsecured connection to VMware server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/unsecure-url.png)</span><span class="sxs-lookup"><span data-stu-id="7fc48-111">![example of unsecured connection to VMware server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/unsecure-url.png)</span></span>

1. <span data-ttu-id="7fc48-112">Click https (with the strike through), and then on the pop-up menu, click the Details link.</span><span class="sxs-lookup"><span data-stu-id="7fc48-112">Click https (with the strike through), and then on the pop-up menu, click the Details link.</span></span>

  <span data-ttu-id="7fc48-113">Depending on your browser, you may need to click **Settings** > **More Tools** > **Developer Tools**, and select the Security tab.</span><span class="sxs-lookup"><span data-stu-id="7fc48-113">Depending on your browser, you may need to click **Settings** > **More Tools** > **Developer Tools**, and select the Security tab.</span></span>

  ![example of unsecured connection error message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/security-tab.png)

2. <span data-ttu-id="7fc48-115">In the details information on the Security tab, click **View Certificate**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-115">In the details information on the Security tab, click **View Certificate**.</span></span>

  ![example of unsecured connection error message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/security-tab-view-certificate.png)

  <span data-ttu-id="7fc48-117">The Certificate dialog opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-117">The Certificate dialog opens.</span></span>

3. <span data-ttu-id="7fc48-118">In the Certificate dialog, click the Certification Path tab.</span><span class="sxs-lookup"><span data-stu-id="7fc48-118">In the Certificate dialog, click the Certification Path tab.</span></span>  

  ![<span data-ttu-id="7fc48-119">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-119">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/certificate-certification-path.png)

  <span data-ttu-id="7fc48-120">The highlighted certificate is not trusted because in this certificate's case, the issuer could not be found.</span><span class="sxs-lookup"><span data-stu-id="7fc48-120">The highlighted certificate is not trusted because in this certificate's case, the issuer could not be found.</span></span> <span data-ttu-id="7fc48-121">There may be other reasons why the certificate is not trusted.</span><span class="sxs-lookup"><span data-stu-id="7fc48-121">There may be other reasons why the certificate is not trusted.</span></span>

4. <span data-ttu-id="7fc48-122">To export the certificate to your local machine, click the Details tab, and then click Copy to File.</span><span class="sxs-lookup"><span data-stu-id="7fc48-122">To export the certificate to your local machine, click the Details tab, and then click Copy to File.</span></span>

  ![<span data-ttu-id="7fc48-123">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-123">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/certificate-details-tab.png)

  <span data-ttu-id="7fc48-124">The Certificate Export Wizard opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-124">The Certificate Export Wizard opens.</span></span>

  ![<span data-ttu-id="7fc48-125">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-125">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/certificate-wizard1.png)

  <span data-ttu-id="7fc48-126">Click **Next** to move through the wizard.</span><span class="sxs-lookup"><span data-stu-id="7fc48-126">Click **Next** to move through the wizard.</span></span>

5. <span data-ttu-id="7fc48-127">On the Export File Format screen, specify the format you prefer for the certificate.</span><span class="sxs-lookup"><span data-stu-id="7fc48-127">On the Export File Format screen, specify the format you prefer for the certificate.</span></span> <span data-ttu-id="7fc48-128">If you don't have a preferred format, accept the default file format for the certificate and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-128">If you don't have a preferred format, accept the default file format for the certificate and click **Next**.</span></span>

  ![<span data-ttu-id="7fc48-129">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-129">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/certificate-wizard1b.png)

6. <span data-ttu-id="7fc48-130">On the File to Export screen, give your certificate a name, and then click Browse to choose the location to store the certificate on your local computer.</span><span class="sxs-lookup"><span data-stu-id="7fc48-130">On the File to Export screen, give your certificate a name, and then click Browse to choose the location to store the certificate on your local computer.</span></span> <span data-ttu-id="7fc48-131">Save the certificate where you can find it.</span><span class="sxs-lookup"><span data-stu-id="7fc48-131">Save the certificate where you can find it.</span></span>

  ![<span data-ttu-id="7fc48-132">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-132">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/certificate-wizard2.png)

7. <span data-ttu-id="7fc48-133">After exporting the certificate, go to the location where you saved it, right-click the certificate and from the menu, select **Install Certificate**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-133">After exporting the certificate, go to the location where you saved it, right-click the certificate and from the menu, select **Install Certificate**.</span></span>

  <span data-ttu-id="7fc48-134">The Certificate Import Wizard opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-134">The Certificate Import Wizard opens.</span></span>

  ![<span data-ttu-id="7fc48-135">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-135">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/cert-import-wizard1.png)

8. <span data-ttu-id="7fc48-136">On the Certificate Import Wizard, select **Local Machine** as the destination for the certificate, and click **Next** to continue.</span><span class="sxs-lookup"><span data-stu-id="7fc48-136">On the Certificate Import Wizard, select **Local Machine** as the destination for the certificate, and click **Next** to continue.</span></span>

9. <span data-ttu-id="7fc48-137">On the Certificate Store screen, select **Place all certificates in the following store** and click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-137">On the Certificate Store screen, select **Place all certificates in the following store** and click **Browse**.</span></span>

  ![<span data-ttu-id="7fc48-138">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-138">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

  <span data-ttu-id="7fc48-139">The Select Certificate Store dialog opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-139">The Select Certificate Store dialog opens.</span></span>

  ![<span data-ttu-id="7fc48-140">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-140">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/cert-store.png)

  <span data-ttu-id="7fc48-141">Choose the destination folder for the certificates, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-141">Choose the destination folder for the certificates, and click **OK**.</span></span> <span data-ttu-id="7fc48-142">If you don't know which folder to use, choose Trusted Root Certification Authorities.</span><span class="sxs-lookup"><span data-stu-id="7fc48-142">If you don't know which folder to use, choose Trusted Root Certification Authorities.</span></span> <span data-ttu-id="7fc48-143">The chosen destination folder appears in the Certificate store dialog.</span><span class="sxs-lookup"><span data-stu-id="7fc48-143">The chosen destination folder appears in the Certificate store dialog.</span></span> <span data-ttu-id="7fc48-144">Click **Next** to import the certificate.</span><span class="sxs-lookup"><span data-stu-id="7fc48-144">Click **Next** to import the certificate.</span></span>

10. <span data-ttu-id="7fc48-145">On the Completing the Certificate Import Wizard screen, verify the certificate is in the desired folder, and click Finish to complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="7fc48-145">On the Completing the Certificate Import Wizard screen, verify the certificate is in the desired folder, and click Finish to complete the wizard.</span></span>

  ![<span data-ttu-id="7fc48-146">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-146">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

  <span data-ttu-id="7fc48-147">A dialog appears letting you know if the import was successful.</span><span class="sxs-lookup"><span data-stu-id="7fc48-147">A dialog appears letting you know if the import was successful.</span></span>

11. <span data-ttu-id="7fc48-148">Log in to the VMware VM to check that you have secure connection to the VMware server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-148">Log in to the VMware VM to check that you have secure connection to the VMware server.</span></span> <span data-ttu-id="7fc48-149">The Azure Backup Server connects to the VMware server over a secure HTTPs channel.</span><span class="sxs-lookup"><span data-stu-id="7fc48-149">The Azure Backup Server connects to the VMware server over a secure HTTPs channel.</span></span> <span data-ttu-id="7fc48-150">If you have secure boundaries within your organization, and don't want to enable HTTPs protocol, then disable the secure communication via the registry.</span><span class="sxs-lookup"><span data-stu-id="7fc48-150">If you have secure boundaries within your organization, and don't want to enable HTTPs protocol, then disable the secure communication via the registry.</span></span> <span data-ttu-id="7fc48-151">However, it is recommended that you install certificates on Azure Backup Server and VMware server to enable secure communication.</span><span class="sxs-lookup"><span data-stu-id="7fc48-151">However, it is recommended that you install certificates on Azure Backup Server and VMware server to enable secure communication.</span></span>


## <a name="create-role-and-user-account-on-vmware-server"></a><span data-ttu-id="7fc48-152">Create role and user account on VMware server</span><span class="sxs-lookup"><span data-stu-id="7fc48-152">Create role and user account on VMware server</span></span>

<span data-ttu-id="7fc48-153">Azure Backup Server communicates with a remote VMware server by authenticating a specified VMware user's credentials.</span><span class="sxs-lookup"><span data-stu-id="7fc48-153">Azure Backup Server communicates with a remote VMware server by authenticating a specified VMware user's credentials.</span></span> <span data-ttu-id="7fc48-154">Azure Backup Server authenticates the VMware user's credentials for all backup operations.</span><span class="sxs-lookup"><span data-stu-id="7fc48-154">Azure Backup Server authenticates the VMware user's credentials for all backup operations.</span></span> <span data-ttu-id="7fc48-155">Use the Azure Backup Server's Production Server Addition wizard, to enable Azure Backup Server to securely communicate with the VMware server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-155">Use the Azure Backup Server's Production Server Addition wizard, to enable Azure Backup Server to securely communicate with the VMware server.</span></span> <span data-ttu-id="7fc48-156">There are three phases to setting up the relationship between Azure Backup Server and</span><span class="sxs-lookup"><span data-stu-id="7fc48-156">There are three phases to setting up the relationship between Azure Backup Server and</span></span> 

- <span data-ttu-id="7fc48-157">Create a user role that has assigned privileges</span><span class="sxs-lookup"><span data-stu-id="7fc48-157">Create a user role that has assigned privileges</span></span>
- <span data-ttu-id="7fc48-158">Create a user account with credentials - a username and password</span><span class="sxs-lookup"><span data-stu-id="7fc48-158">Create a user account with credentials - a username and password</span></span>
- <span data-ttu-id="7fc48-159">Add the VMware server user account to Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="7fc48-159">Add the VMware server user account to Azure Backup Server</span></span>

<span data-ttu-id="7fc48-160">, when going through the Production Server Addition Wizard.</span><span class="sxs-lookup"><span data-stu-id="7fc48-160">, when going through the Production Server Addition Wizard.</span></span> <span data-ttu-id="7fc48-161">The username and password pair are stored as a credential.</span><span class="sxs-lookup"><span data-stu-id="7fc48-161">The username and password pair are stored as a credential.</span></span>


### <a name="create-user-role-and-add-privileges"></a><span data-ttu-id="7fc48-162">Create user role and add privileges</span><span class="sxs-lookup"><span data-stu-id="7fc48-162">Create user role and add privileges</span></span>
<span data-ttu-id="7fc48-163">The VMware user account, which is specified in the Azure Backup Server credential, must have certain associated privileges.</span><span class="sxs-lookup"><span data-stu-id="7fc48-163">The VMware user account, which is specified in the Azure Backup Server credential, must have certain associated privileges.</span></span> <span data-ttu-id="7fc48-164">However, privileges are associated with a user role, so we'll first create a user role and then add specific privileges to that role.</span><span class="sxs-lookup"><span data-stu-id="7fc48-164">However, privileges are associated with a user role, so we'll first create a user role and then add specific privileges to that role.</span></span> <span data-ttu-id="7fc48-165">The privileges that are associated with the user role are for a backup administrator.</span><span class="sxs-lookup"><span data-stu-id="7fc48-165">The privileges that are associated with the user role are for a backup administrator.</span></span>

1. <span data-ttu-id="7fc48-166">To create a new VMware user role, log in to your VMware server, and on the **Navigator** panel click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-166">To create a new VMware user role, log in to your VMware server, and on the **Navigator** panel click **Administration**.</span></span>

  ![<span data-ttu-id="7fc48-167">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-167">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="7fc48-168">To create a new role, in the **Administration** section, select **Roles** and in the **Roles** panel click the Add role icon, (the + symbol).</span><span class="sxs-lookup"><span data-stu-id="7fc48-168">To create a new role, in the **Administration** section, select **Roles** and in the **Roles** panel click the Add role icon, (the + symbol).</span></span>

  ![<span data-ttu-id="7fc48-169">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-169">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

  <span data-ttu-id="7fc48-170">The **Create Role** dialog opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-170">The **Create Role** dialog opens.</span></span>

  ![<span data-ttu-id="7fc48-171">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-171">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="7fc48-172">In the **Create Role** dialog, in the **Role name** field, type a name for the role.</span><span class="sxs-lookup"><span data-stu-id="7fc48-172">In the **Create Role** dialog, in the **Role name** field, type a name for the role.</span></span> <span data-ttu-id="7fc48-173">In this example, we'll use the name, *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="7fc48-173">In this example, we'll use the name, *BackupAdminRole*.</span></span> <span data-ttu-id="7fc48-174">The role name can be whatever you like, but the name should be recognizable for the role.</span><span class="sxs-lookup"><span data-stu-id="7fc48-174">The role name can be whatever you like, but the name should be recognizable for the role.</span></span>

4. <span data-ttu-id="7fc48-175">Select the privileges to apply them to the user role.</span><span class="sxs-lookup"><span data-stu-id="7fc48-175">Select the privileges to apply them to the user role.</span></span> <span data-ttu-id="7fc48-176">Select the privileges in the following list.</span><span class="sxs-lookup"><span data-stu-id="7fc48-176">Select the privileges in the following list.</span></span> <span data-ttu-id="7fc48-177">When selecting the privileges, click the chevron on the parent label to expand the parent and view the child privileges.</span><span class="sxs-lookup"><span data-stu-id="7fc48-177">When selecting the privileges, click the chevron on the parent label to expand the parent and view the child privileges.</span></span> <span data-ttu-id="7fc48-178">You don't need to select all child privileges within a parent privilege.</span><span class="sxs-lookup"><span data-stu-id="7fc48-178">You don't need to select all child privileges within a parent privilege.</span></span>

  ![<span data-ttu-id="7fc48-179">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-179">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  - <span data-ttu-id="7fc48-180">Privilege.Datastore.AllocateSpace.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-180">Privilege.Datastore.AllocateSpace.label</span></span>
  - <span data-ttu-id="7fc48-181">Privilege.Global.ManageCustomerFields.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-181">Privilege.Global.ManageCustomerFields.label</span></span>
  - <span data-ttu-id="7fc48-182">privilege.Network.Assign.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-182">privilege.Network.Assign.label</span></span>
  - <span data-ttu-id="7fc48-183">Privilege.VirtualMachine.Config.AddNewDisk.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-183">Privilege.VirtualMachine.Config.AddNewDisk.label</span></span>
  - <span data-ttu-id="7fc48-184">Privilege.VirtualMachine.Config.AdvanceConfig.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-184">Privilege.VirtualMachine.Config.AdvanceConfig.label</span></span>
  - <span data-ttu-id="7fc48-185">Privilege.VirtualMachine.Config.ChangeTracking.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-185">Privilege.VirtualMachine.Config.ChangeTracking.label</span></span>
  - <span data-ttu-id="7fc48-186">Privilege.VirtualMachine.Config.HostUSBDevice.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-186">Privilege.VirtualMachine.Config.HostUSBDevice.label</span></span>
  - <span data-ttu-id="7fc48-187">Privilege.VirtualMachine.Config.SwapPlacement.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-187">Privilege.VirtualMachine.Config.SwapPlacement.label</span></span>  
  - <span data-ttu-id="7fc48-188">Privilege.VirtualMachine.Interact.PowerOff.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-188">Privilege.VirtualMachine.Interact.PowerOff.label</span></span>
  - <span data-ttu-id="7fc48-189">Privilege.VirtualMachine.Inventory.Create.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-189">Privilege.VirtualMachine.Inventory.Create.label</span></span>
  - <span data-ttu-id="7fc48-190">Privilege.VirtualMachine.Provisioning.DiskRandomRead.summary</span><span class="sxs-lookup"><span data-stu-id="7fc48-190">Privilege.VirtualMachine.Provisioning.DiskRandomRead.summary</span></span>
  - <span data-ttu-id="7fc48-191">Privilege.VirtualMachine.State.CreateSnapshot.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-191">Privilege.VirtualMachine.State.CreateSnapshot.label</span></span>
  - <span data-ttu-id="7fc48-192">Privilege.VirtualMachine.State.RemoveSnapshot.label</span><span class="sxs-lookup"><span data-stu-id="7fc48-192">Privilege.VirtualMachine.State.RemoveSnapshot.label</span></span>
</br>

  <span data-ttu-id="7fc48-193">Once you have selected the privileges, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-193">Once you have selected the privileges, click **OK**.</span></span> <span data-ttu-id="7fc48-194">The new role appears in the list on the Roles panel.</span><span class="sxs-lookup"><span data-stu-id="7fc48-194">The new role appears in the list on the Roles panel.</span></span>

### <a name="create-a-user-account-and-assign-permissions"></a><span data-ttu-id="7fc48-195">Create a user account and assign permissions</span><span class="sxs-lookup"><span data-stu-id="7fc48-195">Create a user account and assign permissions</span></span>

<span data-ttu-id="7fc48-196">Once you have defined the user role with privileges, create a user account.</span><span class="sxs-lookup"><span data-stu-id="7fc48-196">Once you have defined the user role with privileges, create a user account.</span></span> <span data-ttu-id="7fc48-197">As you create the user account, you assign it to a specific user role, which gives the account the associated privileges.</span><span class="sxs-lookup"><span data-stu-id="7fc48-197">As you create the user account, you assign it to a specific user role, which gives the account the associated privileges.</span></span> <span data-ttu-id="7fc48-198">The user account has a name and password, which provides the credentials used for authentication.</span><span class="sxs-lookup"><span data-stu-id="7fc48-198">The user account has a name and password, which provides the credentials used for authentication.</span></span>

1. <span data-ttu-id="7fc48-199">To create a new user account, on the VMware server, on the Navigator pane, click **Users and Groups**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-199">To create a new user account, on the VMware server, on the Navigator pane, click **Users and Groups**.</span></span>

  ![<span data-ttu-id="7fc48-200">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-200">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

  <span data-ttu-id="7fc48-201">The Users and Groups panel appears.</span><span class="sxs-lookup"><span data-stu-id="7fc48-201">The Users and Groups panel appears.</span></span>

  ![<span data-ttu-id="7fc48-202">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-202">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="7fc48-203">In the VMware Users and Groups panel, on the Users tab, click the Add users icon (the + symbol).</span><span class="sxs-lookup"><span data-stu-id="7fc48-203">In the VMware Users and Groups panel, on the Users tab, click the Add users icon (the + symbol).</span></span>

  <span data-ttu-id="7fc48-204">The New User dialog opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-204">The New User dialog opens.</span></span>

3. <span data-ttu-id="7fc48-205">The user account that you create, contains the user name and password pair that is used as credentials.</span><span class="sxs-lookup"><span data-stu-id="7fc48-205">The user account that you create, contains the user name and password pair that is used as credentials.</span></span> <span data-ttu-id="7fc48-206">In the New User dialog, fill out the fields and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-206">In the New User dialog, fill out the fields and click **OK**.</span></span>

  ![<span data-ttu-id="7fc48-207">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-207">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

  <span data-ttu-id="7fc48-208">The new user account appears in the list.</span><span class="sxs-lookup"><span data-stu-id="7fc48-208">The new user account appears in the list.</span></span>

4. <span data-ttu-id="7fc48-209">Now that you've created the user account, associate it with the user role (that has the desired permissions).</span><span class="sxs-lookup"><span data-stu-id="7fc48-209">Now that you've created the user account, associate it with the user role (that has the desired permissions).</span></span> <span data-ttu-id="7fc48-210">On the Navigator pane, click **Global Permissions**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-210">On the Navigator pane, click **Global Permissions**.</span></span> <span data-ttu-id="7fc48-211">On the Global Permissions panel, click the **Manage** tab and then click the Add icon (the + symbol).</span><span class="sxs-lookup"><span data-stu-id="7fc48-211">On the Global Permissions panel, click the **Manage** tab and then click the Add icon (the + symbol).</span></span>

  ![<span data-ttu-id="7fc48-212">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-212">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

  <span data-ttu-id="7fc48-213">The Global Permissions Root - Add Permission dialog opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-213">The Global Permissions Root - Add Permission dialog opens.</span></span>

5. <span data-ttu-id="7fc48-214">In the **Global Permission Root - Add Permission** dialog, click **Add** to choose the user or group.</span><span class="sxs-lookup"><span data-stu-id="7fc48-214">In the **Global Permission Root - Add Permission** dialog, click **Add** to choose the user or group.</span></span>

  ![<span data-ttu-id="7fc48-215">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-215">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

  <span data-ttu-id="7fc48-216">The Select Users/Groups dialog opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-216">The Select Users/Groups dialog opens.</span></span>

6. <span data-ttu-id="7fc48-217">In the **Select Users/Groups** dialog, select the user account that you created, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-217">In the **Select Users/Groups** dialog, select the user account that you created, and click **Add**.</span></span> <span data-ttu-id="7fc48-218">The selected user account appears in the Users field.</span><span class="sxs-lookup"><span data-stu-id="7fc48-218">The selected user account appears in the Users field.</span></span> <span data-ttu-id="7fc48-219">The user name appears in the Users field in the format *domain*`\`*user name*.</span><span class="sxs-lookup"><span data-stu-id="7fc48-219">The user name appears in the Users field in the format *domain*`\`*user name*.</span></span>

  ![<span data-ttu-id="7fc48-220">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-220">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

  <span data-ttu-id="7fc48-221">Click **OK** to add the selected users to the Add Permission dialog.</span><span class="sxs-lookup"><span data-stu-id="7fc48-221">Click **OK** to add the selected users to the Add Permission dialog.</span></span>

7. <span data-ttu-id="7fc48-222">Now that you've identified the user, assign the user to the role.</span><span class="sxs-lookup"><span data-stu-id="7fc48-222">Now that you've identified the user, assign the user to the role.</span></span> <span data-ttu-id="7fc48-223">In the Assigned Role area, from the drop-down menu, select the role and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-223">In the Assigned Role area, from the drop-down menu, select the role and click **OK**.</span></span>

  ![<span data-ttu-id="7fc48-224">certificate dialog with error</span><span class="sxs-lookup"><span data-stu-id="7fc48-224">certificate dialog with error</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="7fc48-225">On the Manage tab of the Global Permissions, the new user account and the associated role appear in the list.</span><span class="sxs-lookup"><span data-stu-id="7fc48-225">On the Manage tab of the Global Permissions, the new user account and the associated role appear in the list.</span></span>


### <a name="add-the-vmware-user-account-credentials-to-azure-backup-server"></a><span data-ttu-id="7fc48-226">Add the VMware user account credentials to Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="7fc48-226">Add the VMware user account credentials to Azure Backup Server</span></span>

<span data-ttu-id="7fc48-227">Before you add the VMware server to Azure Backup Server, be sure that you have installed [Update 1 for Microsoft Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="7fc48-227">Before you add the VMware server to Azure Backup Server, be sure that you have installed [Update 1 for Microsoft Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="7fc48-228">Click the following icon (located on the server desktop) to open the Azure Backup Server console.</span><span class="sxs-lookup"><span data-stu-id="7fc48-228">Click the following icon (located on the server desktop) to open the Azure Backup Server console.</span></span>

  ![Azure Backup Server icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/mabs-icon.png)

  <span data-ttu-id="7fc48-230">If you can't find the icon on the desktop, you can open the Azure Backup Server from the list of installed apps.</span><span class="sxs-lookup"><span data-stu-id="7fc48-230">If you can't find the icon on the desktop, you can open the Azure Backup Server from the list of installed apps.</span></span> <span data-ttu-id="7fc48-231">In the list of installed apps, the Azure Backup Server app is named Microsoft Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="7fc48-231">In the list of installed apps, the Azure Backup Server app is named Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="7fc48-232">In the Azure Backup Server console, click **Management**, then click **Production Servers**, and then in the tool ribbon, click **Manage VMware**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-232">In the Azure Backup Server console, click **Management**, then click **Production Servers**, and then in the tool ribbon, click **Manage VMware**.</span></span>

  ![MABS console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

  <span data-ttu-id="7fc48-234">The Manage Credentials dialog opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-234">The Manage Credentials dialog opens.</span></span>

  ![MABS manage credentials dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="7fc48-236">In the Manage Credentials dialog, click **Add** to open the Add Credentials dialog.</span><span class="sxs-lookup"><span data-stu-id="7fc48-236">In the Manage Credentials dialog, click **Add** to open the Add Credentials dialog.</span></span>

4. <span data-ttu-id="7fc48-237">In the Add Credentials dialog, type a name and description for the new credential.</span><span class="sxs-lookup"><span data-stu-id="7fc48-237">In the Add Credentials dialog, type a name and description for the new credential.</span></span> <span data-ttu-id="7fc48-238">The user name and password should be the same as you used when creating the user account in the VMware server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-238">The user name and password should be the same as you used when creating the user account in the VMware server.</span></span>

  ![MABS manage credentials dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/mabs-add-credential-dialog.png)

  <span data-ttu-id="7fc48-240">Click **Add** to add the new credential to Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-240">Click **Add** to add the new credential to Azure Backup Server.</span></span> <span data-ttu-id="7fc48-241">The new credential appears in the list in the Manage Credentials dialog.</span><span class="sxs-lookup"><span data-stu-id="7fc48-241">The new credential appears in the list in the Manage Credentials dialog.</span></span>
  <span data-ttu-id="7fc48-242">![MABS manage credentials dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)</span><span class="sxs-lookup"><span data-stu-id="7fc48-242">![MABS manage credentials dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)</span></span>

5. <span data-ttu-id="7fc48-243">Click the **X** in the upper-right hand corner to close the Manage Credentials dialog.</span><span class="sxs-lookup"><span data-stu-id="7fc48-243">Click the **X** in the upper-right hand corner to close the Manage Credentials dialog.</span></span>


## <a name="add-vmware-server-to-azure-backup-server"></a><span data-ttu-id="7fc48-244">Add VMware server to Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="7fc48-244">Add VMware server to Azure Backup Server</span></span>

<span data-ttu-id="7fc48-245">to open the Production Server Addition wizard</span><span class="sxs-lookup"><span data-stu-id="7fc48-245">to open the Production Server Addition wizard</span></span>

1. <span data-ttu-id="7fc48-246">In the Azure Backup Server console, click **Management**, click **Production Server**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-246">In the Azure Backup Server console, click **Management**, click **Production Server**, and then click **Add**.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

  <span data-ttu-id="7fc48-248">The Production Server Addition Wizard opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-248">The Production Server Addition Wizard opens.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="7fc48-250">On the Select Production Server type screen, select VMware Servers, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-250">On the Select Production Server type screen, select VMware Servers, and click **Next**.</span></span>

3. <span data-ttu-id="7fc48-251">In the Server Name/IP address, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-251">In the Server Name/IP address, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span></span> <span data-ttu-id="7fc48-252">You can enter the VMware name if all the ESXi servers are managed by the same Vcenter.</span><span class="sxs-lookup"><span data-stu-id="7fc48-252">You can enter the VMware name if all the ESXi servers are managed by the same Vcenter.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="7fc48-254">In the **SSL Port** dialog, enter the port used to communicate with the VMware server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-254">In the **SSL Port** dialog, enter the port used to communicate with the VMware server.</span></span> <span data-ttu-id="7fc48-255">Use port 443, which is the default port, unless you know that a different port is required.</span><span class="sxs-lookup"><span data-stu-id="7fc48-255">Use port 443, which is the default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="7fc48-256">In the **Specify Credential** dialog, you can create a new credential, or select an existing credential.</span><span class="sxs-lookup"><span data-stu-id="7fc48-256">In the **Specify Credential** dialog, you can create a new credential, or select an existing credential.</span></span> <span data-ttu-id="7fc48-257">In the previous section, you created a credential.</span><span class="sxs-lookup"><span data-stu-id="7fc48-257">In the previous section, you created a credential.</span></span> <span data-ttu-id="7fc48-258">Select this credential.</span><span class="sxs-lookup"><span data-stu-id="7fc48-258">Select this credential.</span></span>

  <span data-ttu-id="7fc48-259">If there isn't an available credential, or you need to create a new credential, click **Add New Credential**, create the new credential, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-259">If there isn't an available credential, or you need to create a new credential, click **Add New Credential**, create the new credential, and click **OK**.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/specify-new-cred.png)

6. <span data-ttu-id="7fc48-261">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and click \*\*Next to move to the next screen in the wizard.</span><span class="sxs-lookup"><span data-stu-id="7fc48-261">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and click \*\*Next to move to the next screen in the wizard.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="7fc48-263">In the **Tasks** screen, click **Add** to add the specified VMware server to the Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-263">In the **Tasks** screen, click **Add** to add the specified VMware server to the Azure Backup Server.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="7fc48-265">Since the VMware server backup is an agentless backup, adding the new server happens in seconds.</span><span class="sxs-lookup"><span data-stu-id="7fc48-265">Since the VMware server backup is an agentless backup, adding the new server happens in seconds.</span></span> <span data-ttu-id="7fc48-266">You can add multiple VMware servers to the Azure Backup Server by repeating the preceding steps in this section.</span><span class="sxs-lookup"><span data-stu-id="7fc48-266">You can add multiple VMware servers to the Azure Backup Server by repeating the preceding steps in this section.</span></span>

<span data-ttu-id="7fc48-267">Now that you have added a VMware server to the Azure Backup Server, the next step is to create a protection group.</span><span class="sxs-lookup"><span data-stu-id="7fc48-267">Now that you have added a VMware server to the Azure Backup Server, the next step is to create a protection group.</span></span> <span data-ttu-id="7fc48-268">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span><span class="sxs-lookup"><span data-stu-id="7fc48-268">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span></span> <span data-ttu-id="7fc48-269">The backup policy is the schedule for when backups are taken, and what is backed up.</span><span class="sxs-lookup"><span data-stu-id="7fc48-269">The backup policy is the schedule for when backups are taken, and what is backed up.</span></span>


## <a name="configure-a-protection-group-to-back-up-vmware-server"></a><span data-ttu-id="7fc48-270">Configure a protection group to back up VMware server</span><span class="sxs-lookup"><span data-stu-id="7fc48-270">Configure a protection group to back up VMware server</span></span>

<span data-ttu-id="7fc48-271">If you have not used System Center Data Protection Manager or Azure Backup Server before, see the topic, [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx), to prepare your hardware environment.</span><span class="sxs-lookup"><span data-stu-id="7fc48-271">If you have not used System Center Data Protection Manager or Azure Backup Server before, see the topic, [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx), to prepare your hardware environment.</span></span> <span data-ttu-id="7fc48-272">Once you've checked that you have proper storage, use the Create New Protection Group wizard to add the specific VMs.</span><span class="sxs-lookup"><span data-stu-id="7fc48-272">Once you've checked that you have proper storage, use the Create New Protection Group wizard to add the specific VMs.</span></span>

1. <span data-ttu-id="7fc48-273">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span><span class="sxs-lookup"><span data-stu-id="7fc48-273">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/open-protection-wizard.png)

  <span data-ttu-id="7fc48-275">The Create New Protection Group wizard opens.</span><span class="sxs-lookup"><span data-stu-id="7fc48-275">The Create New Protection Group wizard opens.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/protection-wizard.png)

  <span data-ttu-id="7fc48-277">Click **Next** to advance to the **Select protection group type** screen.</span><span class="sxs-lookup"><span data-stu-id="7fc48-277">Click **Next** to advance to the **Select protection group type** screen.</span></span>

2. <span data-ttu-id="7fc48-278">On the Select Protection Group Type screen, select **Servers** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-278">On the Select Protection Group Type screen, select **Servers** and click **Next**.</span></span>

3. <span data-ttu-id="7fc48-279">On the Select Group Members screen, you can see the available members and the members that have been selected.</span><span class="sxs-lookup"><span data-stu-id="7fc48-279">On the Select Group Members screen, you can see the available members and the members that have been selected.</span></span> <span data-ttu-id="7fc48-280">Select the members you want to protect and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-280">Select the members you want to protect and click **Next**.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/server-add-to-selected-members.png)

  <span data-ttu-id="7fc48-282">When selecting a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span><span class="sxs-lookup"><span data-stu-id="7fc48-282">When selecting a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="7fc48-283">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span><span class="sxs-lookup"><span data-stu-id="7fc48-283">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span></span> <span data-ttu-id="7fc48-284">You can exclude any folder or VM by de-selecting the checkbox.</span><span class="sxs-lookup"><span data-stu-id="7fc48-284">You can exclude any folder or VM by de-selecting the checkbox.</span></span>

  <span data-ttu-id="7fc48-285">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span><span class="sxs-lookup"><span data-stu-id="7fc48-285">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span></span> <span data-ttu-id="7fc48-286">That is, once a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span><span class="sxs-lookup"><span data-stu-id="7fc48-286">That is, once a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="7fc48-287">If you want to see which Azure Backup Server already protects a member, hover your mouse over the member, to see the name of the protecting server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-287">If you want to see which Azure Backup Server already protects a member, hover your mouse over the member, to see the name of the protecting server.</span></span>

4. <span data-ttu-id="7fc48-288">On the Select Data Protection Method screen, type a name for the protection group.</span><span class="sxs-lookup"><span data-stu-id="7fc48-288">On the Select Data Protection Method screen, type a name for the protection group.</span></span> <span data-ttu-id="7fc48-289">Then, for **Protection method**, select where you want to back up your data.</span><span class="sxs-lookup"><span data-stu-id="7fc48-289">Then, for **Protection method**, select where you want to back up your data.</span></span> <span data-ttu-id="7fc48-290">Data is backed up to disk for short-term protection.</span><span class="sxs-lookup"><span data-stu-id="7fc48-290">Data is backed up to disk for short-term protection.</span></span> <span data-ttu-id="7fc48-291">Data is backed up to the Cloud (Azure) for long-term protection.</span><span class="sxs-lookup"><span data-stu-id="7fc48-291">Data is backed up to the Cloud (Azure) for long-term protection.</span></span> <span data-ttu-id="7fc48-292">Click **Next** to proceed to the short-term protection range.</span><span class="sxs-lookup"><span data-stu-id="7fc48-292">Click **Next** to proceed to the short-term protection range.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="7fc48-294">On the Specify Short-Term Goals screen, for **Retention Range**, specify the number of days you want to retain recovery points *stored to disk*.</span><span class="sxs-lookup"><span data-stu-id="7fc48-294">On the Specify Short-Term Goals screen, for **Retention Range**, specify the number of days you want to retain recovery points *stored to disk*.</span></span> <span data-ttu-id="7fc48-295">If you want to change the time and days when recovery points are taken, click **Modify**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-295">If you want to change the time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="7fc48-296">The short-term recovery points are full backups.</span><span class="sxs-lookup"><span data-stu-id="7fc48-296">The short-term recovery points are full backups.</span></span> <span data-ttu-id="7fc48-297">They are not incremental backups.</span><span class="sxs-lookup"><span data-stu-id="7fc48-297">They are not incremental backups.</span></span> <span data-ttu-id="7fc48-298">When you are satisfied with the short-term goals, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-298">When you are satisfied with the short-term goals, click **Next**.</span></span>

  ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="7fc48-300">On the Review Disk Allocation screen, review and if necessary, modify the disk space for the VMs.</span><span class="sxs-lookup"><span data-stu-id="7fc48-300">On the Review Disk Allocation screen, review and if necessary, modify the disk space for the VMs.</span></span> <span data-ttu-id="7fc48-301">The recommended disk allocations are based on the retention range specified in the previous screen, the type of workload and the size of the protected data (identified in step 3).</span><span class="sxs-lookup"><span data-stu-id="7fc48-301">The recommended disk allocations are based on the retention range specified in the previous screen, the type of workload and the size of the protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="7fc48-302">Data size - Size of the data in the protection group.</span><span class="sxs-lookup"><span data-stu-id="7fc48-302">Data size - Size of the data in the protection group.</span></span>
  - <span data-ttu-id="7fc48-303">Disk space - The amount of disk space recommended for the protection group.</span><span class="sxs-lookup"><span data-stu-id="7fc48-303">Disk space - The amount of disk space recommended for the protection group.</span></span> <span data-ttu-id="7fc48-304">If you want to modify this setting, you should allocate total space that is slightly larger than the amount you estimate each data source will grow.</span><span class="sxs-lookup"><span data-stu-id="7fc48-304">If you want to modify this setting, you should allocate total space that is slightly larger than the amount you estimate each data source will grow.</span></span>
  - <span data-ttu-id="7fc48-305">Colocate data - If you enable colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span><span class="sxs-lookup"><span data-stu-id="7fc48-305">Colocate data - If you enable colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span></span> <span data-ttu-id="7fc48-306">Colocation isn't supported for all workloads.</span><span class="sxs-lookup"><span data-stu-id="7fc48-306">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="7fc48-307">Automatically grow - If you enable this setting, if data in the protected group outgrows the initial allocation, DPM tries to increase the disk size by 25%.</span><span class="sxs-lookup"><span data-stu-id="7fc48-307">Automatically grow - If you enable this setting, if data in the protected group outgrows the initial allocation, DPM tries to increase the disk size by 25%.</span></span>
  - <span data-ttu-id="7fc48-308">Storage pool details - Shows the current status of the storage pool, including total and remaining disk size.</span><span class="sxs-lookup"><span data-stu-id="7fc48-308">Storage pool details - Shows the current status of the storage pool, including total and remaining disk size.</span></span>

    ![Production Server Addition wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/review-disk-allocation.png)

  <span data-ttu-id="7fc48-310">When you have finished, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-310">When you have finished, click **Next**.</span></span>

7. <span data-ttu-id="7fc48-311">On the Choose Replica Creation Method screen, specify how you want to generate the initial copy, or replica, of the protected data on the Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-311">On the Choose Replica Creation Method screen, specify how you want to generate the initial copy, or replica, of the protected data on the Azure Backup Server.</span></span>

  <span data-ttu-id="7fc48-312">The default is **Automatically over the network** and **Now**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-312">The default is **Automatically over the network** and **Now**.</span></span> <span data-ttu-id="7fc48-313">If you use the default, it is recommended you specify an off-peak time.</span><span class="sxs-lookup"><span data-stu-id="7fc48-313">If you use the default, it is recommended you specify an off-peak time.</span></span> <span data-ttu-id="7fc48-314">Choose **Later** and specify a day and time.</span><span class="sxs-lookup"><span data-stu-id="7fc48-314">Choose **Later** and specify a day and time.</span></span>

  <span data-ttu-id="7fc48-315">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline using removable media.</span><span class="sxs-lookup"><span data-stu-id="7fc48-315">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline using removable media.</span></span>

  <span data-ttu-id="7fc48-316">Once you have made your choices, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-316">Once you have made your choices, click **Next**.</span></span>

  ![Create New Protection Group wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="7fc48-318">On the **Consistency Check Options** screen, select how and when to automate consistency checks.</span><span class="sxs-lookup"><span data-stu-id="7fc48-318">On the **Consistency Check Options** screen, select how and when to automate consistency checks.</span></span> <span data-ttu-id="7fc48-319">You can run consistency checks when replica data becomes inconsistent, or according to a set schedule.</span><span class="sxs-lookup"><span data-stu-id="7fc48-319">You can run consistency checks when replica data becomes inconsistent, or according to a set schedule.</span></span>

  <span data-ttu-id="7fc48-320">If you don't want to configure automatic consistency checking, you can run a manual check any time by right-clicking the protection group in the Protection area of the Azure Backup Server console, and selecting Perform Consistency Check.</span><span class="sxs-lookup"><span data-stu-id="7fc48-320">If you don't want to configure automatic consistency checking, you can run a manual check any time by right-clicking the protection group in the Protection area of the Azure Backup Server console, and selecting Perform Consistency Check.</span></span>

  <span data-ttu-id="7fc48-321">Click **Next** to move to the next screen.</span><span class="sxs-lookup"><span data-stu-id="7fc48-321">Click **Next** to move to the next screen.</span></span>

9. <span data-ttu-id="7fc48-322">On the **Specify Online Protection Data** screen, select the data source(s) that you want to protect.</span><span class="sxs-lookup"><span data-stu-id="7fc48-322">On the **Specify Online Protection Data** screen, select the data source(s) that you want to protect.</span></span> <span data-ttu-id="7fc48-323">You can select the members individually, or click **Select All** to choose all members.</span><span class="sxs-lookup"><span data-stu-id="7fc48-323">You can select the members individually, or click **Select All** to choose all members.</span></span> <span data-ttu-id="7fc48-324">Once you choose the members, click \**Next*.</span><span class="sxs-lookup"><span data-stu-id="7fc48-324">Once you choose the members, click \**Next*.</span></span>

  ![Create New Protection Group wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="7fc48-326">On the **Specify Online Backup Schedule** screen, specify the schedule for generating recovery points from the disk backup.</span><span class="sxs-lookup"><span data-stu-id="7fc48-326">On the **Specify Online Backup Schedule** screen, specify the schedule for generating recovery points from the disk backup.</span></span> <span data-ttu-id="7fc48-327">Once the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span><span class="sxs-lookup"><span data-stu-id="7fc48-327">Once the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span></span> <span data-ttu-id="7fc48-328">When you are satisfied with the online backup schedule, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-328">When you are satisfied with the online backup schedule, click **Next**.</span></span>

  ![Create New Protection Group wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="7fc48-330">On the Specify Online Retention Policy screen, indicate how long you want to retain the backup data in Azure.</span><span class="sxs-lookup"><span data-stu-id="7fc48-330">On the Specify Online Retention Policy screen, indicate how long you want to retain the backup data in Azure.</span></span> <span data-ttu-id="7fc48-331">After defining the policy, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7fc48-331">After defining the policy, click **Next**.</span></span>

  ![Create New Protection Group wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/retention-policy.png)

  <span data-ttu-id="7fc48-333">There is no time limit for how long you can keep data in Azure.</span><span class="sxs-lookup"><span data-stu-id="7fc48-333">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="7fc48-334">When storing recovery point data in Azure, the only limit is you cannot have more than 9999 recovery points per protected instance.</span><span class="sxs-lookup"><span data-stu-id="7fc48-334">When storing recovery point data in Azure, the only limit is you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="7fc48-335">In this example, the protected instance is the VMware server.</span><span class="sxs-lookup"><span data-stu-id="7fc48-335">In this example, the protected instance is the VMware server.</span></span>

12. <span data-ttu-id="7fc48-336">On the Summary screen, review the details for your protection group.</span><span class="sxs-lookup"><span data-stu-id="7fc48-336">On the Summary screen, review the details for your protection group.</span></span> <span data-ttu-id="7fc48-337">Note the group members and the settings.</span><span class="sxs-lookup"><span data-stu-id="7fc48-337">Note the group members and the settings.</span></span> <span data-ttu-id="7fc48-338">When you are satisfied with the settings, click \*\* Create Group\*\*.</span><span class="sxs-lookup"><span data-stu-id="7fc48-338">When you are satisfied with the settings, click \*\* Create Group\*\*.</span></span>

  ![Create New Protection Group wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="7fc48-340">Next steps</span><span class="sxs-lookup"><span data-stu-id="7fc48-340">Next steps</span></span>
<span data-ttu-id="7fc48-341">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to protect [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="7fc48-341">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to protect [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="7fc48-342">See [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md) for information on problems registering the agent, configuring the protection group, and problems with backup jobs.</span><span class="sxs-lookup"><span data-stu-id="7fc48-342">See [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md) for information on problems registering the agent, configuring the protection group, and problems with backup jobs.</span></span>













































