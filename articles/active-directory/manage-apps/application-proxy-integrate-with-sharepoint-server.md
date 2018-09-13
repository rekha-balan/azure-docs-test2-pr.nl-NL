---
title: Enable remote access to SharePoint with Azure AD Application Proxy | Microsoft Docs
description: Covers the basics about how to integrate an on-premises SharePoint server with Azure AD Application Proxy.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/06/2017
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: fcd02e264d5e85b1bef7e75d2a6375d6bf5e18c0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868354"
---
# <a name="enable-remote-access-to-sharepoint-with-azure-ad-application-proxy"></a><span data-ttu-id="82b67-103">Enable remote access to SharePoint with Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="82b67-103">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>

<span data-ttu-id="82b67-104">This article discusses how to integrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="82b67-104">This article discusses how to integrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span></span>

<span data-ttu-id="82b67-105">To enable remote access to SharePoint with Azure AD Application Proxy, follow the sections in this article step by step.</span><span class="sxs-lookup"><span data-stu-id="82b67-105">To enable remote access to SharePoint with Azure AD Application Proxy, follow the sections in this article step by step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82b67-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="82b67-106">Prerequisites</span></span>

<span data-ttu-id="82b67-107">This article assumes that you already have SharePoint 2013 or newer in your environment.</span><span class="sxs-lookup"><span data-stu-id="82b67-107">This article assumes that you already have SharePoint 2013 or newer in your environment.</span></span> <span data-ttu-id="82b67-108">In addition, consider the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="82b67-108">In addition, consider the following prerequisites:</span></span>

* <span data-ttu-id="82b67-109">SharePoint includes native Kerberos support.</span><span class="sxs-lookup"><span data-stu-id="82b67-109">SharePoint includes native Kerberos support.</span></span> <span data-ttu-id="82b67-110">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume to have a single sign-on (SSO) experience.</span><span class="sxs-lookup"><span data-stu-id="82b67-110">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume to have a single sign-on (SSO) experience.</span></span>

* <span data-ttu-id="82b67-111">This scenario includes configuration changes to your SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="82b67-111">This scenario includes configuration changes to your SharePoint server.</span></span> <span data-ttu-id="82b67-112">We recommend using a staging environment.</span><span class="sxs-lookup"><span data-stu-id="82b67-112">We recommend using a staging environment.</span></span> <span data-ttu-id="82b67-113">This way, you can make updates to your staging server first, and then facilitate a testing cycle before going into production.</span><span class="sxs-lookup"><span data-stu-id="82b67-113">This way, you can make updates to your staging server first, and then facilitate a testing cycle before going into production.</span></span>

* <span data-ttu-id="82b67-114">We require SSL on the published URL.</span><span class="sxs-lookup"><span data-stu-id="82b67-114">We require SSL on the published URL.</span></span> <span data-ttu-id="82b67-115">You need to have SSL enabled on your internal site to ensure that links are sent/mapped correctly.</span><span class="sxs-lookup"><span data-stu-id="82b67-115">You need to have SSL enabled on your internal site to ensure that links are sent/mapped correctly.</span></span> <span data-ttu-id="82b67-116">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span><span class="sxs-lookup"><span data-stu-id="82b67-116">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span></span> <span data-ttu-id="82b67-117">Also, make sure that the connector machine trusts the certificate that you issue.</span><span class="sxs-lookup"><span data-stu-id="82b67-117">Also, make sure that the connector machine trusts the certificate that you issue.</span></span> <span data-ttu-id="82b67-118">(The certificate does not need to be publicly issued.)</span><span class="sxs-lookup"><span data-stu-id="82b67-118">(The certificate does not need to be publicly issued.)</span></span>

## <a name="step-1-set-up-single-sign-on-to-sharepoint"></a><span data-ttu-id="82b67-119">Step 1: Set up single sign-on to SharePoint</span><span class="sxs-lookup"><span data-stu-id="82b67-119">Step 1: Set up single sign-on to SharePoint</span></span>

