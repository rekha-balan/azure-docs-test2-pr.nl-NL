---
title: Enable remote access to SharePoint with Azure AD Application Proxy | Microsoft Docs
description: Covers the basics about how to integrate an on-premises SharePoint server with Azure AD Application Proxy.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: kgremban
ms.openlocfilehash: a45586d410e3257c9d047a5b49a665e0a5a29fa5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556536"
---
# <a name="enable-remote-access-to-sharepoint-with-azure-ad-application-proxy"></a><span data-ttu-id="99468-103">Enable remote access to SharePoint with Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="99468-103">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>

<span data-ttu-id="99468-104">This article discusses how to integrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="99468-104">This article discusses how to integrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span></span>

<span data-ttu-id="99468-105">To enable remote access to SharePoint with Azure AD Application Proxy, follow the sections in this article step by step.</span><span class="sxs-lookup"><span data-stu-id="99468-105">To enable remote access to SharePoint with Azure AD Application Proxy, follow the sections in this article step by step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99468-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99468-106">Prerequisites</span></span>

<span data-ttu-id="99468-107">This article assumes that you already have SharePoint 2013 or newer already set up and running in your environment.</span><span class="sxs-lookup"><span data-stu-id="99468-107">This article assumes that you already have SharePoint 2013 or newer already set up and running in your environment.</span></span> <span data-ttu-id="99468-108">In addition, consider the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="99468-108">In addition, consider the following prerequisites:</span></span>

* <span data-ttu-id="99468-109">The Application Proxy feature is available only if you upgraded to the Premium or Basic edition of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="99468-109">The Application Proxy feature is available only if you upgraded to the Premium or Basic edition of Azure Active Directory.</span></span> <span data-ttu-id="99468-110">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="99468-110">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

* <span data-ttu-id="99468-111">SharePoint includes native Kerberos support.</span><span class="sxs-lookup"><span data-stu-id="99468-111">SharePoint includes native Kerberos support.</span></span> <span data-ttu-id="99468-112">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume to have a seamless single sign-on (SSO) experience.</span><span class="sxs-lookup"><span data-stu-id="99468-112">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume to have a seamless single sign-on (SSO) experience.</span></span>

* <span data-ttu-id="99468-113">You will need to make a few configuration changes to your SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="99468-113">You will need to make a few configuration changes to your SharePoint server.</span></span> <span data-ttu-id="99468-114">We recommend using a staging environment.</span><span class="sxs-lookup"><span data-stu-id="99468-114">We recommend using a staging environment.</span></span> <span data-ttu-id="99468-115">This way, you can make updates to your staging server first, and then facilitate a testing cycle before going into production.</span><span class="sxs-lookup"><span data-stu-id="99468-115">This way, you can make updates to your staging server first, and then facilitate a testing cycle before going into production.</span></span>

* <span data-ttu-id="99468-116">We assume that you have already set up SSL for SharePoint, because we require SSL on the published URL.</span><span class="sxs-lookup"><span data-stu-id="99468-116">We assume that you have already set up SSL for SharePoint, because we require SSL on the published URL.</span></span> <span data-ttu-id="99468-117">You need to have SSL enabled on your internal site, to ensure that links are sent/mapped correctly.</span><span class="sxs-lookup"><span data-stu-id="99468-117">You need to have SSL enabled on your internal site, to ensure that links are sent/mapped correctly.</span></span> <span data-ttu-id="99468-118">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span><span class="sxs-lookup"><span data-stu-id="99468-118">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span></span> <span data-ttu-id="99468-119">Also, make sure that the connector machine trusts the certificate that you issue.</span><span class="sxs-lookup"><span data-stu-id="99468-119">Also, make sure that the connector machine trusts the certificate that you issue.</span></span> <span data-ttu-id="99468-120">(The certificate does not need to be publicly issued.)</span><span class="sxs-lookup"><span data-stu-id="99468-120">(The certificate does not need to be publicly issued.)</span></span>

## <a name="step-1-set-up-single-sign-on-to-sharepoint"></a><span data-ttu-id="99468-121">Step 1: Set up single sign-on to SharePoint</span><span class="sxs-lookup"><span data-stu-id="99468-121">Step 1: Set up single sign-on to SharePoint</span></span>

