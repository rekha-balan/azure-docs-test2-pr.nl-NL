---
title: Back up VMware servers with Azure Backup Server
description: Use Azure Backup Server to back up a VMware vCenter/ESXi servers to Azure or disk. This article provides step=by-step instruction for backing up (or protecting) your VMware workloads.
services: backup
author: markgalioto
manager: carmonm
ms.service: backup
ms.topic: conceptual
ms.date: 07/24/2017
ms.author: adigan
ms.openlocfilehash: ce7b255359c076ddae642ed44f056e444b655e25
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804432"
---
# <a name="back-up-a-vmware-server-to-azure"></a><span data-ttu-id="973c8-104">Back up a VMware server to Azure</span><span class="sxs-lookup"><span data-stu-id="973c8-104">Back up a VMware server to Azure</span></span>

<span data-ttu-id="973c8-105">This article explains how to configure Azure Backup Server to help protect VMware server workloads.</span><span class="sxs-lookup"><span data-stu-id="973c8-105">This article explains how to configure Azure Backup Server to help protect VMware server workloads.</span></span> <span data-ttu-id="973c8-106">This article assumes you already have Azure Backup Server installed.</span><span class="sxs-lookup"><span data-stu-id="973c8-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="973c8-107">If you don't have Azure Backup Server installed, see [Prepare to back up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="973c8-107">If you don't have Azure Backup Server installed, see [Prepare to back up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="973c8-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span><span class="sxs-lookup"><span data-stu-id="973c8-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-to-the-vcenter-server"></a><span data-ttu-id="973c8-109">Create a secure connection to the vCenter Server</span><span class="sxs-lookup"><span data-stu-id="973c8-109">Create a secure connection to the vCenter Server</span></span>

<span data-ttu-id="973c8-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span><span class="sxs-lookup"><span data-stu-id="973c8-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="973c8-111">To turn on the secure communication, we recommend that you install the VMware Certificate Authority (CA) certificate on Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="973c8-111">To turn on the secure communication, we recommend that you install the VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="973c8-112">If you don't require secure communication, and would prefer to disable the HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="973c8-112">If you don't require secure communication, and would prefer to disable the HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="973c8-113">To create a secure connection between Azure Backup Server and the vCenter Server, import the trusted certificate on Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="973c8-113">To create a secure connection between Azure Backup Server and the vCenter Server, import the trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="973c8-114">Typically, you use a browser on the Azure Backup Server machine to connect to the vCenter Server via the vSphere Web Client.</span><span class="sxs-lookup"><span data-stu-id="973c8-114">Typically, you use a browser on the Azure Backup Server machine to connect to the vCenter Server via the vSphere Web Client.</span></span> <span data-ttu-id="973c8-115">The first time you use the Azure Backup Server browser to connect to the vCenter Server, the connection isn't secure.</span><span class="sxs-lookup"><span data-stu-id="973c8-115">The first time you use the Azure Backup Server browser to connect to the vCenter Server, the connection isn't secure.</span></span> <span data-ttu-id="973c8-116">The following image shows the unsecured connection.</span><span class="sxs-lookup"><span data-stu-id="973c8-116">The following image shows the unsecured connection.</span></span>