<span data-ttu-id="82b67-120">For on-premises applications that use Windows authentication, you can achieve single sign-on (SSO) with the Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span><span class="sxs-lookup"><span data-stu-id="82b67-120">For on-premises applications that use Windows authentication, you can achieve single sign-on (SSO) with the Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span></span> <span data-ttu-id="82b67-121">KCD, when configured, allows the Application Proxy connector to obtain a Windows token for a user, even if the user hasn’t signed in to Windows directly.</span><span class="sxs-lookup"><span data-stu-id="82b67-121">KCD, when configured, allows the Application Proxy connector to obtain a Windows token for a user, even if the user hasn’t signed in to Windows directly.</span></span> <span data-ttu-id="82b67-122">To learn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b67-122">To learn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span></span>

<span data-ttu-id="82b67-123">To set up KCD for a SharePoint server, use the procedures in the following sequential sections:</span><span class="sxs-lookup"><span data-stu-id="82b67-123">To set up KCD for a SharePoint server, use the procedures in the following sequential sections:</span></span>

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a><span data-ttu-id="82b67-124">Ensure that SharePoint is running under a service account</span><span class="sxs-lookup"><span data-stu-id="82b67-124">Ensure that SharePoint is running under a service account</span></span>

<span data-ttu-id="82b67-125">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span><span class="sxs-lookup"><span data-stu-id="82b67-125">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span></span> <span data-ttu-id="82b67-126">Do this so that you can attach service principal names (SPNs) to a valid account.</span><span class="sxs-lookup"><span data-stu-id="82b67-126">Do this so that you can attach service principal names (SPNs) to a valid account.</span></span> <span data-ttu-id="82b67-127">SPNs are how the Kerberos protocol identifies different services.</span><span class="sxs-lookup"><span data-stu-id="82b67-127">SPNs are how the Kerberos protocol identifies different services.</span></span> <span data-ttu-id="82b67-128">And you will need the account later to configure the KCD.</span><span class="sxs-lookup"><span data-stu-id="82b67-128">And you will need the account later to configure the KCD.</span></span>

> [!NOTE]
<span data-ttu-id="82b67-129">You need to have a previously created Azure AD account for the service.</span><span class="sxs-lookup"><span data-stu-id="82b67-129">You need to have a previously created Azure AD account for the service.</span></span> <span data-ttu-id="82b67-130">We suggest that you allow for an automatic password change.</span><span class="sxs-lookup"><span data-stu-id="82b67-130">We suggest that you allow for an automatic password change.</span></span> <span data-ttu-id="82b67-131">For more information about the full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b67-131">For more information about the full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span></span>

<span data-ttu-id="82b67-132">To ensure that your sites are running under a defined service account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="82b67-132">To ensure that your sites are running under a defined service account, perform the following steps:</span></span>

1. <span data-ttu-id="82b67-133">Open the **SharePoint 2013 Central Administration** site.</span><span class="sxs-lookup"><span data-stu-id="82b67-133">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="82b67-134">Go to **Security** and select **Configure service accounts**.</span><span class="sxs-lookup"><span data-stu-id="82b67-134">Go to **Security** and select **Configure service accounts**.</span></span>
3. <span data-ttu-id="82b67-135">Select **Web Application Pool - SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="82b67-135">Select **Web Application Pool - SharePoint - 80**.</span></span> <span data-ttu-id="82b67-136">The options may be slightly different based on the name of your web pool, or if the web pool uses SSL by default.</span><span class="sxs-lookup"><span data-stu-id="82b67-136">The options may be slightly different based on the name of your web pool, or if the web pool uses SSL by default.</span></span>

  ![Choices for configuring a service account](./media/application-proxy-integrate-with-sharepoint-server/service-web-application.png)