<span data-ttu-id="99468-122">Our customers want the best SSO experience for their back-end applications, SharePoint server in this case.</span><span class="sxs-lookup"><span data-stu-id="99468-122">Our customers want the best SSO experience for their back-end applications, SharePoint server in this case.</span></span> <span data-ttu-id="99468-123">In this common Azure AD scenario, the user is authenticated only once, because they will not be prompted for authentication again.</span><span class="sxs-lookup"><span data-stu-id="99468-123">In this common Azure AD scenario, the user is authenticated only once, because they will not be prompted for authentication again.</span></span>

<span data-ttu-id="99468-124">For on-premises applications that require or use Windows authentication, you can achieve SSO by using the Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span><span class="sxs-lookup"><span data-stu-id="99468-124">For on-premises applications that require or use Windows authentication, you can achieve SSO by using the Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span></span> <span data-ttu-id="99468-125">KCD, when configured, allows the Application Proxy connector to obtain a windows ticket/token for a user, even if the user hasn’t signed in to Windows directly.</span><span class="sxs-lookup"><span data-stu-id="99468-125">KCD, when configured, allows the Application Proxy connector to obtain a windows ticket/token for a user, even if the user hasn’t signed in to Windows directly.</span></span> <span data-ttu-id="99468-126">To learn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span><span class="sxs-lookup"><span data-stu-id="99468-126">To learn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span></span>

<span data-ttu-id="99468-127">To set up KCD for a SharePoint server, use the procedures in the following sequential sections.</span><span class="sxs-lookup"><span data-stu-id="99468-127">To set up KCD for a SharePoint server, use the procedures in the following sequential sections.</span></span>

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a><span data-ttu-id="99468-128">Ensure that SharePoint is running under a service account</span><span class="sxs-lookup"><span data-stu-id="99468-128">Ensure that SharePoint is running under a service account</span></span>

<span data-ttu-id="99468-129">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span><span class="sxs-lookup"><span data-stu-id="99468-129">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span></span> <span data-ttu-id="99468-130">You need to do this so that you can attach service principal names (SPNs) to a valid account.</span><span class="sxs-lookup"><span data-stu-id="99468-130">You need to do this so that you can attach service principal names (SPNs) to a valid account.</span></span> <span data-ttu-id="99468-131">SPNs are how the Kerberos protocol identifies different services.</span><span class="sxs-lookup"><span data-stu-id="99468-131">SPNs are how the Kerberos protocol identifies different services.</span></span> <span data-ttu-id="99468-132">And you will need the account later to configure the KCD.</span><span class="sxs-lookup"><span data-stu-id="99468-132">And you will need the account later to configure the KCD.</span></span>

<span data-ttu-id="99468-133">To ensure that your sites are running under a defined service account, do the following:</span><span class="sxs-lookup"><span data-stu-id="99468-133">To ensure that your sites are running under a defined service account, do the following:</span></span>