![Example of unsecured connection to VMware server](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="973c8-118">To fix this issue, and create a secure connection, download the trusted root CA certificates.</span><span class="sxs-lookup"><span data-stu-id="973c8-118">To fix this issue, and create a secure connection, download the trusted root CA certificates.</span></span>

1. <span data-ttu-id="973c8-119">In the browser on Azure Backup Server, enter the URL to the vSphere Web Client.</span><span class="sxs-lookup"><span data-stu-id="973c8-119">In the browser on Azure Backup Server, enter the URL to the vSphere Web Client.</span></span> <span data-ttu-id="973c8-120">The vSphere Web Client login page appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-120">The vSphere Web Client login page appears.</span></span>

    ![vSphere Web Client](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="973c8-122">At the bottom of the information for administrators and developers, locate the **Download trusted root CA certificates** link.</span><span class="sxs-lookup"><span data-stu-id="973c8-122">At the bottom of the information for administrators and developers, locate the **Download trusted root CA certificates** link.</span></span>

    ![Link to download the trusted root CA certificates](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="973c8-124">If you don't see the vSphere Web Client login page, check your browser's proxy settings.</span><span class="sxs-lookup"><span data-stu-id="973c8-124">If you don't see the vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="973c8-125">Click **Download trusted root CA certificates**.</span><span class="sxs-lookup"><span data-stu-id="973c8-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="973c8-126">The vCenter Server downloads a file to your local computer.</span><span class="sxs-lookup"><span data-stu-id="973c8-126">The vCenter Server downloads a file to your local computer.</span></span> <span data-ttu-id="973c8-127">The file's name is named **download**.</span><span class="sxs-lookup"><span data-stu-id="973c8-127">The file's name is named **download**.</span></span> <span data-ttu-id="973c8-128">Depending on your browser, you receive a message that asks whether to open or save the file.</span><span class="sxs-lookup"><span data-stu-id="973c8-128">Depending on your browser, you receive a message that asks whether to open or save the file.</span></span>

    ![download message when certificates are downloaded](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="973c8-130">Save the file to a location on Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="973c8-130">Save the file to a location on Azure Backup Server.</span></span> <span data-ttu-id="973c8-131">When you save the file, add the .zip file name extension.</span><span class="sxs-lookup"><span data-stu-id="973c8-131">When you save the file, add the .zip file name extension.</span></span>

    <span data-ttu-id="973c8-132">The file is a .zip file that contains the information about the certificates.</span><span class="sxs-lookup"><span data-stu-id="973c8-132">The file is a .zip file that contains the information about the certificates.</span></span> <span data-ttu-id="973c8-133">With the .zip extension, you can use the extraction tools.</span><span class="sxs-lookup"><span data-stu-id="973c8-133">With the .zip extension, you can use the extraction tools.</span></span>

4. <span data-ttu-id="973c8-134">Right-click **download.zip**, and then select **Extract All** to extract the contents.</span><span class="sxs-lookup"><span data-stu-id="973c8-134">Right-click **download.zip**, and then select **Extract All** to extract the contents.</span></span>

    <span data-ttu-id="973c8-135">The .zip file extracts its contents to a folder named **certs**.</span><span class="sxs-lookup"><span data-stu-id="973c8-135">The .zip file extracts its contents to a folder named **certs**.</span></span> <span data-ttu-id="973c8-136">Two types of files appear in the certs folder.</span><span class="sxs-lookup"><span data-stu-id="973c8-136">Two types of files appear in the certs folder.</span></span> <span data-ttu-id="973c8-137">The root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span><span class="sxs-lookup"><span data-stu-id="973c8-137">The root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="973c8-138">The CRL file has an extension that begins with a sequence like .r0 or .r1.</span><span class="sxs-lookup"><span data-stu-id="973c8-138">The CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="973c8-139">The CRL file is associated with a certificate.</span><span class="sxs-lookup"><span data-stu-id="973c8-139">The CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="973c8-140">Download file extracted locally</span><span class="sxs-lookup"><span data-stu-id="973c8-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="973c8-141">In the **certs** folder, right-click the root certificate file, and then click **Rename**.</span><span class="sxs-lookup"><span data-stu-id="973c8-141">In the **certs** folder, right-click the root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="973c8-142">Rename root certificate</span><span class="sxs-lookup"><span data-stu-id="973c8-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="973c8-143">Change the root certificate's extension to .crt.</span><span class="sxs-lookup"><span data-stu-id="973c8-143">Change the root certificate's extension to .crt.</span></span> <span data-ttu-id="973c8-144">When you're asked if you're sure you want to change the extension, click **Yes** or **OK**.</span><span class="sxs-lookup"><span data-stu-id="973c8-144">When you're asked if you're sure you want to change the extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="973c8-145">Otherwise, you change the file's intended function.</span><span class="sxs-lookup"><span data-stu-id="973c8-145">Otherwise, you change the file's intended function.</span></span> <span data-ttu-id="973c8-146">The icon for the file changes to an icon that represents a root certificate.</span><span class="sxs-lookup"><span data-stu-id="973c8-146">The icon for the file changes to an icon that represents a root certificate.</span></span>

6. <span data-ttu-id="973c8-147">Right-click the root certificate and from the pop-up menu, select **Install Certificate**.</span><span class="sxs-lookup"><span data-stu-id="973c8-147">Right-click the root certificate and from the pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="973c8-148">The **Certificate Import Wizard** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-148">The **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="973c8-149">In the **Certificate Import Wizard** dialog box, select **Local Machine** as the destination for the certificate, and then click **Next** to continue.</span><span class="sxs-lookup"><span data-stu-id="973c8-149">In the **Certificate Import Wizard** dialog box, select **Local Machine** as the destination for the certificate, and then click **Next** to continue.</span></span>

    ![<span data-ttu-id="973c8-150">Certificate storage destination options</span><span class="sxs-lookup"><span data-stu-id="973c8-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="973c8-151">If you're asked if you want to allow changes to the computer, click **Yes** or **OK**, to all the changes.</span><span class="sxs-lookup"><span data-stu-id="973c8-151">If you're asked if you want to allow changes to the computer, click **Yes** or **OK**, to all the changes.</span></span>

8. <span data-ttu-id="973c8-152">On the **Certificate Store** page, select **Place all certificates in the following store**, and then click **Browse** to choose the certificate store.</span><span class="sxs-lookup"><span data-stu-id="973c8-152">On the **Certificate Store** page, select **Place all certificates in the following store**, and then click **Browse** to choose the certificate store.</span></span>

    ![Place certificates in a specific storage spot](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="973c8-154">The **Select Certificate Store** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-154">The **Select Certificate Store** dialog box appears.</span></span>

    ![Certificate storage folder hierarchy](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="973c8-156">Select **Trusted Root Certification Authorities** as the destination folder for the certificates, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="973c8-156">Select **Trusted Root Certification Authorities** as the destination folder for the certificates, and then click **OK**.</span></span>

    ![Certificate destination folder](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="973c8-158">The **Trusted Root Certification Authorities** folder is confirmed as the certificate store.</span><span class="sxs-lookup"><span data-stu-id="973c8-158">The **Trusted Root Certification Authorities** folder is confirmed as the certificate store.</span></span> <span data-ttu-id="973c8-159">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="973c8-159">Click **Next**.</span></span>

    ![Certificate store folder](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="973c8-161">On the **Completing the Certificate Import Wizard** page, verify that the certificate is in the desired folder, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="973c8-161">On the **Completing the Certificate Import Wizard** page, verify that the certificate is in the desired folder, and then click **Finish**.</span></span>

    ![Verify certificate is in the proper folder](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="973c8-163">A dialog box appears, the successful certificate import is confirmed.</span><span class="sxs-lookup"><span data-stu-id="973c8-163">A dialog box appears, the successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="973c8-164">Sign in to the vCenter Server to confirm that your connection is secure.</span><span class="sxs-lookup"><span data-stu-id="973c8-164">Sign in to the vCenter Server to confirm that your connection is secure.</span></span>

  <span data-ttu-id="973c8-165">If the certificate import is not successful, and you cannot establish a secure connection, consult the VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="973c8-165">If the certificate import is not successful, and you cannot establish a secure connection, consult the VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="973c8-166">If you have secure boundaries within your organization, and don't want to turn on the HTTPS protocol, use the following procedure to disable the secure communications.</span><span class="sxs-lookup"><span data-stu-id="973c8-166">If you have secure boundaries within your organization, and don't want to turn on the HTTPS protocol, use the following procedure to disable the secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="973c8-167">Disable secure communication protocol</span><span class="sxs-lookup"><span data-stu-id="973c8-167">Disable secure communication protocol</span></span>

<span data-ttu-id="973c8-168">If your organization doesn't require the HTTPS protocol, use the following steps to disable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="973c8-168">If your organization doesn't require the HTTPS protocol, use the following steps to disable HTTPS.</span></span> <span data-ttu-id="973c8-169">To disable the default behavior, create a registry key that ignores the default behavior.</span><span class="sxs-lookup"><span data-stu-id="973c8-169">To disable the default behavior, create a registry key that ignores the default behavior.</span></span>

1. <span data-ttu-id="973c8-170">Copy and paste the following text into a .txt file.</span><span class="sxs-lookup"><span data-stu-id="973c8-170">Copy and paste the following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="973c8-171">Save the file to your Azure Backup Server computer.</span><span class="sxs-lookup"><span data-stu-id="973c8-171">Save the file to your Azure Backup Server computer.</span></span> <span data-ttu-id="973c8-172">For the file name, use DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="973c8-172">For the file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="973c8-173">Double-click the file to activate the registry entry.</span><span class="sxs-lookup"><span data-stu-id="973c8-173">Double-click the file to activate the registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-the-vcenter-server"></a><span data-ttu-id="973c8-174">Create a role and user account on the vCenter Server</span><span class="sxs-lookup"><span data-stu-id="973c8-174">Create a role and user account on the vCenter Server</span></span>

<span data-ttu-id="973c8-175">On the vCenter Server, a role is a predefined set of privileges.</span><span class="sxs-lookup"><span data-stu-id="973c8-175">On the vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="973c8-176">A vCenter Server administrator creates the roles.</span><span class="sxs-lookup"><span data-stu-id="973c8-176">A vCenter Server administrator creates the roles.</span></span> <span data-ttu-id="973c8-177">To assign permissions, the administrator pairs user accounts with a role.</span><span class="sxs-lookup"><span data-stu-id="973c8-177">To assign permissions, the administrator pairs user accounts with a role.</span></span> <span data-ttu-id="973c8-178">To establish the necessary user credentials to back up the vCenter Server computer, create a role with specific privileges, and then associate the user account with the role.</span><span class="sxs-lookup"><span data-stu-id="973c8-178">To establish the necessary user credentials to back up the vCenter Server computer, create a role with specific privileges, and then associate the user account with the role.</span></span>

<span data-ttu-id="973c8-179">Azure Backup Server uses a username and password to authenticate with the vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="973c8-179">Azure Backup Server uses a username and password to authenticate with the vCenter Server.</span></span> <span data-ttu-id="973c8-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span><span class="sxs-lookup"><span data-stu-id="973c8-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="973c8-181">To add a vCenter Server role and its privileges for a backup administrator:</span><span class="sxs-lookup"><span data-stu-id="973c8-181">To add a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="973c8-182">Sign in to the vCenter Server, and then in the vCenter Server **Navigator** panel, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="973c8-182">Sign in to the vCenter Server, and then in the vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Administration option in vCenter Server Navigator panel](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="973c8-184">In **Administration** select **Roles**, and then in the **Roles** panel click the add role icon (the + symbol).</span><span class="sxs-lookup"><span data-stu-id="973c8-184">In **Administration** select **Roles**, and then in the **Roles** panel click the add role icon (the + symbol).</span></span>

    ![Add role](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="973c8-186">The **Create Role** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-186">The **Create Role** dialog box appears.</span></span>

    ![Create role](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="973c8-188">In the **Create Role** dialog box, in the **Role name** box, enter *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="973c8-188">In the **Create Role** dialog box, in the **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="973c8-189">The role name can be whatever you like, but it should be recognizable for the role's purpose.</span><span class="sxs-lookup"><span data-stu-id="973c8-189">The role name can be whatever you like, but it should be recognizable for the role's purpose.</span></span>

4. <span data-ttu-id="973c8-190">Select the privileges for the appropriate version of vCenter, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="973c8-190">Select the privileges for the appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="973c8-191">The following table identifies the required privileges for vCenter 6.0 and vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="973c8-191">The following table identifies the required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="973c8-192">When you select the privileges, click the icon next to the parent label to expand the parent and view the child privileges.</span><span class="sxs-lookup"><span data-stu-id="973c8-192">When you select the privileges, click the icon next to the parent label to expand the parent and view the child privileges.</span></span> <span data-ttu-id="973c8-193">To select the VirtualMachine privileges, you need to go several levels into the parent child hierarchy.</span><span class="sxs-lookup"><span data-stu-id="973c8-193">To select the VirtualMachine privileges, you need to go several levels into the parent child hierarchy.</span></span> <span data-ttu-id="973c8-194">You don't need to select all child privileges within a parent privilege.</span><span class="sxs-lookup"><span data-stu-id="973c8-194">You don't need to select all child privileges within a parent privilege.</span></span>

  ![Parent child privilege hierarchy](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="973c8-196">After you click **OK**, the new role appears in the list on the Roles panel.</span><span class="sxs-lookup"><span data-stu-id="973c8-196">After you click **OK**, the new role appears in the list on the Roles panel.</span></span>

|<span data-ttu-id="973c8-197">Privileges for vCenter 6.0 and 6.5</span><span class="sxs-lookup"><span data-stu-id="973c8-197">Privileges for vCenter 6.0 and 6.5</span></span>| <span data-ttu-id="973c8-198">Privileges for vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="973c8-198">Privileges for vCenter 5.5</span></span>|
|----------------------------------|---------------------------|
|<span data-ttu-id="973c8-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="973c8-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="973c8-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="973c8-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="973c8-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="973c8-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="973c8-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="973c8-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="973c8-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="973c8-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="973c8-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="973c8-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="973c8-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="973c8-205">Network.Assign</span></span> |
|<span data-ttu-id="973c8-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="973c8-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="973c8-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="973c8-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="973c8-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="973c8-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="973c8-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="973c8-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="973c8-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="973c8-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="973c8-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="973c8-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="973c8-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="973c8-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="973c8-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="973c8-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="973c8-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="973c8-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="973c8-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="973c8-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="973c8-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="973c8-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="973c8-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="973c8-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="973c8-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="973c8-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="973c8-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="973c8-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="973c8-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="973c8-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="973c8-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="973c8-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="973c8-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="973c8-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="973c8-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="973c8-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="973c8-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="973c8-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="973c8-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="973c8-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="973c8-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="973c8-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="973c8-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="973c8-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="973c8-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="973c8-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="973c8-229">Create a vCenter Server user account and permissions</span><span class="sxs-lookup"><span data-stu-id="973c8-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="973c8-230">After the role with privileges is set up, create a user account.</span><span class="sxs-lookup"><span data-stu-id="973c8-230">After the role with privileges is set up, create a user account.</span></span> <span data-ttu-id="973c8-231">The user account has a name and password, which provides the credentials that are used for authentication.</span><span class="sxs-lookup"><span data-stu-id="973c8-231">The user account has a name and password, which provides the credentials that are used for authentication.</span></span>

1. <span data-ttu-id="973c8-232">To create a user account, in the vCenter Server **Navigator** panel, click **Users and Groups**.</span><span class="sxs-lookup"><span data-stu-id="973c8-232">To create a user account, in the vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Users and Groups option](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="973c8-234">The **vCenter Users and Groups** panel appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-234">The **vCenter Users and Groups** panel appears.</span></span>

    ![vCenter Users and Groups panel](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="973c8-236">In the **vCenter Users and Groups** panel, select the **Users** tab, and then click the add users icon (the + symbol).</span><span class="sxs-lookup"><span data-stu-id="973c8-236">In the **vCenter Users and Groups** panel, select the **Users** tab, and then click the add users icon (the + symbol).</span></span>

    <span data-ttu-id="973c8-237">The **New User** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-237">The **New User** dialog box appears.</span></span>

3. <span data-ttu-id="973c8-238">In the **New User** dialog box, add the user's information and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="973c8-238">In the **New User** dialog box, add the user's information and then click **OK**.</span></span> <span data-ttu-id="973c8-239">In this procedure, the username is BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="973c8-239">In this procedure, the username is BackupAdmin.</span></span>

    ![New User dialog box](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="973c8-241">The new user account appears in the list.</span><span class="sxs-lookup"><span data-stu-id="973c8-241">The new user account appears in the list.</span></span>

4. <span data-ttu-id="973c8-242">To associate the user account with the role, in the **Navigator** panel, click **Global Permissions**.</span><span class="sxs-lookup"><span data-stu-id="973c8-242">To associate the user account with the role, in the **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="973c8-243">In the **Global Permissions** panel, select the **Manage** tab, and then click the add icon (the + symbol).</span><span class="sxs-lookup"><span data-stu-id="973c8-243">In the **Global Permissions** panel, select the **Manage** tab, and then click the add icon (the + symbol).</span></span>

    ![Global Permissions panel](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="973c8-245">The **Global Permissions Root - Add Permission** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-245">The **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="973c8-246">In the **Global Permission Root - Add Permission** dialog box, click **Add** to choose the user or group.</span><span class="sxs-lookup"><span data-stu-id="973c8-246">In the **Global Permission Root - Add Permission** dialog box, click **Add** to choose the user or group.</span></span>

    ![Choose user or group](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="973c8-248">The **Select Users/Groups** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-248">The **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="973c8-249">In the **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="973c8-249">In the **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="973c8-250">In **Users**, the *domain\username* format is used for the user account.</span><span class="sxs-lookup"><span data-stu-id="973c8-250">In **Users**, the *domain\username* format is used for the user account.</span></span> <span data-ttu-id="973c8-251">If you want to use a different domain, choose it from the **Domain** list.</span><span class="sxs-lookup"><span data-stu-id="973c8-251">If you want to use a different domain, choose it from the **Domain** list.</span></span>

    ![Add BackupAdmin user](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="973c8-253">Click **OK** to add the selected users to the **Add Permission** dialog box.</span><span class="sxs-lookup"><span data-stu-id="973c8-253">Click **OK** to add the selected users to the **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="973c8-254">Now that you've identified the user, assign the user to the role.</span><span class="sxs-lookup"><span data-stu-id="973c8-254">Now that you've identified the user, assign the user to the role.</span></span> <span data-ttu-id="973c8-255">In **Assigned Role**, from the drop-down list, select **BackupAdminRole**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="973c8-255">In **Assigned Role**, from the drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Assign user to role](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="973c8-257">On the **Manage** tab in the **Global Permissions** panel, the new user account and the associated role appear in the list.</span><span class="sxs-lookup"><span data-stu-id="973c8-257">On the **Manage** tab in the **Global Permissions** panel, the new user account and the associated role appear in the list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="973c8-258">Establish vCenter Server credentials on Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="973c8-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="973c8-259">Before you add the VMware server to Azure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="973c8-259">Before you add the VMware server to Azure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="973c8-260">To open Azure Backup Server, double-click the icon on the Azure Backup Server desktop.</span><span class="sxs-lookup"><span data-stu-id="973c8-260">To open Azure Backup Server, double-click the icon on the Azure Backup Server desktop.</span></span>

    ![Azure Backup Server icon](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="973c8-262">If you can't find the icon on the desktop, open Azure Backup Server from the list of installed apps.</span><span class="sxs-lookup"><span data-stu-id="973c8-262">If you can't find the icon on the desktop, open Azure Backup Server from the list of installed apps.</span></span> <span data-ttu-id="973c8-263">The Azure Backup Server app name is called Microsoft Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="973c8-263">The Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="973c8-264">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then on the tool ribbon, click **Manage VMware**.</span><span class="sxs-lookup"><span data-stu-id="973c8-264">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then on the tool ribbon, click **Manage VMware**.</span></span>

    ![Azure Backup Server console](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="973c8-266">The **Manage Credentials** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-266">The **Manage Credentials** dialog box appears.</span></span>

    ![Azure Backup Server Manage Credentials dialog box](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="973c8-268">In the **Manage Credentials** dialog box, click **Add** to open the **Add Credential** dialog box.</span><span class="sxs-lookup"><span data-stu-id="973c8-268">In the **Manage Credentials** dialog box, click **Add** to open the **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="973c8-269">In the **Add Credential** dialog box, enter a name and a description for the new credential.</span><span class="sxs-lookup"><span data-stu-id="973c8-269">In the **Add Credential** dialog box, enter a name and a description for the new credential.</span></span> <span data-ttu-id="973c8-270">Then specify the username and password.</span><span class="sxs-lookup"><span data-stu-id="973c8-270">Then specify the username and password.</span></span> <span data-ttu-id="973c8-271">The name, *Contoso Vcenter credential* is used to identify the credential in the next procedure.</span><span class="sxs-lookup"><span data-stu-id="973c8-271">The name, *Contoso Vcenter credential* is used to identify the credential in the next procedure.</span></span> <span data-ttu-id="973c8-272">Use the same username and password that is used for the vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="973c8-272">Use the same username and password that is used for the vCenter Server.</span></span> <span data-ttu-id="973c8-273">If the vCenter Server and Azure Backup Server are not in the same domain, in **User name**, specify the domain.</span><span class="sxs-lookup"><span data-stu-id="973c8-273">If the vCenter Server and Azure Backup Server are not in the same domain, in **User name**, specify the domain.</span></span>

    ![Azure Backup Server Add Credential dialog box](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="973c8-275">Click **Add** to add the new credential to Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="973c8-275">Click **Add** to add the new credential to Azure Backup Server.</span></span> <span data-ttu-id="973c8-276">The new credential appears in the list in the **Manage Credentials** dialog box.</span><span class="sxs-lookup"><span data-stu-id="973c8-276">The new credential appears in the list in the **Manage Credentials** dialog box.</span></span>
    
    ![Azure Backup Server Manage Credentials dialog box](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="973c8-278">To close the **Manage Credentials** dialog box, click the **X** in the upper-right corner.</span><span class="sxs-lookup"><span data-stu-id="973c8-278">To close the **Manage Credentials** dialog box, click the **X** in the upper-right corner.</span></span>


## <a name="add-the-vcenter-server-to-azure-backup-server"></a><span data-ttu-id="973c8-279">Add the vCenter Server to Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="973c8-279">Add the vCenter Server to Azure Backup Server</span></span>

<span data-ttu-id="973c8-280">Production Server Addition Wizard is used to add the vCenter Server to Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="973c8-280">Production Server Addition Wizard is used to add the vCenter Server to Azure Backup Server.</span></span>

<span data-ttu-id="973c8-281">To open Production Server Addition Wizard, complete the following procedure:</span><span class="sxs-lookup"><span data-stu-id="973c8-281">To open Production Server Addition Wizard, complete the following procedure:</span></span>

1. <span data-ttu-id="973c8-282">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="973c8-282">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Open Production Server Addition Wizard](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="973c8-284">The **Production Server Addition Wizard** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-284">The **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Production Server Addition Wizard](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="973c8-286">On the **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="973c8-286">On the **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="973c8-287">In **Server Name/IP Address**, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span><span class="sxs-lookup"><span data-stu-id="973c8-287">In **Server Name/IP Address**, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span></span> <span data-ttu-id="973c8-288">If all the ESXi servers are managed by the same vCenter, you can use the vCenter name.</span><span class="sxs-lookup"><span data-stu-id="973c8-288">If all the ESXi servers are managed by the same vCenter, you can use the vCenter name.</span></span>

    ![Specify VMware server FQDN or IP address](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="973c8-290">In **SSL Port**, enter the port that is used to communicate with the VMware server.</span><span class="sxs-lookup"><span data-stu-id="973c8-290">In **SSL Port**, enter the port that is used to communicate with the VMware server.</span></span> <span data-ttu-id="973c8-291">Use port 443, which is the default port, unless you know that a different port is required.</span><span class="sxs-lookup"><span data-stu-id="973c8-291">Use port 443, which is the default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="973c8-292">In **Specify Credential**, select the credential that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="973c8-292">In **Specify Credential**, select the credential that you created earlier.</span></span>

    ![Specify credential](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="973c8-294">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and then click **Next** to move to the next page in the wizard.</span><span class="sxs-lookup"><span data-stu-id="973c8-294">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and then click **Next** to move to the next page in the wizard.</span></span>

    ![Add VMWare server and credential](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="973c8-296">In the **Summary** page, click **Add** to add the specified VMware server to Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="973c8-296">In the **Summary** page, click **Add** to add the specified VMware server to Azure Backup Server.</span></span>

    ![Add VMware server to Azure Backup Server](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="973c8-298">The VMware server backup is an agentless backup, and the new server is added immediately.</span><span class="sxs-lookup"><span data-stu-id="973c8-298">The VMware server backup is an agentless backup, and the new server is added immediately.</span></span> <span data-ttu-id="973c8-299">The **Finish** page shows you the results.</span><span class="sxs-lookup"><span data-stu-id="973c8-299">The **Finish** page shows you the results.</span></span>

  ![Finish page](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="973c8-301">To add multiple instances of vCenter Server to Azure Backup Server, repeat the previous steps in this section.</span><span class="sxs-lookup"><span data-stu-id="973c8-301">To add multiple instances of vCenter Server to Azure Backup Server, repeat the previous steps in this section.</span></span>

<span data-ttu-id="973c8-302">After you add the vCenter Server to Azure Backup Server, the next step is to create a protection group.</span><span class="sxs-lookup"><span data-stu-id="973c8-302">After you add the vCenter Server to Azure Backup Server, the next step is to create a protection group.</span></span> <span data-ttu-id="973c8-303">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span><span class="sxs-lookup"><span data-stu-id="973c8-303">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span></span> <span data-ttu-id="973c8-304">The backup policy is the schedule for when backups occur, and what is backed up.</span><span class="sxs-lookup"><span data-stu-id="973c8-304">The backup policy is the schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="973c8-305">Configure a protection group</span><span class="sxs-lookup"><span data-stu-id="973c8-305">Configure a protection group</span></span>

<span data-ttu-id="973c8-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) to prepare your hardware environment.</span><span class="sxs-lookup"><span data-stu-id="973c8-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) to prepare your hardware environment.</span></span> <span data-ttu-id="973c8-307">After you check that you have proper storage, use the Create New Protection Group wizard to add VMware virtual machines.</span><span class="sxs-lookup"><span data-stu-id="973c8-307">After you check that you have proper storage, use the Create New Protection Group wizard to add VMware virtual machines.</span></span>

1. <span data-ttu-id="973c8-308">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span><span class="sxs-lookup"><span data-stu-id="973c8-308">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span></span>

    ![Open the Create New Protection Group wizard](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="973c8-310">The **Create New Protection Group** wizard dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-310">The **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Create New Protection Group wizard dialog box](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="973c8-312">Click **Next** to advance to the **Select protection group type** page.</span><span class="sxs-lookup"><span data-stu-id="973c8-312">Click **Next** to advance to the **Select protection group type** page.</span></span>

2. <span data-ttu-id="973c8-313">On the **Select Protection group type** page, select **Servers** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="973c8-313">On the **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="973c8-314">The **Select group members** page appears.</span><span class="sxs-lookup"><span data-stu-id="973c8-314">The **Select group members** page appears.</span></span>

3. <span data-ttu-id="973c8-315">On the **Select group members** page, the available members and the selected members appear.</span><span class="sxs-lookup"><span data-stu-id="973c8-315">On the **Select group members** page, the available members and the selected members appear.</span></span> <span data-ttu-id="973c8-316">Select the members that you want to protect, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="973c8-316">Select the members that you want to protect, and then click **Next**.</span></span>

    ![Select group members](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="973c8-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span><span class="sxs-lookup"><span data-stu-id="973c8-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="973c8-319">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span><span class="sxs-lookup"><span data-stu-id="973c8-319">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span></span> <span data-ttu-id="973c8-320">To remove a folder or VM, clear the check box.</span><span class="sxs-lookup"><span data-stu-id="973c8-320">To remove a folder or VM, clear the check box.</span></span>

    <span data-ttu-id="973c8-321">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span><span class="sxs-lookup"><span data-stu-id="973c8-321">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span></span> <span data-ttu-id="973c8-322">That is, after a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span><span class="sxs-lookup"><span data-stu-id="973c8-322">That is, after a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="973c8-323">If you want to see which Azure Backup Server instance already protects a member, point to the member to see the name of the protecting server.</span><span class="sxs-lookup"><span data-stu-id="973c8-323">If you want to see which Azure Backup Server instance already protects a member, point to the member to see the name of the protecting server.</span></span>

4. <span data-ttu-id="973c8-324">On the **Select Data Protection Method** page, enter a name for the protection group.</span><span class="sxs-lookup"><span data-stu-id="973c8-324">On the **Select Data Protection Method** page, enter a name for the protection group.</span></span> <span data-ttu-id="973c8-325">Short-term protection (to disk) and online protection are selected.</span><span class="sxs-lookup"><span data-stu-id="973c8-325">Short-term protection (to disk) and online protection are selected.</span></span> <span data-ttu-id="973c8-326">If you want to use online protection (to Azure), you must use short-term protection to disk.</span><span class="sxs-lookup"><span data-stu-id="973c8-326">If you want to use online protection (to Azure), you must use short-term protection to disk.</span></span> <span data-ttu-id="973c8-327">Click **Next** to proceed to the short-term protection range.</span><span class="sxs-lookup"><span data-stu-id="973c8-327">Click **Next** to proceed to the short-term protection range.</span></span>

    ![Select data protection method](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="973c8-329">On the **Specify Short-Term Goals** page, for **Retention Range**, specify the number of days that you want to retain recovery points that are *stored to disk*.</span><span class="sxs-lookup"><span data-stu-id="973c8-329">On the **Specify Short-Term Goals** page, for **Retention Range**, specify the number of days that you want to retain recovery points that are *stored to disk*.</span></span> <span data-ttu-id="973c8-330">If you want to change the time and days when recovery points are taken, click **Modify**.</span><span class="sxs-lookup"><span data-stu-id="973c8-330">If you want to change the time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="973c8-331">The short-term recovery points are full backups.</span><span class="sxs-lookup"><span data-stu-id="973c8-331">The short-term recovery points are full backups.</span></span> <span data-ttu-id="973c8-332">They are not incremental backups.</span><span class="sxs-lookup"><span data-stu-id="973c8-332">They are not incremental backups.</span></span> <span data-ttu-id="973c8-333">When you are satisfied with the short-term goals, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="973c8-333">When you are satisfied with the short-term goals, click **Next**.</span></span>

    ![Specify short-term goals](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="973c8-335">On the **Review Disk Allocation** page, review and if necessary, modify the disk space for the VMs.</span><span class="sxs-lookup"><span data-stu-id="973c8-335">On the **Review Disk Allocation** page, review and if necessary, modify the disk space for the VMs.</span></span> <span data-ttu-id="973c8-336">The recommended disk allocations are based on the retention range that is specified in the **Specify Short-Term Goals** page, the type of workload, and the size of the protected data (identified in step 3).</span><span class="sxs-lookup"><span data-stu-id="973c8-336">The recommended disk allocations are based on the retention range that is specified in the **Specify Short-Term Goals** page, the type of workload, and the size of the protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="973c8-337">**Data size:** Size of the data in the protection group.</span><span class="sxs-lookup"><span data-stu-id="973c8-337">**Data size:** Size of the data in the protection group.</span></span>
  - <span data-ttu-id="973c8-338">**Disk space:** The recommended amount of disk space for the protection group.</span><span class="sxs-lookup"><span data-stu-id="973c8-338">**Disk space:** The recommended amount of disk space for the protection group.</span></span> <span data-ttu-id="973c8-339">If you want to modify this setting, you should allocate total space that is slightly larger than the amount that you estimate each data source grows.</span><span class="sxs-lookup"><span data-stu-id="973c8-339">If you want to modify this setting, you should allocate total space that is slightly larger than the amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="973c8-340">**Colocate data:** If you turn on colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span><span class="sxs-lookup"><span data-stu-id="973c8-340">**Colocate data:** If you turn on colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span></span> <span data-ttu-id="973c8-341">Colocation isn't supported for all workloads.</span><span class="sxs-lookup"><span data-stu-id="973c8-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="973c8-342">**Automatically grow:** If you turn on this setting, if data in the protected group outgrows the initial allocation, System Center Data Protection Manager tries to increase the disk size by 25 percent.</span><span class="sxs-lookup"><span data-stu-id="973c8-342">**Automatically grow:** If you turn on this setting, if data in the protected group outgrows the initial allocation, System Center Data Protection Manager tries to increase the disk size by 25 percent.</span></span>
  - <span data-ttu-id="973c8-343">**Storage pool details:** Shows the status of the storage pool, including total and remaining disk size.</span><span class="sxs-lookup"><span data-stu-id="973c8-343">**Storage pool details:** Shows the status of the storage pool, including total and remaining disk size.</span></span>

    ![Review disk allocation](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="973c8-345">When you are satisfied with the space allocation, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="973c8-345">When you are satisfied with the space allocation, click **Next**.</span></span>

7. <span data-ttu-id="973c8-346">On the **Choose Replica Creation Method** page, specify how you want to generate the initial copy, or replica, of the protected data on Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="973c8-346">On the **Choose Replica Creation Method** page, specify how you want to generate the initial copy, or replica, of the protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="973c8-347">The default is **Automatically over the network** and **Now**.</span><span class="sxs-lookup"><span data-stu-id="973c8-347">The default is **Automatically over the network** and **Now**.</span></span> <span data-ttu-id="973c8-348">If you use the default, we recommend that you specify an off-peak time.</span><span class="sxs-lookup"><span data-stu-id="973c8-348">If you use the default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="973c8-349">Choose **Later** and specify a day and time.</span><span class="sxs-lookup"><span data-stu-id="973c8-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="973c8-350">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline by using removable media.</span><span class="sxs-lookup"><span data-stu-id="973c8-350">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline by using removable media.</span></span>

    <span data-ttu-id="973c8-351">After you have made your choices, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="973c8-351">After you have made your choices, click **Next**.</span></span>

    ![Choose replica creation method](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="973c8-353">On the **Consistency Check Options** page, select how and when to automate the consistency checks.</span><span class="sxs-lookup"><span data-stu-id="973c8-353">On the **Consistency Check Options** page, select how and when to automate the consistency checks.</span></span> <span data-ttu-id="973c8-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span><span class="sxs-lookup"><span data-stu-id="973c8-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="973c8-355">If you don't want to configure automatic consistency checks, you can run a manual check.</span><span class="sxs-lookup"><span data-stu-id="973c8-355">If you don't want to configure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="973c8-356">In the protection area of the Azure Backup Server console, right-click the protection group and then select **Perform Consistency Check**.</span><span class="sxs-lookup"><span data-stu-id="973c8-356">In the protection area of the Azure Backup Server console, right-click the protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="973c8-357">Click **Next** to move to the next page.</span><span class="sxs-lookup"><span data-stu-id="973c8-357">Click **Next** to move to the next page.</span></span>

9. <span data-ttu-id="973c8-358">On the **Specify Online Protection Data** page, select one or more data sources that you want to protect.</span><span class="sxs-lookup"><span data-stu-id="973c8-358">On the **Specify Online Protection Data** page, select one or more data sources that you want to protect.</span></span> <span data-ttu-id="973c8-359">You can select the members individually, or click **Select All** to choose all members.</span><span class="sxs-lookup"><span data-stu-id="973c8-359">You can select the members individually, or click **Select All** to choose all members.</span></span> <span data-ttu-id="973c8-360">After you choose the members, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="973c8-360">After you choose the members, click **Next**.</span></span>

    ![Specify online protection data](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="973c8-362">On the **Specify Online Backup Schedule** page, specify the schedule to generate recovery points from the disk backup.</span><span class="sxs-lookup"><span data-stu-id="973c8-362">On the **Specify Online Backup Schedule** page, specify the schedule to generate recovery points from the disk backup.</span></span> <span data-ttu-id="973c8-363">After the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span><span class="sxs-lookup"><span data-stu-id="973c8-363">After the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span></span> <span data-ttu-id="973c8-364">When you are satisfied with the online backup schedule, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="973c8-364">When you are satisfied with the online backup schedule, click **Next**.</span></span>

    ![Specify online backup schedule](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="973c8-366">On the **Specify Online Retention Policy** page, indicate how long you want to retain the backup data in Azure.</span><span class="sxs-lookup"><span data-stu-id="973c8-366">On the **Specify Online Retention Policy** page, indicate how long you want to retain the backup data in Azure.</span></span> <span data-ttu-id="973c8-367">After the policy is defined, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="973c8-367">After the policy is defined, click **Next**.</span></span>

    ![Specify online retention policy](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="973c8-369">There is no time limit for how long you can keep data in Azure.</span><span class="sxs-lookup"><span data-stu-id="973c8-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="973c8-370">When you store recovery point data in Azure, the only limit is that you cannot have more than 9999 recovery points per protected instance.</span><span class="sxs-lookup"><span data-stu-id="973c8-370">When you store recovery point data in Azure, the only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="973c8-371">In this example, the protected instance is the VMware server.</span><span class="sxs-lookup"><span data-stu-id="973c8-371">In this example, the protected instance is the VMware server.</span></span>

12. <span data-ttu-id="973c8-372">On the **Summary** page, review the details for your protection group members and settings, and then click **Create Group**.</span><span class="sxs-lookup"><span data-stu-id="973c8-372">On the **Summary** page, review the details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Protection group member and setting summary](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="973c8-374">Next steps</span><span class="sxs-lookup"><span data-stu-id="973c8-374">Next steps</span></span>
<span data-ttu-id="973c8-375">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to help protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="973c8-375">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to help protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="973c8-376">For information on problems with registering the agent, configuring the protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="973c8-376">For information on problems with registering the agent, configuring the protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