4. <span data-ttu-id="82b67-138">If **Select an account for this component** field is set to **Local Service** or **Network Service**, you need to create an account.</span><span class="sxs-lookup"><span data-stu-id="82b67-138">If **Select an account for this component** field is set to **Local Service** or **Network Service**, you need to create an account.</span></span> <span data-ttu-id="82b67-139">If not, you're finished and can move to the next section.</span><span class="sxs-lookup"><span data-stu-id="82b67-139">If not, you're finished and can move to the next section.</span></span>
5. <span data-ttu-id="82b67-140">Select **Register new managed account**.</span><span class="sxs-lookup"><span data-stu-id="82b67-140">Select **Register new managed account**.</span></span> <span data-ttu-id="82b67-141">After your account is created, you must set **Web Application Pool** before you can use the account.</span><span class="sxs-lookup"><span data-stu-id="82b67-141">After your account is created, you must set **Web Application Pool** before you can use the account.</span></span>

### <a name="configure-sharepoint-for-kerberos"></a><span data-ttu-id="82b67-142">Configure SharePoint for Kerberos</span><span class="sxs-lookup"><span data-stu-id="82b67-142">Configure SharePoint for Kerberos</span></span>

<span data-ttu-id="82b67-143">You use KCD to perform single sign-on to the SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="82b67-143">You use KCD to perform single sign-on to the SharePoint server.</span></span>

<span data-ttu-id="82b67-144">To configure your SharePoint site for Kerberos authentication:</span><span class="sxs-lookup"><span data-stu-id="82b67-144">To configure your SharePoint site for Kerberos authentication:</span></span>

1. <span data-ttu-id="82b67-145">Open the **SharePoint 2013 Central Administration** site.</span><span class="sxs-lookup"><span data-stu-id="82b67-145">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="82b67-146">Go to **Application Management**, select **Manage web applications**, and select your SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="82b67-146">Go to **Application Management**, select **Manage web applications**, and select your SharePoint site.</span></span> <span data-ttu-id="82b67-147">In this example, it is **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="82b67-147">In this example, it is **SharePoint - 80**.</span></span>

  ![Selecting the SharePoint site](./media/application-proxy-integrate-with-sharepoint-server/manage-web-applications.png)

3. <span data-ttu-id="82b67-149">Click **Authentication Providers** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="82b67-149">Click **Authentication Providers** on the toolbar.</span></span>
4. <span data-ttu-id="82b67-150">In the **Authentication Providers** box, click **Default Zone** to view the settings.</span><span class="sxs-lookup"><span data-stu-id="82b67-150">In the **Authentication Providers** box, click **Default Zone** to view the settings.</span></span>
5. <span data-ttu-id="82b67-151">In the **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types**.</span><span class="sxs-lookup"><span data-stu-id="82b67-151">In the **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types**.</span></span> <span data-ttu-id="82b67-152">Ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span><span class="sxs-lookup"><span data-stu-id="82b67-152">Ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span></span>
6. <span data-ttu-id="82b67-153">In the drop-down box for the Integrated Windows Authentication field, make sure that **Negotiate (Kerberos)** is selected.</span><span class="sxs-lookup"><span data-stu-id="82b67-153">In the drop-down box for the Integrated Windows Authentication field, make sure that **Negotiate (Kerberos)** is selected.</span></span>

  ![Edit Authentication dialog box](./media/application-proxy-integrate-with-sharepoint-server/service-edit-authentication.png)

7. <span data-ttu-id="82b67-155">At the bottom of the **Edit Authentication** dialog box, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="82b67-155">At the bottom of the **Edit Authentication** dialog box, click **Save**.</span></span>

### <a name="set-a-service-principal-name-for-the-sharepoint-service-account"></a><span data-ttu-id="82b67-156">Set a service principal name for the SharePoint service account</span><span class="sxs-lookup"><span data-stu-id="82b67-156">Set a service principal name for the SharePoint service account</span></span>

