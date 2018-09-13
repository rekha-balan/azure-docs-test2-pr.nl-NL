---
title: Create a secure LDAP certificate for an Azure AD Domain Services manage domain | Microsoft Docs
description: Create a secure LDAP certificate for an Azure AD Domain Services manage domain
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/01/2017
ms.author: maheshu
ms.openlocfilehash: d34da3c7a32a9fd425e30880ba9bc808d9d2bab1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868045"
---
# <a name="create-a-pfx-file-with-the-secure-ldap-ldaps-certificate-for-a-managed-domain"></a><span data-ttu-id="ef993-103">Create a .PFX file with the secure LDAP (LDAPS) certificate for a managed domain</span><span class="sxs-lookup"><span data-stu-id="ef993-103">Create a .PFX file with the secure LDAP (LDAPS) certificate for a managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ef993-104">Before you begin</span><span class="sxs-lookup"><span data-stu-id="ef993-104">Before you begin</span></span>
<span data-ttu-id="ef993-105">Complete [Task 1: obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="ef993-105">Complete [Task 1: obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2-export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="ef993-106">Task 2: Export the secure LDAP certificate to a .PFX file</span><span class="sxs-lookup"><span data-stu-id="ef993-106">Task 2: Export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="ef993-107">Before you start this task, get the secure LDAP certificate from a public certification authority or create a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="ef993-107">Before you start this task, get the secure LDAP certificate from a public certification authority or create a self-signed certificate.</span></span>

<span data-ttu-id="ef993-108">To export the LDAPS certificate to a .PFX file:</span><span class="sxs-lookup"><span data-stu-id="ef993-108">To export the LDAPS certificate to a .PFX file:</span></span>

1. <span data-ttu-id="ef993-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ef993-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Launch the MMC console](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="ef993-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span><span class="sxs-lookup"><span data-stu-id="ef993-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="ef993-112">From the **File** menu, click **Add/Remove Snap-in...**.</span><span class="sxs-lookup"><span data-stu-id="ef993-112">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Add snap-in to MMC console](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="ef993-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span><span class="sxs-lookup"><span data-stu-id="ef993-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![Add certificates snap-in to MMC console](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="ef993-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ef993-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Add certificates snap-in for computer account](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="ef993-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="ef993-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![Add certificates snap-in - select computer](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="ef993-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span><span class="sxs-lookup"><span data-stu-id="ef993-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![Add certificates snap-in to MMC - done](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="ef993-122">In the MMC window, click to expand **Console Root**.</span><span class="sxs-lookup"><span data-stu-id="ef993-122">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="ef993-123">You should see the Certificates snap-in loaded.</span><span class="sxs-lookup"><span data-stu-id="ef993-123">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="ef993-124">Click **Certificates (Local Computer)** to expand.</span><span class="sxs-lookup"><span data-stu-id="ef993-124">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="ef993-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span><span class="sxs-lookup"><span data-stu-id="ef993-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![Open personal certificates store](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="ef993-127">You should see the self-signed certificate we created.</span><span class="sxs-lookup"><span data-stu-id="ef993-127">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="ef993-128">You can examine the properties of the certificate to verify the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span><span class="sxs-lookup"><span data-stu-id="ef993-128">You can examine the properties of the certificate to verify the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="ef993-129">Select the self-signed certificate and **right click**.</span><span class="sxs-lookup"><span data-stu-id="ef993-129">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="ef993-130">From the right-click menu, select **All Tasks** and select **Export...**.</span><span class="sxs-lookup"><span data-stu-id="ef993-130">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Export certificate](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="ef993-132">In the **Certificate Export Wizard**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ef993-132">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![Export certificate wizard](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="ef993-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ef993-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![Export certificate private key](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="ef993-136">You MUST export the private key along with the certificate.</span><span class="sxs-lookup"><span data-stu-id="ef993-136">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="ef993-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span><span class="sxs-lookup"><span data-stu-id="ef993-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >

13. <span data-ttu-id="ef993-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span><span class="sxs-lookup"><span data-stu-id="ef993-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![Export certificate file format](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="ef993-140">Only the .PFX file format is supported.</span><span class="sxs-lookup"><span data-stu-id="ef993-140">Only the .PFX file format is supported.</span></span> <span data-ttu-id="ef993-141">Do not export the certificate to the .CER file format.</span><span class="sxs-lookup"><span data-stu-id="ef993-141">Do not export the certificate to the .CER file format.</span></span>
    >
    >

14. <span data-ttu-id="ef993-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span><span class="sxs-lookup"><span data-stu-id="ef993-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="ef993-143">Remember this password since it will be needed in the next task.</span><span class="sxs-lookup"><span data-stu-id="ef993-143">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="ef993-144">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ef993-144">Click **Next**.</span></span>

    ![<span data-ttu-id="ef993-145">Password for certificate export</span><span class="sxs-lookup"><span data-stu-id="ef993-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="ef993-146">Make a note of this password.</span><span class="sxs-lookup"><span data-stu-id="ef993-146">Make a note of this password.</span></span> <span data-ttu-id="ef993-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="ef993-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >

15. <span data-ttu-id="ef993-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span><span class="sxs-lookup"><span data-stu-id="ef993-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![Path for certificate export](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="ef993-150">On the following page, click **Finish** to export the certificate to a PFX file.</span><span class="sxs-lookup"><span data-stu-id="ef993-150">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="ef993-151">You should see confirmation dialog when the certificate has been exported.</span><span class="sxs-lookup"><span data-stu-id="ef993-151">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![Export certificate done](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="ef993-153">Next step</span><span class="sxs-lookup"><span data-stu-id="ef993-153">Next step</span></span>
[<span data-ttu-id="ef993-154">Task 3: enable secure LDAP for the managed domain</span><span class="sxs-lookup"><span data-stu-id="ef993-154">Task 3: enable secure LDAP for the managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