1. <span data-ttu-id="99468-134">Open the **SharePoint 2013 Central Administration** site.</span><span class="sxs-lookup"><span data-stu-id="99468-134">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="99468-135">Go to **Security** and select **Configure service accounts**.</span><span class="sxs-lookup"><span data-stu-id="99468-135">Go to **Security** and select **Configure service accounts**.</span></span>
3. <span data-ttu-id="99468-136">Select **Web Application Pool - SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="99468-136">Select **Web Application Pool - SharePoint - 80**.</span></span> <span data-ttu-id="99468-137">The options may be slightly different based on the name of your web pool, or if the web pool uses SSL by default.</span><span class="sxs-lookup"><span data-stu-id="99468-137">The options may be slightly different based on the name of your web pool, or if the web pool uses SSL by default.</span></span>

  ![Choices for configuring a service account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. <span data-ttu-id="99468-139">If **Select an account for this component** is **Local Service** or **Network Service**, you need to create an account.</span><span class="sxs-lookup"><span data-stu-id="99468-139">If **Select an account for this component** is **Local Service** or **Network Service**, you need to create an account.</span></span> <span data-ttu-id="99468-140">If not, you're finished and can move to the next section.</span><span class="sxs-lookup"><span data-stu-id="99468-140">If not, you're finished and can move to the next section.</span></span>
5. <span data-ttu-id="99468-141">Select **Register new managed account**.</span><span class="sxs-lookup"><span data-stu-id="99468-141">Select **Register new managed account**.</span></span> <span data-ttu-id="99468-142">After your account is created, you must set **Web Application Pool** before you can use the account.</span><span class="sxs-lookup"><span data-stu-id="99468-142">After your account is created, you must set **Web Application Pool** before you can use the account.</span></span>

> [!NOTE]
<span data-ttu-id="99468-143">You need to have a previously created Azure AD account for the service.</span><span class="sxs-lookup"><span data-stu-id="99468-143">You need to have a previously created Azure AD account for the service.</span></span> <span data-ttu-id="99468-144">We suggest that you allow for an automatic password change.</span><span class="sxs-lookup"><span data-stu-id="99468-144">We suggest that you allow for an automatic password change.</span></span> <span data-ttu-id="99468-145">For more information about the full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span><span class="sxs-lookup"><span data-stu-id="99468-145">For more information about the full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span></span>

### <a name="configure-sharepoint-for-kerberos"></a><span data-ttu-id="99468-146">Configure SharePoint for Kerberos</span><span class="sxs-lookup"><span data-stu-id="99468-146">Configure SharePoint for Kerberos</span></span>

<span data-ttu-id="99468-147">You use KCD to perform single sign-on to the SharePoint server, and this works only with Kerberos.</span><span class="sxs-lookup"><span data-stu-id="99468-147">You use KCD to perform single sign-on to the SharePoint server, and this works only with Kerberos.</span></span>

<span data-ttu-id="99468-148">To configure your SharePoint site for Kerberos authentication:</span><span class="sxs-lookup"><span data-stu-id="99468-148">To configure your SharePoint site for Kerberos authentication:</span></span>

1. <span data-ttu-id="99468-149">Open the **SharePoint 2013 Central Administration** site.</span><span class="sxs-lookup"><span data-stu-id="99468-149">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="99468-150">Go to **Application Management**, select **Manage web applications**, and select your SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="99468-150">Go to **Application Management**, select **Manage web applications**, and select your SharePoint site.</span></span> <span data-ttu-id="99468-151">In this example, it's **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="99468-151">In this example, it's **SharePoint - 80**.</span></span>

  ![Selecting the SharePoint site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. <span data-ttu-id="99468-153">Click **Authentication Providers** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="99468-153">Click **Authentication Providers** on the toolbar.</span></span>
4. <span data-ttu-id="99468-154">In the **Authentication Providers** box, click **Default Zone** to view the settings.</span><span class="sxs-lookup"><span data-stu-id="99468-154">In the **Authentication Providers** box, click **Default Zone** to view the settings.</span></span>
5. <span data-ttu-id="99468-155">In the **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types** and ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span><span class="sxs-lookup"><span data-stu-id="99468-155">In the **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types** and ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span></span>
6. <span data-ttu-id="99468-156">In the drop-down box, make sure that **Negotiate (Kerberos)** is selected.</span><span class="sxs-lookup"><span data-stu-id="99468-156">In the drop-down box, make sure that **Negotiate (Kerberos)** is selected.</span></span>

  ![Edit Authentication dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. <span data-ttu-id="99468-158">At the bottom of the **Edit Authentication** dialog box, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="99468-158">At the bottom of the **Edit Authentication** dialog box, click **Save**.</span></span>

### <a name="set-a-service-principal-name-for-the-sharepoint-service-account"></a><span data-ttu-id="99468-159">Set a service principal name for the SharePoint service account</span><span class="sxs-lookup"><span data-stu-id="99468-159">Set a service principal name for the SharePoint service account</span></span>

<span data-ttu-id="99468-160">Before you configure the KCD, you need to identify the SharePoint service running as the service account that you've configured.</span><span class="sxs-lookup"><span data-stu-id="99468-160">Before you configure the KCD, you need to identify the SharePoint service running as the service account that you've configured.</span></span> <span data-ttu-id="99468-161">You do this by setting an SPN.</span><span class="sxs-lookup"><span data-stu-id="99468-161">You do this by setting an SPN.</span></span> <span data-ttu-id="99468-162">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span><span class="sxs-lookup"><span data-stu-id="99468-162">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span></span>

<span data-ttu-id="99468-163">The SPN format is:</span><span class="sxs-lookup"><span data-stu-id="99468-163">The SPN format is:</span></span>

```
<service class>/<host>:<port>
```

<span data-ttu-id="99468-164">In the SPN format:</span><span class="sxs-lookup"><span data-stu-id="99468-164">In the SPN format:</span></span>

* <span data-ttu-id="99468-165">_service class_ is a unique name for the service.</span><span class="sxs-lookup"><span data-stu-id="99468-165">_service class_ is a unique name for the service.</span></span> <span data-ttu-id="99468-166">For SharePoint, you use **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="99468-166">For SharePoint, you use **HTTP**.</span></span>

* <span data-ttu-id="99468-167">_host_ is the fully qualified domain or NetBIOS name of the host that the service is running on.</span><span class="sxs-lookup"><span data-stu-id="99468-167">_host_ is the fully qualified domain or NetBIOS name of the host that the service is running on.</span></span> <span data-ttu-id="99468-168">In the case of a SharePoint site, this might need to be the URL of the site, depending on the version of IIS that you're using.</span><span class="sxs-lookup"><span data-stu-id="99468-168">In the case of a SharePoint site, this might need to be the URL of the site, depending on the version of IIS that you're using.</span></span>

* <span data-ttu-id="99468-169">_port_ is optional.</span><span class="sxs-lookup"><span data-stu-id="99468-169">_port_ is optional.</span></span>

<span data-ttu-id="99468-170">If the FQDN of the SharePoint server is:</span><span class="sxs-lookup"><span data-stu-id="99468-170">If the FQDN of the SharePoint server is:</span></span>

```
sharepoint.demo.o365identity.us
```

<span data-ttu-id="99468-171">Then the SPN is:</span><span class="sxs-lookup"><span data-stu-id="99468-171">Then the SPN is:</span></span>

```
HTTP/ sharepoint.demo.o365identity.us demo
```

<span data-ttu-id="99468-172">You might also need to set SPNs for specific sites on your server.</span><span class="sxs-lookup"><span data-stu-id="99468-172">You might also need to set SPNs for specific sites on your server.</span></span> <span data-ttu-id="99468-173">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span><span class="sxs-lookup"><span data-stu-id="99468-173">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span></span> <span data-ttu-id="99468-174">Pay close attention to the section "Create Service Principal Names for your Web applications using Kerberos authentication."</span><span class="sxs-lookup"><span data-stu-id="99468-174">Pay close attention to the section "Create Service Principal Names for your Web applications using Kerberos authentication."</span></span>

<span data-ttu-id="99468-175">The easiest way for you to set SPNs is to follow the SPN formats that may already be present for your sites.</span><span class="sxs-lookup"><span data-stu-id="99468-175">The easiest way for you to set SPNs is to follow the SPN formats that may already be present for your sites.</span></span> <span data-ttu-id="99468-176">Copy those SPNs to register against the service account.</span><span class="sxs-lookup"><span data-stu-id="99468-176">Copy those SPNs to register against the service account.</span></span> <span data-ttu-id="99468-177">To do this:</span><span class="sxs-lookup"><span data-stu-id="99468-177">To do this:</span></span>

1. <span data-ttu-id="99468-178">Browse to the site with the SPN from another machine.</span><span class="sxs-lookup"><span data-stu-id="99468-178">Browse to the site with the SPN from another machine.</span></span>
 <span data-ttu-id="99468-179">When you do, the relevant set of Kerberos tickets is cached on the machine.</span><span class="sxs-lookup"><span data-stu-id="99468-179">When you do, the relevant set of Kerberos tickets is cached on the machine.</span></span> <span data-ttu-id="99468-180">These tickets contain the SPN of the target site that you browsed to.</span><span class="sxs-lookup"><span data-stu-id="99468-180">These tickets contain the SPN of the target site that you browsed to.</span></span>

2. <span data-ttu-id="99468-181">You can pull the SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span><span class="sxs-lookup"><span data-stu-id="99468-181">You can pull the SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span></span> <span data-ttu-id="99468-182">In a command window that's running in the same context as the user who accessed the site in the browser, run the following command:</span><span class="sxs-lookup"><span data-stu-id="99468-182">In a command window that's running in the same context as the user who accessed the site in the browser, run the following command:</span></span>
```
Klist
```
<span data-ttu-id="99468-183">Klist then returns the set of target SPNs.</span><span class="sxs-lookup"><span data-stu-id="99468-183">Klist then returns the set of target SPNs.</span></span> <span data-ttu-id="99468-184">In this example, the highlighted value is the SPN that's needed:</span><span class="sxs-lookup"><span data-stu-id="99468-184">In this example, the highlighted value is the SPN that's needed:</span></span>

  ![Example Klist results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. <span data-ttu-id="99468-186">Now that you have the SPN, you need to make sure that it's configured correctly on the service account that you set up for the web application earlier.</span><span class="sxs-lookup"><span data-stu-id="99468-186">Now that you have the SPN, you need to make sure that it's configured correctly on the service account that you set up for the web application earlier.</span></span> <span data-ttu-id="99468-187">Run the following command from the command prompt as an administrator of the domain:</span><span class="sxs-lookup"><span data-stu-id="99468-187">Run the following command from the command prompt as an administrator of the domain:</span></span>

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 <span data-ttu-id="99468-188">This command sets the SPN for the SharePoint service account running as _demo\sp_svc_.</span><span class="sxs-lookup"><span data-stu-id="99468-188">This command sets the SPN for the SharePoint service account running as _demo\sp_svc_.</span></span>

 <span data-ttu-id="99468-189">Replace _http/sharepoint.demo.o365identity.us_ with the SPN for your server and _demo\sp_svc_ with the service account in your environment.</span><span class="sxs-lookup"><span data-stu-id="99468-189">Replace _http/sharepoint.demo.o365identity.us_ with the SPN for your server and _demo\sp_svc_ with the service account in your environment.</span></span> <span data-ttu-id="99468-190">The Setspn command will search for the SPN before it adds it.</span><span class="sxs-lookup"><span data-stu-id="99468-190">The Setspn command will search for the SPN before it adds it.</span></span> <span data-ttu-id="99468-191">In this case, you might see a **Duplicate SPN Value** error.</span><span class="sxs-lookup"><span data-stu-id="99468-191">In this case, you might see a **Duplicate SPN Value** error.</span></span> <span data-ttu-id="99468-192">If you see this error, make sure that the value is associated with the service account.</span><span class="sxs-lookup"><span data-stu-id="99468-192">If you see this error, make sure that the value is associated with the service account.</span></span>

<span data-ttu-id="99468-193">You can verify that the SPN was added by running the Setspn command with the -l option.</span><span class="sxs-lookup"><span data-stu-id="99468-193">You can verify that the SPN was added by running the Setspn command with the -l option.</span></span> <span data-ttu-id="99468-194">To learn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span><span class="sxs-lookup"><span data-stu-id="99468-194">To learn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span></span>

### <a name="ensure-that-the-connector-is-set-as-a-trusted-delegate-to-sharepoint"></a><span data-ttu-id="99468-195">Ensure that the connector is set as a trusted delegate to SharePoint</span><span class="sxs-lookup"><span data-stu-id="99468-195">Ensure that the connector is set as a trusted delegate to SharePoint</span></span>

<span data-ttu-id="99468-196">Configure the KCD so that the Azure AD Application Proxy service can delegate user identities to the SharePoint service.</span><span class="sxs-lookup"><span data-stu-id="99468-196">Configure the KCD so that the Azure AD Application Proxy service can delegate user identities to the SharePoint service.</span></span> <span data-ttu-id="99468-197">You do this by enabling the Application Proxy connector to retrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99468-197">You do this by enabling the Application Proxy connector to retrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span></span> <span data-ttu-id="99468-198">Then that server will pass the context to the target application, or SharePoint in this case.</span><span class="sxs-lookup"><span data-stu-id="99468-198">Then that server will pass the context to the target application, or SharePoint in this case.</span></span>

<span data-ttu-id="99468-199">To configure the KCD, repeat the following steps for each connector machine:</span><span class="sxs-lookup"><span data-stu-id="99468-199">To configure the KCD, repeat the following steps for each connector machine:</span></span>

1. <span data-ttu-id="99468-200">Log in as a domain administrator to a DC, and then open **Active Directory Users and Computers**.</span><span class="sxs-lookup"><span data-stu-id="99468-200">Log in as a domain administrator to a DC, and then open **Active Directory Users and Computers**.</span></span>
2. <span data-ttu-id="99468-201">Find the computer that the connector is running on.</span><span class="sxs-lookup"><span data-stu-id="99468-201">Find the computer that the connector is running on.</span></span> <span data-ttu-id="99468-202">In this example, it's the same SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="99468-202">In this example, it's the same SharePoint server.</span></span>
3. <span data-ttu-id="99468-203">Double-click the computer, and then click the **Delegation** tab.</span><span class="sxs-lookup"><span data-stu-id="99468-203">Double-click the computer, and then click the **Delegation** tab.</span></span>
4. <span data-ttu-id="99468-204">Ensure that the delegation settings are set to **Trust this computer for delegation to the specified services only**, and then select **Use any authentication protocol**.</span><span class="sxs-lookup"><span data-stu-id="99468-204">Ensure that the delegation settings are set to **Trust this computer for delegation to the specified services only**, and then select **Use any authentication protocol**.</span></span>

  ![Delegation settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. <span data-ttu-id="99468-206">Click the **Add** button, click **Users or Computers**, and locate the service account.</span><span class="sxs-lookup"><span data-stu-id="99468-206">Click the **Add** button, click **Users or Computers**, and locate the service account.</span></span>

  ![Adding the SPN for the service account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. <span data-ttu-id="99468-208">In the list of SPNs, select the one that you created earlier for the service account.</span><span class="sxs-lookup"><span data-stu-id="99468-208">In the list of SPNs, select the one that you created earlier for the service account.</span></span>
7. <span data-ttu-id="99468-209">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="99468-209">Click **OK**.</span></span> <span data-ttu-id="99468-210">Click **OK** again to save the changes.</span><span class="sxs-lookup"><span data-stu-id="99468-210">Click **OK** again to save the changes.</span></span>

## <a name="step-2-enable-remote-access-to-sharepoint"></a><span data-ttu-id="99468-211">Step 2: Enable remote access to SharePoint</span><span class="sxs-lookup"><span data-stu-id="99468-211">Step 2: Enable remote access to SharePoint</span></span>

<span data-ttu-id="99468-212">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready to set up single sign-on to SharePoint.</span><span class="sxs-lookup"><span data-stu-id="99468-212">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready to set up single sign-on to SharePoint.</span></span> <span data-ttu-id="99468-213">Then from the connector, you can publish the SharePoint farm for remote access through Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="99468-213">Then from the connector, you can publish the SharePoint farm for remote access through Azure AD Application Proxy.</span></span>

<span data-ttu-id="99468-214">To perform the following steps, you need to be a member of the Global Administrator Role in your organization's Azure Active Directory account.</span><span class="sxs-lookup"><span data-stu-id="99468-214">To perform the following steps, you need to be a member of the Global Administrator Role in your organization's Azure Active Directory account.</span></span>

1. <span data-ttu-id="99468-215">Sign in to the [Azure portal](https://manage.windowsazure.com) and find your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="99468-215">Sign in to the [Azure portal](https://manage.windowsazure.com) and find your Azure AD tenant.</span></span>
2. <span data-ttu-id="99468-216">Click **Applications**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="99468-216">Click **Applications**, and then click **Add**.</span></span>
3. <span data-ttu-id="99468-217">Select **Publish an application that will be accessible from outside your network**.</span><span class="sxs-lookup"><span data-stu-id="99468-217">Select **Publish an application that will be accessible from outside your network**.</span></span> <span data-ttu-id="99468-218">If you don’t see this option, make sure that you have Azure AD Basic or Premium set up in the tenant.</span><span class="sxs-lookup"><span data-stu-id="99468-218">If you don’t see this option, make sure that you have Azure AD Basic or Premium set up in the tenant.</span></span>
4. <span data-ttu-id="99468-219">Complete each of the options as follows:</span><span class="sxs-lookup"><span data-stu-id="99468-219">Complete each of the options as follows:</span></span>
 * <span data-ttu-id="99468-220">**Name**: Use any value that you want--for example, **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="99468-220">**Name**: Use any value that you want--for example, **SharePoint**.</span></span>
 * <span data-ttu-id="99468-221">**Internal URL**: This is the URL of the SharePoint site internally, such as **https://SharePoint/**.</span><span class="sxs-lookup"><span data-stu-id="99468-221">**Internal URL**: This is the URL of the SharePoint site internally, such as **https://SharePoint/**.</span></span> <span data-ttu-id="99468-222">In this example, make sure to use **https**.</span><span class="sxs-lookup"><span data-stu-id="99468-222">In this example, make sure to use **https**.</span></span>
 * <span data-ttu-id="99468-223">**Preauthentication Method**: Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99468-223">**Preauthentication Method**: Select **Azure Active Directory**.</span></span>

  ![Options for adding an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. <span data-ttu-id="99468-225">After the app is published, click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="99468-225">After the app is published, click the **Configure** tab.</span></span>
6. <span data-ttu-id="99468-226">Scroll down to the option **Translate URL in Headers**.</span><span class="sxs-lookup"><span data-stu-id="99468-226">Scroll down to the option **Translate URL in Headers**.</span></span> <span data-ttu-id="99468-227">The default value is **YES**.</span><span class="sxs-lookup"><span data-stu-id="99468-227">The default value is **YES**.</span></span> <span data-ttu-id="99468-228">Change it to **NO**.</span><span class="sxs-lookup"><span data-stu-id="99468-228">Change it to **NO**.</span></span>

 <span data-ttu-id="99468-229">SharePoint uses the _Host Header_ value to look up the site.</span><span class="sxs-lookup"><span data-stu-id="99468-229">SharePoint uses the _Host Header_ value to look up the site.</span></span> <span data-ttu-id="99468-230">It also generates links based on this value.</span><span class="sxs-lookup"><span data-stu-id="99468-230">It also generates links based on this value.</span></span> <span data-ttu-id="99468-231">The net effect is to make sure that any link that SharePoint generates is a published URL that is correctly set to use the external URL.</span><span class="sxs-lookup"><span data-stu-id="99468-231">The net effect is to make sure that any link that SharePoint generates is a published URL that is correctly set to use the external URL.</span></span> <span data-ttu-id="99468-232">Setting the value to **YES** also enables the connector to forward the request to the back-end application.</span><span class="sxs-lookup"><span data-stu-id="99468-232">Setting the value to **YES** also enables the connector to forward the request to the back-end application.</span></span> <span data-ttu-id="99468-233">However, setting the value to **NO** means that the connector will not send the internal host name.</span><span class="sxs-lookup"><span data-stu-id="99468-233">However, setting the value to **NO** means that the connector will not send the internal host name.</span></span> <span data-ttu-id="99468-234">Instead, the connector will send the host header as the published URL to the back-end application.</span><span class="sxs-lookup"><span data-stu-id="99468-234">Instead, the connector will send the host header as the published URL to the back-end application.</span></span>

 <span data-ttu-id="99468-235">Also, to ensure that SharePoint accepts this URL, you need to complete one more configurations on the SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="99468-235">Also, to ensure that SharePoint accepts this URL, you need to complete one more configurations on the SharePoint server.</span></span> <span data-ttu-id="99468-236">You'll do that in the next section.</span><span class="sxs-lookup"><span data-stu-id="99468-236">You'll do that in the next section.</span></span>

7. <span data-ttu-id="99468-237">Change **Internal Authentication Method** to **Integrated Windows Authentication**.</span><span class="sxs-lookup"><span data-stu-id="99468-237">Change **Internal Authentication Method** to **Integrated Windows Authentication**.</span></span> <span data-ttu-id="99468-238">If your Azure AD tenant uses a UPN in the cloud that's different from the UPN on-premises, remember to update **Delegated Login Identity** as well.</span><span class="sxs-lookup"><span data-stu-id="99468-238">If your Azure AD tenant uses a UPN in the cloud that's different from the UPN on-premises, remember to update **Delegated Login Identity** as well.</span></span>
8. <span data-ttu-id="99468-239">Set **Internal Application SPN** to the value that you set earlier.</span><span class="sxs-lookup"><span data-stu-id="99468-239">Set **Internal Application SPN** to the value that you set earlier.</span></span> <span data-ttu-id="99468-240">For example, use **http/sharepoint.demo.o365identity.us**.</span><span class="sxs-lookup"><span data-stu-id="99468-240">For example, use **http/sharepoint.demo.o365identity.us**.</span></span>
9. <span data-ttu-id="99468-241">Assign the application to your target users.</span><span class="sxs-lookup"><span data-stu-id="99468-241">Assign the application to your target users.</span></span>

<span data-ttu-id="99468-242">Your application should look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="99468-242">Your application should look similar to the following:</span></span>

  ![Finished application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-the-external-url"></a><span data-ttu-id="99468-244">Step 3: Ensure that SharePoint knows about the external URL</span><span class="sxs-lookup"><span data-stu-id="99468-244">Step 3: Ensure that SharePoint knows about the external URL</span></span>

<span data-ttu-id="99468-245">Your last step to ensure that SharePoint can find the site based on the external URL, so that it will render links based on that external URL.</span><span class="sxs-lookup"><span data-stu-id="99468-245">Your last step to ensure that SharePoint can find the site based on the external URL, so that it will render links based on that external URL.</span></span> <span data-ttu-id="99468-246">You do this by configuring alternate access mappings for the SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="99468-246">You do this by configuring alternate access mappings for the SharePoint site.</span></span>

1. <span data-ttu-id="99468-247">Open the **SharePoint 2013 Central Administration** site.</span><span class="sxs-lookup"><span data-stu-id="99468-247">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="99468-248">Under **System Settings**, select **Configure Alternate Access Mappings**.</span><span class="sxs-lookup"><span data-stu-id="99468-248">Under **System Settings**, select **Configure Alternate Access Mappings**.</span></span>

 <span data-ttu-id="99468-249">This opens the **Alternate Access Mappings** box.</span><span class="sxs-lookup"><span data-stu-id="99468-249">This opens the **Alternate Access Mappings** box.</span></span>

  ![Alternate Access Mappings box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. <span data-ttu-id="99468-251">In the drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span><span class="sxs-lookup"><span data-stu-id="99468-251">In the drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span></span>
4. <span data-ttu-id="99468-252">Select your site--for example, **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="99468-252">Select your site--for example, **SharePoint - 80**.</span></span>

  ![Selecting a site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. <span data-ttu-id="99468-254">You can choose to add the published URL as either an internal URL or a public URL.</span><span class="sxs-lookup"><span data-stu-id="99468-254">You can choose to add the published URL as either an internal URL or a public URL.</span></span> <span data-ttu-id="99468-255">This example uses a public URL as the extranet.</span><span class="sxs-lookup"><span data-stu-id="99468-255">This example uses a public URL as the extranet.</span></span>
6. <span data-ttu-id="99468-256">Click **Edit Public URLs** in the **Extranet** path, and then enter the path for the published application, as in the previous step.</span><span class="sxs-lookup"><span data-stu-id="99468-256">Click **Edit Public URLs** in the **Extranet** path, and then enter the path for the published application, as in the previous step.</span></span> <span data-ttu-id="99468-257">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span><span class="sxs-lookup"><span data-stu-id="99468-257">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span></span>

  ![Entering the path](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. <span data-ttu-id="99468-259">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="99468-259">Click **Save**.</span></span>

 <span data-ttu-id="99468-260">You can now access the SharePoint site externally via Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="99468-260">You can now access the SharePoint site externally via Azure AD Application Proxy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99468-261">Next steps</span><span class="sxs-lookup"><span data-stu-id="99468-261">Next steps</span></span>

- [<span data-ttu-id="99468-262">How to provide secure remote access to on-premises applications</span><span class="sxs-lookup"><span data-stu-id="99468-262">How to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- [<span data-ttu-id="99468-263">Understand Azure AD Application Proxy connectors</span><span class="sxs-lookup"><span data-stu-id="99468-263">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
- [<span data-ttu-id="99468-264">Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="99468-264">Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy</span></span>](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)