<span data-ttu-id="82b67-157">Before you configure  KCD, you need to identify the SharePoint service running as the service account that you've configured.</span><span class="sxs-lookup"><span data-stu-id="82b67-157">Before you configure  KCD, you need to identify the SharePoint service running as the service account that you've configured.</span></span> <span data-ttu-id="82b67-158">Identify the service by setting an SPN.</span><span class="sxs-lookup"><span data-stu-id="82b67-158">Identify the service by setting an SPN.</span></span> <span data-ttu-id="82b67-159">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b67-159">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span></span>

<span data-ttu-id="82b67-160">The SPN format is:</span><span class="sxs-lookup"><span data-stu-id="82b67-160">The SPN format is:</span></span>

```
<service class>/<host>:<port>
```

<span data-ttu-id="82b67-161">In the SPN format:</span><span class="sxs-lookup"><span data-stu-id="82b67-161">In the SPN format:</span></span>

* <span data-ttu-id="82b67-162">_service class_ is a unique name for the service.</span><span class="sxs-lookup"><span data-stu-id="82b67-162">_service class_ is a unique name for the service.</span></span> <span data-ttu-id="82b67-163">For SharePoint, you use **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="82b67-163">For SharePoint, you use **HTTP**.</span></span>

* <span data-ttu-id="82b67-164">_host_ is the fully qualified domain or NetBIOS name of the host that the service is running on.</span><span class="sxs-lookup"><span data-stu-id="82b67-164">_host_ is the fully qualified domain or NetBIOS name of the host that the service is running on.</span></span> <span data-ttu-id="82b67-165">For a SharePoint site, this text might need to be the URL of the site, depending on the version of IIS that you're using.</span><span class="sxs-lookup"><span data-stu-id="82b67-165">For a SharePoint site, this text might need to be the URL of the site, depending on the version of IIS that you're using.</span></span>

* <span data-ttu-id="82b67-166">_port_ is optional.</span><span class="sxs-lookup"><span data-stu-id="82b67-166">_port_ is optional.</span></span>

<span data-ttu-id="82b67-167">If the FQDN of the SharePoint server is:</span><span class="sxs-lookup"><span data-stu-id="82b67-167">If the FQDN of the SharePoint server is:</span></span>

```
sharepoint.demo.o365identity.us
```

<span data-ttu-id="82b67-168">Then the SPN is:</span><span class="sxs-lookup"><span data-stu-id="82b67-168">Then the SPN is:</span></span>

```
HTTP/sharepoint.demo.o365identity.us demo
```

<span data-ttu-id="82b67-169">You might also need to set SPNs for specific sites on your server.</span><span class="sxs-lookup"><span data-stu-id="82b67-169">You might also need to set SPNs for specific sites on your server.</span></span> <span data-ttu-id="82b67-170">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span><span class="sxs-lookup"><span data-stu-id="82b67-170">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span></span> <span data-ttu-id="82b67-171">Pay close attention to the "Create Service Principal Names for your Web applications using Kerberos authentication" section.</span><span class="sxs-lookup"><span data-stu-id="82b67-171">Pay close attention to the "Create Service Principal Names for your Web applications using Kerberos authentication" section.</span></span>

<span data-ttu-id="82b67-172">The easiest way for you to set SPNs is to follow the SPN formats that may already be present for your sites.</span><span class="sxs-lookup"><span data-stu-id="82b67-172">The easiest way for you to set SPNs is to follow the SPN formats that may already be present for your sites.</span></span> <span data-ttu-id="82b67-173">Copy those SPNs to register against the service account.</span><span class="sxs-lookup"><span data-stu-id="82b67-173">Copy those SPNs to register against the service account.</span></span> <span data-ttu-id="82b67-174">To do this:</span><span class="sxs-lookup"><span data-stu-id="82b67-174">To do this:</span></span>

1. <span data-ttu-id="82b67-175">Browse to the site with the SPN from another machine.</span><span class="sxs-lookup"><span data-stu-id="82b67-175">Browse to the site with the SPN from another machine.</span></span>
 <span data-ttu-id="82b67-176">When you do, the relevant set of Kerberos tickets is cached on the machine.</span><span class="sxs-lookup"><span data-stu-id="82b67-176">When you do, the relevant set of Kerberos tickets is cached on the machine.</span></span> <span data-ttu-id="82b67-177">These tickets contain the SPN of the target site that you browsed to.</span><span class="sxs-lookup"><span data-stu-id="82b67-177">These tickets contain the SPN of the target site that you browsed to.</span></span>

