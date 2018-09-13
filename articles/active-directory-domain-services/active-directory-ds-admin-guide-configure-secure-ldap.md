---
title: Configure Secure LDAP (LDAPS) in Azure AD Domain Services | Microsoft Docs
description: Configure Secure LDAP (LDAPS) for an Azure AD Domain Services managed domain
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 8585edb8c926a05004e6121d8cf9dfddd3b84458
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554303"
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="4cc6a-103">Configure Secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="4cc6a-103">Configure Secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="4cc6a-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="4cc6a-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4cc6a-106">Before you begin</span><span class="sxs-lookup"><span data-stu-id="4cc6a-106">Before you begin</span></span>
<span data-ttu-id="4cc6a-107">To perform the tasks listed in this article, you need:</span><span class="sxs-lookup"><span data-stu-id="4cc6a-107">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="4cc6a-108">A valid **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="4cc6a-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="4cc6a-110">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-110">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="4cc6a-111">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4cc6a-111">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="4cc6a-112">A **certificate to be used to enable secure LDAP**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-112">A **certificate to be used to enable secure LDAP**.</span></span>

   * <span data-ttu-id="4cc6a-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="4cc6a-114">This configuration option is more secure.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="4cc6a-115">Alternately, you may also choose to [create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-115">Alternately, you may also choose to [create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-the-secure-ldap-certificate"></a><span data-ttu-id="4cc6a-116">Requirements for the secure LDAP certificate</span><span class="sxs-lookup"><span data-stu-id="4cc6a-116">Requirements for the secure LDAP certificate</span></span>
<span data-ttu-id="4cc6a-117">Acquire a valid certificate per the following guidelines, before you enable secure LDAP.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-117">Acquire a valid certificate per the following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="4cc6a-118">You encounter failures if you try to enable secure LDAP for your managed domain with an invalid/incorrect certificate.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-118">You encounter failures if you try to enable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="4cc6a-119">**Trusted issuer** - The certificate must be issued by an authority trusted by computers that need to connect to the domain using secure LDAP.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-119">**Trusted issuer** - The certificate must be issued by an authority trusted by computers that need to connect to the domain using secure LDAP.</span></span> <span data-ttu-id="4cc6a-120">This authority may be a public certification authority trusted by these computers.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="4cc6a-121">**Lifetime** - The certificate must be valid for at least the next 3-6 months.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-121">**Lifetime** - The certificate must be valid for at least the next 3-6 months.</span></span> <span data-ttu-id="4cc6a-122">Secure LDAP access to your managed domain is disrupted when the certificate expires.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-122">Secure LDAP access to your managed domain is disrupted when the certificate expires.</span></span>
3. <span data-ttu-id="4cc6a-123">**Subject name** - The subject name on the certificate must be a wildcard for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-123">**Subject name** - The subject name on the certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="4cc6a-124">For instance, if your domain is named 'contoso100.com', the certificate's subject name must be '\*.contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-124">For instance, if your domain is named 'contoso100.com', the certificate's subject name must be '\*.contoso100.com'.</span></span> <span data-ttu-id="4cc6a-125">Set the DNS name (subject alternate name) to this wildcard name.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-125">Set the DNS name (subject alternate name) to this wildcard name.</span></span>
4. <span data-ttu-id="4cc6a-126">**Key usage** - The certificate must be configured for the following uses - Digital signatures and key encipherment.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-126">**Key usage** - The certificate must be configured for the following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="4cc6a-127">**Certificate purpose** - The certificate must be valid for SSL server authentication.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-127">**Certificate purpose** - The certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="4cc6a-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not currently support using secure LDAP certificates issued by your organization's enterprise certification authority.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not currently support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="4cc6a-129">This restriction is because the service does not trust your enterprise CA as a root certification authority.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-129">This restriction is because the service does not trust your enterprise CA as a root certification authority.</span></span> <span data-ttu-id="4cc6a-130">We expect to add support for enterprise CAs in the future.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-130">We expect to add support for enterprise CAs in the future.</span></span> <span data-ttu-id="4cc6a-131">If you absolutely must use certificates issued by your enterprise CA, [contact us](active-directory-ds-contact-us.md) for assistance.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-131">If you absolutely must use certificates issued by your enterprise CA, [contact us](active-directory-ds-contact-us.md) for assistance.</span></span>
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="4cc6a-132">Task 1 - Obtain a certificate for secure LDAP</span><span class="sxs-lookup"><span data-stu-id="4cc6a-132">Task 1 - Obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="4cc6a-133">The first task involves obtaining a certificate used for secure LDAP access to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-133">The first task involves obtaining a certificate used for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="4cc6a-134">You have two options:</span><span class="sxs-lookup"><span data-stu-id="4cc6a-134">You have two options:</span></span>

* <span data-ttu-id="4cc6a-135">Obtain a certificate from a certification authority.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-135">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="4cc6a-136">The authority may be a public certification authority.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-136">The authority may be a public certification authority.</span></span>
* <span data-ttu-id="4cc6a-137">Create a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-137">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="4cc6a-138">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span><span class="sxs-lookup"><span data-stu-id="4cc6a-138">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="4cc6a-139">If your organization obtains its certificates from a public certification authority, you need to obtain the secure LDAP certificate from that public certification authority.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-139">If your organization obtains its certificates from a public certification authority, you need to obtain the secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="4cc6a-140">When requesting a certificate, ensure that you follow the requirements outlined in [Requirement for the secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="4cc6a-140">When requesting a certificate, ensure that you follow the requirements outlined in [Requirement for the secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="4cc6a-141">Client computers that need to connect to the managed domain using secure LDAP must trust the issuer of the secure LDAP certificate.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-141">Client computers that need to connect to the managed domain using secure LDAP must trust the issuer of the secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="4cc6a-142">Option B - Create a self-signed certificate for secure LDAP</span><span class="sxs-lookup"><span data-stu-id="4cc6a-142">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="4cc6a-143">If you do not expect to use a certificate from a public certification authority, you may choose to create a self-signed certificate for secure LDAP.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-143">If you do not expect to use a certificate from a public certification authority, you may choose to create a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="4cc6a-144">**Create a self-signed certificate using PowerShell**</span><span class="sxs-lookup"><span data-stu-id="4cc6a-144">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="4cc6a-145">On your Windows computer, open a new PowerShell window as **Administrator** and type the following commands, to create a new self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-145">On your Windows computer, open a new PowerShell window as **Administrator** and type the following commands, to create a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="4cc6a-146">In the preceding sample, replace 'contoso100.com' with the DNS domain name of your Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-146">In the preceding sample, replace 'contoso100.com' with the DNS domain name of your Azure AD Domain Services managed domain.</span></span>

![Select Azure AD Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="4cc6a-148">The newly created self-signed certificate is placed in the local machine's certificate store.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-148">The newly created self-signed certificate is placed in the local machine's certificate store.</span></span>

## <a name="task-2---export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="4cc6a-149">Task 2 - Export the secure LDAP certificate to a .PFX file</span><span class="sxs-lookup"><span data-stu-id="4cc6a-149">Task 2 - Export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="4cc6a-150">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-150">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="4cc6a-151">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-151">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span></span>

1. <span data-ttu-id="4cc6a-152">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-152">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Launch the MMC console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="4cc6a-154">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-154">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="4cc6a-155">From the **File** menu, click **Add/Remove Snap-in...**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-155">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Add snap-in to MMC console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="4cc6a-157">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-157">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![Add certificates snap-in to MMC console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="4cc6a-159">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-159">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Add certificates snap-in for computer account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="4cc6a-161">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-161">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![Add certificates snap-in - select computer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="4cc6a-163">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-163">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![Add certificates snap-in to MMC - done](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="4cc6a-165">In the MMC window, click to expand **Console Root**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-165">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="4cc6a-166">You should see the Certificates snap-in loaded.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-166">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="4cc6a-167">Click **Certificates (Local Computer)** to expand.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-167">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="4cc6a-168">Click to expand the **Personal** node, followed by the **Certificates** node.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-168">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![Open personal certificates store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="4cc6a-170">You should see the self-signed certificate we created.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-170">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="4cc6a-171">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-171">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="4cc6a-172">Select the self-signed certificate and **right click**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-172">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="4cc6a-173">From the right-click menu, select **All Tasks** and select **Export...**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-173">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Export certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="4cc6a-175">In the **Certificate Export Wizard**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-175">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![Export certificate wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="4cc6a-177">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-177">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![Export certificate private key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="4cc6a-179">You MUST export the private key along with the certificate.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-179">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="4cc6a-180">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-180">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="4cc6a-181">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-181">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![Export certificate file format](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="4cc6a-183">Only the .PFX file format is supported.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-183">Only the .PFX file format is supported.</span></span> <span data-ttu-id="4cc6a-184">Do not export the certificate to the .CER file format.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-184">Do not export the certificate to the .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="4cc6a-185">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-185">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="4cc6a-186">Remember this password since it will be needed in the next task.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-186">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="4cc6a-187">Click **Next** to proceed.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-187">Click **Next** to proceed.</span></span>

    ![<span data-ttu-id="4cc6a-188">Password for certificate export</span><span class="sxs-lookup"><span data-stu-id="4cc6a-188">Password for certificate export</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="4cc6a-189">Make a note of this password.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-189">Make a note of this password.</span></span> <span data-ttu-id="4cc6a-190">You need it while enabling secure LDAP for this managed domain in [Task 3 - Enable secure LDAP for the managed domain](#task-3---enable-secure-ldap-for-the-managed-domain)</span><span class="sxs-lookup"><span data-stu-id="4cc6a-190">You need it while enabling secure LDAP for this managed domain in [Task 3 - Enable secure LDAP for the managed domain](#task-3---enable-secure-ldap-for-the-managed-domain)</span></span>
    >
    >
15. <span data-ttu-id="4cc6a-191">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-191">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![Path for certificate export](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="4cc6a-193">On the following page, click **Finish** to export the certificate to a PFX file.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-193">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="4cc6a-194">You should see confirmation dialog when the certificate has been exported.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-194">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![Export certificate done](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)

## <a name="task-3---enable-secure-ldap-for-the-managed-domain"></a><span data-ttu-id="4cc6a-196">Task 3 - Enable secure LDAP for the managed domain</span><span class="sxs-lookup"><span data-stu-id="4cc6a-196">Task 3 - Enable secure LDAP for the managed domain</span></span>
<span data-ttu-id="4cc6a-197">To enable secure LDAP, perform the following configuration steps:</span><span class="sxs-lookup"><span data-stu-id="4cc6a-197">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="4cc6a-198">Navigate to the **[Azure classic portal](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-198">Navigate to the **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="4cc6a-199">Select the **Active Directory** node on the left pane.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-199">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="4cc6a-200">Select the Azure AD directory (also referred to as 'tenant'), for which you have enabled Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-200">Select the Azure AD directory (also referred to as 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Select Azure AD Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="4cc6a-202">Click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-202">Click the **Configure** tab.</span></span>

    ![Configure tab of directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="4cc6a-204">Scroll down to the section titled **domain services**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-204">Scroll down to the section titled **domain services**.</span></span> <span data-ttu-id="4cc6a-205">You should see an option titled **Secure LDAP (LDAPS)** as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="4cc6a-205">You should see an option titled **Secure LDAP (LDAPS)** as shown in the following screenshot:</span></span>

    ![Domain Services configuration section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="4cc6a-207">Click the **Configure certificate ...** button to bring up the **Configure Certificate for Secure LDAP** dialog.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-207">Click the **Configure certificate ...** button to bring up the **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Configure certificate for secure LDAP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="4cc6a-209">Click the folder icon below **PFX FILE WITH CERTIFICATE** to specify the PFX file, which contains the certificate you wish to use for secure LDAP access to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-209">Click the folder icon below **PFX FILE WITH CERTIFICATE** to specify the PFX file, which contains the certificate you wish to use for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="4cc6a-210">Also enter the password you specified when exporting the certificate to the PFX file.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-210">Also enter the password you specified when exporting the certificate to the PFX file.</span></span> <span data-ttu-id="4cc6a-211">Then, click the done button on the bottom.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-211">Then, click the done button on the bottom.</span></span>

    ![Specify secure LDAP PFX file and password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="4cc6a-213">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-213">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="4cc6a-214">During this period, the LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-214">During this period, the LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![Secure LDAP - pending state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="4cc6a-216">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-216">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="4cc6a-217">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-217">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="4cc6a-218">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-218">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="4cc6a-219">When secure LDAP is successfully enabled for your managed domain, the **Pending...** message should disappear.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-219">When secure LDAP is successfully enabled for your managed domain, the **Pending...** message should disappear.</span></span> <span data-ttu-id="4cc6a-220">You should see the thumbprint of the certificate displayed.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-220">You should see the thumbprint of the certificate displayed.</span></span>

    ![Secure LDAP enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-the-internet"></a><span data-ttu-id="4cc6a-222">Task 4 - Enable secure LDAP access over the internet</span><span class="sxs-lookup"><span data-stu-id="4cc6a-222">Task 4 - Enable secure LDAP access over the internet</span></span>
<span data-ttu-id="4cc6a-223">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-223">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="4cc6a-224">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain).</span><span class="sxs-lookup"><span data-stu-id="4cc6a-224">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain).</span></span>

1. <span data-ttu-id="4cc6a-225">You should see an option to **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** in the **domain services** section of the **Configure** page.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-225">You should see an option to **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** in the **domain services** section of the **Configure** page.</span></span> <span data-ttu-id="4cc6a-226">This option is set to **NO** by default since internet access to the managed domain over secure LDAP is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-226">This option is set to **NO** by default since internet access to the managed domain over secure LDAP is disabled by default.</span></span>

    ![Secure LDAP enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="4cc6a-228">Toggle **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** to **YES**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-228">Toggle **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** to **YES**.</span></span> <span data-ttu-id="4cc6a-229">Click the **SAVE** button on the bottom panel.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-229">Click the **SAVE** button on the bottom panel.</span></span>
    <span data-ttu-id="4cc6a-230">![Secure LDAP enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="4cc6a-230">![Secure LDAP enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="4cc6a-231">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-231">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="4cc6a-232">After some time, internet access to your managed domain over secure LDAP is enabled.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-232">After some time, internet access to your managed domain over secure LDAP is enabled.</span></span>

    ![Secure LDAP - pending state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="4cc6a-234">It takes about 10 minutes to enable internet access over secure LDAP for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-234">It takes about 10 minutes to enable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="4cc6a-235">When secure LDAP access to your managed domain over the internet is successfully enabled, the **Pending...** message should disappear.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-235">When secure LDAP access to your managed domain over the internet is successfully enabled, the **Pending...** message should disappear.</span></span> <span data-ttu-id="4cc6a-236">You should see the external IP address that can be used to access your directory over LDAPS in the field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-236">You should see the external IP address that can be used to access your directory over LDAPS in the field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![Secure LDAP enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="4cc6a-238">Task 5 - Configure DNS to access the managed domain from the internet</span><span class="sxs-lookup"><span data-stu-id="4cc6a-238">Task 5 - Configure DNS to access the managed domain from the internet</span></span>
<span data-ttu-id="4cc6a-239">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-239">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="4cc6a-240">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="4cc6a-240">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="4cc6a-241">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-241">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="4cc6a-242">At the end of task 4, an external IP address is displayed on the **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-242">At the end of task 4, an external IP address is displayed on the **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="4cc6a-243">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-243">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="4cc6a-244">In our example, we need to create the following DNS entry:</span><span class="sxs-lookup"><span data-stu-id="4cc6a-244">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="4cc6a-245">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-245">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="4cc6a-246">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-246">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="4cc6a-247">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-247">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="4cc6a-248">If you are using a self-signed certificate, you need to install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span><span class="sxs-lookup"><span data-stu-id="4cc6a-248">If you are using a self-signed certificate, you need to install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>

<br>

## <a name="related-content"></a><span data-ttu-id="4cc6a-249">Related Content</span><span class="sxs-lookup"><span data-stu-id="4cc6a-249">Related Content</span></span>
* [<span data-ttu-id="4cc6a-250">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="4cc6a-250">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="4cc6a-251">Administer an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="4cc6a-251">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="4cc6a-252">Administer Group Policy on an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="4cc6a-252">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)


