2. <span data-ttu-id="82b67-178">You can pull the SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span><span class="sxs-lookup"><span data-stu-id="82b67-178">You can pull the SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span></span> <span data-ttu-id="82b67-179">In a command window that's running in the same context as the user who accessed the site in the browser, run the following command:</span><span class="sxs-lookup"><span data-stu-id="82b67-179">In a command window that's running in the same context as the user who accessed the site in the browser, run the following command:</span></span>
```
Klist
```
<span data-ttu-id="82b67-180">Klist then returns the set of target SPNs.</span><span class="sxs-lookup"><span data-stu-id="82b67-180">Klist then returns the set of target SPNs.</span></span> <span data-ttu-id="82b67-181">In this example, the highlighted value is the SPN that's needed:</span><span class="sxs-lookup"><span data-stu-id="82b67-181">In this example, the highlighted value is the SPN that's needed:</span></span>

  ![Example Klist results](./media/application-proxy-integrate-with-sharepoint-server/remote-sharepoint-target-service.png)

4. <span data-ttu-id="82b67-183">Now that you have the SPN, make sure that it's configured correctly on the service account that you set up for the web application earlier.</span><span class="sxs-lookup"><span data-stu-id="82b67-183">Now that you have the SPN, make sure that it's configured correctly on the service account that you set up for the web application earlier.</span></span> <span data-ttu-id="82b67-184">Run the following command from the command prompt as an administrator of the domain:</span><span class="sxs-lookup"><span data-stu-id="82b67-184">Run the following command from the command prompt as an administrator of the domain:</span></span>

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 <span data-ttu-id="82b67-185">This command sets the SPN for the SharePoint service account running as _demo\sp_svc_.</span><span class="sxs-lookup"><span data-stu-id="82b67-185">This command sets the SPN for the SharePoint service account running as _demo\sp_svc_.</span></span>

 <span data-ttu-id="82b67-186">Replace _http/sharepoint.demo.o365identity.us_ with the SPN for your server and _demo\sp_svc_ with the service account in your environment.</span><span class="sxs-lookup"><span data-stu-id="82b67-186">Replace _http/sharepoint.demo.o365identity.us_ with the SPN for your server and _demo\sp_svc_ with the service account in your environment.</span></span> <span data-ttu-id="82b67-187">The Setspn command searches for the SPN before it adds it.</span><span class="sxs-lookup"><span data-stu-id="82b67-187">The Setspn command searches for the SPN before it adds it.</span></span> <span data-ttu-id="82b67-188">In this case, you might see a **Duplicate SPN Value** error.</span><span class="sxs-lookup"><span data-stu-id="82b67-188">In this case, you might see a **Duplicate SPN Value** error.</span></span> <span data-ttu-id="82b67-189">If you see this error, make sure that the value is associated with the service account.</span><span class="sxs-lookup"><span data-stu-id="82b67-189">If you see this error, make sure that the value is associated with the service account.</span></span>

<span data-ttu-id="82b67-190">You can verify that the SPN was added by running the Setspn command with the -l option.</span><span class="sxs-lookup"><span data-stu-id="82b67-190">You can verify that the SPN was added by running the Setspn command with the -l option.</span></span> <span data-ttu-id="82b67-191">To learn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b67-191">To learn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span></span>

### <a name="ensure-that-the-connector-is-set-as-a-trusted-delegate-to-sharepoint"></a><span data-ttu-id="82b67-192">Ensure that the connector is set as a trusted delegate to SharePoint</span><span class="sxs-lookup"><span data-stu-id="82b67-192">Ensure that the connector is set as a trusted delegate to SharePoint</span></span>

<span data-ttu-id="82b67-193">Configure the KCD so that the Azure AD Application Proxy service can delegate user identities to the SharePoint service.</span><span class="sxs-lookup"><span data-stu-id="82b67-193">Configure the KCD so that the Azure AD Application Proxy service can delegate user identities to the SharePoint service.</span></span> <span data-ttu-id="82b67-194">Configure KCD by enabling the Application Proxy connector to retrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82b67-194">Configure KCD by enabling the Application Proxy connector to retrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span></span> <span data-ttu-id="82b67-195">Then that server passes the context to the target application, or SharePoint in this case.</span><span class="sxs-lookup"><span data-stu-id="82b67-195">Then that server passes the context to the target application, or SharePoint in this case.</span></span>

<span data-ttu-id="82b67-196">To configure the KCD, repeat the following steps for each connector machine:</span><span class="sxs-lookup"><span data-stu-id="82b67-196">To configure the KCD, repeat the following steps for each connector machine:</span></span>

1. <span data-ttu-id="82b67-197">Log in as a domain administrator to a DC, and then open **Active Directory Users and Computers**.</span><span class="sxs-lookup"><span data-stu-id="82b67-197">Log in as a domain administrator to a DC, and then open **Active Directory Users and Computers**.</span></span>
2. <span data-ttu-id="82b67-198">Find the computer that the connector is running on.</span><span class="sxs-lookup"><span data-stu-id="82b67-198">Find the computer that the connector is running on.</span></span> <span data-ttu-id="82b67-199">In this example, it's the same SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="82b67-199">In this example, it's the same SharePoint server.</span></span>
3. <span data-ttu-id="82b67-200">Double-click the computer, and then click the **Delegation** tab.</span><span class="sxs-lookup"><span data-stu-id="82b67-200">Double-click the computer, and then click the **Delegation** tab.</span></span>
4. <span data-ttu-id="82b67-201">Ensure that the delegation settings are set to **Trust this computer for delegation to the specified services only**.</span><span class="sxs-lookup"><span data-stu-id="82b67-201">Ensure that the delegation settings are set to **Trust this computer for delegation to the specified services only**.</span></span> <span data-ttu-id="82b67-202">Then, select **Use any authentication protocol**.</span><span class="sxs-lookup"><span data-stu-id="82b67-202">Then, select **Use any authentication protocol**.</span></span>

  ![Delegation settings](./media/application-proxy-integrate-with-sharepoint-server/delegation-box.png)

5. <span data-ttu-id="82b67-204">Click the **Add** button, click **Users or Computers**, and locate the service account.</span><span class="sxs-lookup"><span data-stu-id="82b67-204">Click the **Add** button, click **Users or Computers**, and locate the service account.</span></span>

  ![Adding the SPN for the service account](./media/application-proxy-integrate-with-sharepoint-server/users-computers.png)

6. <span data-ttu-id="82b67-206">In the list of SPNs, select the one that you created earlier for the service account.</span><span class="sxs-lookup"><span data-stu-id="82b67-206">In the list of SPNs, select the one that you created earlier for the service account.</span></span>
7. <span data-ttu-id="82b67-207">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="82b67-207">Click **OK**.</span></span> <span data-ttu-id="82b67-208">Click **OK** again to save the changes.</span><span class="sxs-lookup"><span data-stu-id="82b67-208">Click **OK** again to save the changes.</span></span>

## <a name="step-2-enable-remote-access-to-sharepoint"></a><span data-ttu-id="82b67-209">Step 2: Enable remote access to SharePoint</span><span class="sxs-lookup"><span data-stu-id="82b67-209">Step 2: Enable remote access to SharePoint</span></span>

<span data-ttu-id="82b67-210">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready to publish the SharePoint farm for remote access through Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="82b67-210">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready to publish the SharePoint farm for remote access through Azure AD Application Proxy.</span></span>

1. <span data-ttu-id="82b67-211">Publish your SharePoint site with the following settings.</span><span class="sxs-lookup"><span data-stu-id="82b67-211">Publish your SharePoint site with the following settings.</span></span> <span data-ttu-id="82b67-212">For step-by-step instructions, see [Publishing applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="82b67-212">For step-by-step instructions, see [Publishing applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span> 
   - <span data-ttu-id="82b67-213">**Internal URL**: the URL of the SharePoint site internally, such as **https://SharePoint/**.</span><span class="sxs-lookup"><span data-stu-id="82b67-213">**Internal URL**: the URL of the SharePoint site internally, such as **https://SharePoint/**.</span></span> <span data-ttu-id="82b67-214">In this example, make sure to use **https**</span><span class="sxs-lookup"><span data-stu-id="82b67-214">In this example, make sure to use **https**</span></span>
   - <span data-ttu-id="82b67-215">**Preauthentication Method**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82b67-215">**Preauthentication Method**: Azure Active Directory</span></span>
   - <span data-ttu-id="82b67-216">**Translate URL in Headers**: NO</span><span class="sxs-lookup"><span data-stu-id="82b67-216">**Translate URL in Headers**: NO</span></span>

   >[!TIP]
   ><span data-ttu-id="82b67-217">SharePoint uses the _Host Header_ value to look up the site.</span><span class="sxs-lookup"><span data-stu-id="82b67-217">SharePoint uses the _Host Header_ value to look up the site.</span></span> <span data-ttu-id="82b67-218">It also generates links based on this value.</span><span class="sxs-lookup"><span data-stu-id="82b67-218">It also generates links based on this value.</span></span> <span data-ttu-id="82b67-219">The net effect is that any link that SharePoint generates is a published URL that is correctly set to use the external URL.</span><span class="sxs-lookup"><span data-stu-id="82b67-219">The net effect is that any link that SharePoint generates is a published URL that is correctly set to use the external URL.</span></span> <span data-ttu-id="82b67-220">Setting the value to **YES** also enables the connector to forward the request to the back-end application.</span><span class="sxs-lookup"><span data-stu-id="82b67-220">Setting the value to **YES** also enables the connector to forward the request to the back-end application.</span></span> <span data-ttu-id="82b67-221">However, setting the value to **NO** means that the connector will not send the internal host name.</span><span class="sxs-lookup"><span data-stu-id="82b67-221">However, setting the value to **NO** means that the connector will not send the internal host name.</span></span> <span data-ttu-id="82b67-222">Instead, the connector sends the host header as the published URL to the back-end application.</span><span class="sxs-lookup"><span data-stu-id="82b67-222">Instead, the connector sends the host header as the published URL to the back-end application.</span></span>

   ![Publish SharePoint as application](./media/application-proxy-integrate-with-sharepoint-server/publish-app.png)

2. <span data-ttu-id="82b67-224">Once your app is published, configure the single sign-on settings with the following steps:</span><span class="sxs-lookup"><span data-stu-id="82b67-224">Once your app is published, configure the single sign-on settings with the following steps:</span></span>

   1. <span data-ttu-id="82b67-225">On the application page in the portal, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="82b67-225">On the application page in the portal, select **Single sign-on**.</span></span>
   2. <span data-ttu-id="82b67-226">For Single Sign-on Mode, select **Integrated Windows Authentication**.</span><span class="sxs-lookup"><span data-stu-id="82b67-226">For Single Sign-on Mode, select **Integrated Windows Authentication**.</span></span>
   3. <span data-ttu-id="82b67-227">Set Internal Application SPN to the value that you set earlier.</span><span class="sxs-lookup"><span data-stu-id="82b67-227">Set Internal Application SPN to the value that you set earlier.</span></span> <span data-ttu-id="82b67-228">For this example, that would be **http/sharepoint.demo.o365identity.us**.</span><span class="sxs-lookup"><span data-stu-id="82b67-228">For this example, that would be **http/sharepoint.demo.o365identity.us**.</span></span>

   ![Configure Integrated Windows Authentication for SSO](./media/application-proxy-integrate-with-sharepoint-server/configure-iwa.png)

3. <span data-ttu-id="82b67-230">To finish setting up your application, go to the **Users and groups** section and assign users to access this application.</span><span class="sxs-lookup"><span data-stu-id="82b67-230">To finish setting up your application, go to the **Users and groups** section and assign users to access this application.</span></span> 

## <a name="step-3-ensure-that-sharepoint-knows-about-the-external-url"></a><span data-ttu-id="82b67-231">Step 3: Ensure that SharePoint knows about the external URL</span><span class="sxs-lookup"><span data-stu-id="82b67-231">Step 3: Ensure that SharePoint knows about the external URL</span></span>

<span data-ttu-id="82b67-232">Your last step is to ensure that SharePoint can find the site based on the external URL, so that it renders links based on that external URL.</span><span class="sxs-lookup"><span data-stu-id="82b67-232">Your last step is to ensure that SharePoint can find the site based on the external URL, so that it renders links based on that external URL.</span></span> <span data-ttu-id="82b67-233">You do this by configuring alternate access mappings for the SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="82b67-233">You do this by configuring alternate access mappings for the SharePoint site.</span></span>

1. <span data-ttu-id="82b67-234">Open the **SharePoint 2013 Central Administration** site.</span><span class="sxs-lookup"><span data-stu-id="82b67-234">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="82b67-235">Under **System Settings**, select **Configure Alternate Access Mappings**.</span><span class="sxs-lookup"><span data-stu-id="82b67-235">Under **System Settings**, select **Configure Alternate Access Mappings**.</span></span> <span data-ttu-id="82b67-236">The Alternate Access Mappings box opens.</span><span class="sxs-lookup"><span data-stu-id="82b67-236">The Alternate Access Mappings box opens.</span></span>

  ![Alternate Access Mappings box](./media/application-proxy-integrate-with-sharepoint-server/alternate-access1.png)

3. <span data-ttu-id="82b67-238">In the drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span><span class="sxs-lookup"><span data-stu-id="82b67-238">In the drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span></span>
4. <span data-ttu-id="82b67-239">Select your site--for example, **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="82b67-239">Select your site--for example, **SharePoint - 80**.</span></span>
5. <span data-ttu-id="82b67-240">You can choose to add the published URL as either an internal URL or a public URL.</span><span class="sxs-lookup"><span data-stu-id="82b67-240">You can choose to add the published URL as either an internal URL or a public URL.</span></span> <span data-ttu-id="82b67-241">This example uses a public URL as the extranet.</span><span class="sxs-lookup"><span data-stu-id="82b67-241">This example uses a public URL as the extranet.</span></span>
6. <span data-ttu-id="82b67-242">Click **Edit Public URLs** in the **Extranet** path, and then enter the External URL that was created when you published the application.</span><span class="sxs-lookup"><span data-stu-id="82b67-242">Click **Edit Public URLs** in the **Extranet** path, and then enter the External URL that was created when you published the application.</span></span> <span data-ttu-id="82b67-243">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span><span class="sxs-lookup"><span data-stu-id="82b67-243">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span></span>

  ![Entering the path](./media/application-proxy-integrate-with-sharepoint-server/alternate-access3.png)

7. <span data-ttu-id="82b67-245">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="82b67-245">Click **Save**.</span></span>

<span data-ttu-id="82b67-246">You can now access the SharePoint site externally via Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="82b67-246">You can now access the SharePoint site externally via Azure AD Application Proxy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82b67-247">Next steps</span><span class="sxs-lookup"><span data-stu-id="82b67-247">Next steps</span></span>

- [<span data-ttu-id="82b67-248">Working with custom domains in Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="82b67-248">Working with custom domains in Azure AD Application Proxy</span></span>](application-proxy-configure-custom-domain.md)
- [<span data-ttu-id="82b67-249">Understand Azure AD Application Proxy connectors</span><span class="sxs-lookup"><span data-stu-id="82b67-249">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-connectors.md)

