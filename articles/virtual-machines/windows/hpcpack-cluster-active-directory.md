---
title: HPC Pack cluster with Azure Active Directory | Microsoft Docs
description: Learn how to integrate an HPC Pack 2016 cluster in Azure with Azure Active Directory
services: virtual-machines-windows
documentationcenter: ''
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 88896a4636b1cd95627480deec3cac1a5f797315
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564153"
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="a0223-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0223-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="a0223-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="a0223-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="a0223-105">Follow the steps in this article for the following high level tasks:</span><span class="sxs-lookup"><span data-stu-id="a0223-105">Follow the steps in this article for the following high level tasks:</span></span> 
* <span data-ttu-id="a0223-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="a0223-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="a0223-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="a0223-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="a0223-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps to integrate other applications and services.</span><span class="sxs-lookup"><span data-stu-id="a0223-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps to integrate other applications and services.</span></span> <span data-ttu-id="a0223-109">This article assumes you are familiar with basic user management in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0223-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="a0223-110">For more information and background, see the [Azure Active Directory documentation](../../active-directory/index.md) and the following section.</span><span class="sxs-lookup"><span data-stu-id="a0223-110">For more information and background, see the [Azure Active Directory documentation](../../active-directory/index.md) and the following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="a0223-111">Benefits of integration</span><span class="sxs-lookup"><span data-stu-id="a0223-111">Benefits of integration</span></span>


<span data-ttu-id="a0223-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access to cloud solutions.</span><span class="sxs-lookup"><span data-stu-id="a0223-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access to cloud solutions.</span></span>

<span data-ttu-id="a0223-113">Integration of an HPC Pack cluster with Azure AD can help you achieve the following goals:</span><span class="sxs-lookup"><span data-stu-id="a0223-113">Integration of an HPC Pack cluster with Azure AD can help you achieve the following goals:</span></span>

* <span data-ttu-id="a0223-114">Remove the traditional Active Directory domain controller from the HPC Pack cluster.</span><span class="sxs-lookup"><span data-stu-id="a0223-114">Remove the traditional Active Directory domain controller from the HPC Pack cluster.</span></span> <span data-ttu-id="a0223-115">This can help reduce the costs of maintaining the cluster if this is not necessary for your business, and speed-up the deployment process.</span><span class="sxs-lookup"><span data-stu-id="a0223-115">This can help reduce the costs of maintaining the cluster if this is not necessary for your business, and speed-up the deployment process.</span></span>
* <span data-ttu-id="a0223-116">Leverage the following benefits that are brought by Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a0223-116">Leverage the following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="a0223-117">Single sign-on</span><span class="sxs-lookup"><span data-stu-id="a0223-117">Single sign-on</span></span> 
    *   <span data-ttu-id="a0223-118">Using a local AD identity for the HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="a0223-118">Using a local AD identity for the HPC Pack cluster in Azure</span></span> 

    ![Azure Active Directory environment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="a0223-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a0223-120">Prerequisites</span></span>
* <span data-ttu-id="a0223-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a0223-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="a0223-122">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="a0223-122">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a0223-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="a0223-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="a0223-124">**Client computer** - You need a Windows or Windows Server client computer to  run HPC Pack client utilities.</span><span class="sxs-lookup"><span data-stu-id="a0223-124">**Client computer** - You need a Windows or Windows Server client computer to  run HPC Pack client utilities.</span></span> <span data-ttu-id="a0223-125">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span><span class="sxs-lookup"><span data-stu-id="a0223-125">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="a0223-126">**HPC Pack client utilities** - Install the HPC Pack client utilities on the client computer, using the free installation package available from the Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="a0223-126">**HPC Pack client utilities** - Install the HPC Pack client utilities on the client computer, using the free installation package available from the Microsoft Download Center.</span></span>


## <a name="step-1-register-the-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="a0223-127">Step 1: Register the HPC cluster server with your Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="a0223-127">Step 1: Register the HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="a0223-128">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a0223-128">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a0223-129">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span><span class="sxs-lookup"><span data-stu-id="a0223-129">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="a0223-130">You must have permission to access resources in the directory.</span><span class="sxs-lookup"><span data-stu-id="a0223-130">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="a0223-131">Click **Users**, and make sure there are user accounts already created or configured.</span><span class="sxs-lookup"><span data-stu-id="a0223-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="a0223-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span><span class="sxs-lookup"><span data-stu-id="a0223-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="a0223-133">Enter the following information in the wizard:</span><span class="sxs-lookup"><span data-stu-id="a0223-133">Enter the following information in the wizard:</span></span>
    * <span data-ttu-id="a0223-134">**Name** - HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="a0223-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="a0223-135">**Type** - Select **Web Application and/or Web API**</span><span class="sxs-lookup"><span data-stu-id="a0223-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="a0223-136">**Sign-on URL**- The base URL for the sample, which is by default `https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="a0223-136">**Sign-on URL**- The base URL for the sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="a0223-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="a0223-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="a0223-138">Replace `<Directory_name`> with the full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with the name you chose previously.</span><span class="sxs-lookup"><span data-stu-id="a0223-138">Replace `<Directory_name`> with the full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with the name you chose previously.</span></span>

5. <span data-ttu-id="a0223-139">After the app is added, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="a0223-139">After the app is added, click **Configure**.</span></span> <span data-ttu-id="a0223-140">Configure the following properties:</span><span class="sxs-lookup"><span data-stu-id="a0223-140">Configure the following properties:</span></span>
    * <span data-ttu-id="a0223-141">Select **Yes** for **Application is multi-tenant**</span><span class="sxs-lookup"><span data-stu-id="a0223-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="a0223-142">Select **Yes** for **User assignment required to access app**.</span><span class="sxs-lookup"><span data-stu-id="a0223-142">Select **Yes** for **User assignment required to access app**.</span></span>

6. <span data-ttu-id="a0223-143">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a0223-143">Click **Save**.</span></span> <span data-ttu-id="a0223-144">When saving completes, click **Manage Manifest**.</span><span class="sxs-lookup"><span data-stu-id="a0223-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="a0223-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span><span class="sxs-lookup"><span data-stu-id="a0223-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="a0223-146">Edit the downloaded manifest by locating the `appRoles` setting and adding the following application role:</span><span class="sxs-lookup"><span data-stu-id="a0223-146">Edit the downloaded manifest by locating the `appRoles` setting and adding the following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="a0223-147">Save the file.</span><span class="sxs-lookup"><span data-stu-id="a0223-147">Save the file.</span></span> <span data-ttu-id="a0223-148">Then in the portal, click **Manage Manifest** > **Upload Manifest**.</span><span class="sxs-lookup"><span data-stu-id="a0223-148">Then in the portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="a0223-149">You can then upload the edited manifest.</span><span class="sxs-lookup"><span data-stu-id="a0223-149">You can then upload the edited manifest.</span></span>
8. <span data-ttu-id="a0223-150">Click **Users**, select a user, and then click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="a0223-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="a0223-151">Assign one of the available roles (HpcUsers or HpcAdminMirror) to the user.</span><span class="sxs-lookup"><span data-stu-id="a0223-151">Assign one of the available roles (HpcUsers or HpcAdminMirror) to the user.</span></span> <span data-ttu-id="a0223-152">Repeat this step with additional users in the directory.</span><span class="sxs-lookup"><span data-stu-id="a0223-152">Repeat this step with additional users in the directory.</span></span> <span data-ttu-id="a0223-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="a0223-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="a0223-154">To manage users, we recommend using the Azure Active Directory preview blade in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a0223-154">To manage users, we recommend using the Azure Active Directory preview blade in the [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-the-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="a0223-155">Step 2: Register the HPC cluster client with your Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="a0223-155">Step 2: Register the HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="a0223-156">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a0223-156">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a0223-157">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span><span class="sxs-lookup"><span data-stu-id="a0223-157">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="a0223-158">You must have permission to access resources in the directory.</span><span class="sxs-lookup"><span data-stu-id="a0223-158">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="a0223-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span><span class="sxs-lookup"><span data-stu-id="a0223-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="a0223-160">Enter the following information in the wizard:</span><span class="sxs-lookup"><span data-stu-id="a0223-160">Enter the following information in the wizard:</span></span>

    * <span data-ttu-id="a0223-161">**Name** - HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="a0223-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="a0223-162">**Type** - Select **Native Client Application**</span><span class="sxs-lookup"><span data-stu-id="a0223-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="a0223-163">**Redirect URI** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="a0223-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="a0223-164">After the app is added, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="a0223-164">After the app is added, click **Configure**.</span></span> <span data-ttu-id="a0223-165">Copy the **Client ID** value and save it.</span><span class="sxs-lookup"><span data-stu-id="a0223-165">Copy the **Client ID** value and save it.</span></span> <span data-ttu-id="a0223-166">You need this later when configuring your application.</span><span class="sxs-lookup"><span data-stu-id="a0223-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="a0223-167">In **Permissions to other applications**, click **Add Application**.</span><span class="sxs-lookup"><span data-stu-id="a0223-167">In **Permissions to other applications**, click **Add Application**.</span></span> <span data-ttu-id="a0223-168">Search and add the  HpcPackClusterServer application (created in Step 1).</span><span class="sxs-lookup"><span data-stu-id="a0223-168">Search and add the  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="a0223-169">In the **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span><span class="sxs-lookup"><span data-stu-id="a0223-169">In the **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="a0223-170">Then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a0223-170">Then click **Save**.</span></span>


## <a name="step-3-configure-the-hpc-cluster"></a><span data-ttu-id="a0223-171">Step 3: Configure the HPC cluster</span><span class="sxs-lookup"><span data-stu-id="a0223-171">Step 3: Configure the HPC cluster</span></span>

1. <span data-ttu-id="a0223-172">Connect to the HPC Pack 2016 head node in Azure.</span><span class="sxs-lookup"><span data-stu-id="a0223-172">Connect to the HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="a0223-173">Start HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0223-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="a0223-174">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="a0223-174">Run the following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="a0223-175">where</span><span class="sxs-lookup"><span data-stu-id="a0223-175">where</span></span>

    * <span data-ttu-id="a0223-176">`AADTenant` specifies the Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="a0223-176">`AADTenant` specifies the Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="a0223-177">`AADClientAppId` specifies the client ID for the app created in Step 2.</span><span class="sxs-lookup"><span data-stu-id="a0223-177">`AADClientAppId` specifies the client ID for the app created in Step 2.</span></span>

4. <span data-ttu-id="a0223-178">Restart the HpcSchedulerStateful service.</span><span class="sxs-lookup"><span data-stu-id="a0223-178">Restart the HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="a0223-179">In a cluster with multiple head nodes, you can run the following PowerShell commands on the head node to switch the primary replica for the HpcSchedulerStateful service:</span><span class="sxs-lookup"><span data-stu-id="a0223-179">In a cluster with multiple head nodes, you can run the following PowerShell commands on the head node to switch the primary replica for the HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-the-client"></a><span data-ttu-id="a0223-180">Step 4: Manage and submit jobs from the client</span><span class="sxs-lookup"><span data-stu-id="a0223-180">Step 4: Manage and submit jobs from the client</span></span>

<span data-ttu-id="a0223-181">To install the HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from the Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="a0223-181">To install the HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from the Microsoft Download Center.</span></span> <span data-ttu-id="a0223-182">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span><span class="sxs-lookup"><span data-stu-id="a0223-182">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="a0223-183">To prepare the client computer, install the certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on the client computer.</span><span class="sxs-lookup"><span data-stu-id="a0223-183">To prepare the client computer, install the certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on the client computer.</span></span> <span data-ttu-id="a0223-184">Use standard Windows certificate management procedures to install the public certificate to the **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span><span class="sxs-lookup"><span data-stu-id="a0223-184">Use standard Windows certificate management procedures to install the public certificate to the **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="a0223-185">You can now run the HPC Pack commands or use the HPC Pack Job manager GUI to submit and manage cluster jobs by using the Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="a0223-185">You can now run the HPC Pack commands or use the HPC Pack Job manager GUI to submit and manage cluster jobs by using the Azure AD account.</span></span> <span data-ttu-id="a0223-186">For job submission options, see [Submit HPC jobs to an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="a0223-186">For job submission options, see [Submit HPC jobs to an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="a0223-187">When you try to connect to the HPC Pack cluster in Azure for the first time, a popup windows appears.</span><span class="sxs-lookup"><span data-stu-id="a0223-187">When you try to connect to the HPC Pack cluster in Azure for the first time, a popup windows appears.</span></span> <span data-ttu-id="a0223-188">Enter your Azure AD credentials to log in.</span><span class="sxs-lookup"><span data-stu-id="a0223-188">Enter your Azure AD credentials to log in.</span></span> <span data-ttu-id="a0223-189">The token is then cached.</span><span class="sxs-lookup"><span data-stu-id="a0223-189">The token is then cached.</span></span> <span data-ttu-id="a0223-190">Later connections to the cluster in Azure use the cached token unless authentication changes or the cached is cleared.</span><span class="sxs-lookup"><span data-stu-id="a0223-190">Later connections to the cluster in Azure use the cached token unless authentication changes or the cached is cleared.</span></span>
>
  
<span data-ttu-id="a0223-191">For example, after completing the previous steps, you can query for jobs from an on-premises client as follows:</span><span class="sxs-lookup"><span data-stu-id="a0223-191">For example, after completing the previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="a0223-192">Useful cmdlets for job submission with Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="a0223-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-the-local-token-cache"></a><span data-ttu-id="a0223-193">Manage the local token cache</span><span class="sxs-lookup"><span data-stu-id="a0223-193">Manage the local token cache</span></span>

<span data-ttu-id="a0223-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets to manage the local token cache.</span><span class="sxs-lookup"><span data-stu-id="a0223-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets to manage the local token cache.</span></span> <span data-ttu-id="a0223-195">These cmdlets are useful for submitting jobs non-interactively.</span><span class="sxs-lookup"><span data-stu-id="a0223-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="a0223-196">See the following example:</span><span class="sxs-lookup"><span data-stu-id="a0223-196">See the following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-the-credentials-for-submitting-jobs-using-the-azure-ad-account"></a><span data-ttu-id="a0223-197">Set the credentials for submitting jobs using the Azure AD account</span><span class="sxs-lookup"><span data-stu-id="a0223-197">Set the credentials for submitting jobs using the Azure AD account</span></span> 

<span data-ttu-id="a0223-198">Sometimes, you may want to run the job under the HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on the head node).</span><span class="sxs-lookup"><span data-stu-id="a0223-198">Sometimes, you may want to run the job under the HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on the head node).</span></span>

1. <span data-ttu-id="a0223-199">Use the following commands to set the credentials:</span><span class="sxs-lookup"><span data-stu-id="a0223-199">Use the following commands to set the credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="a0223-200">Then submit the job as follows.</span><span class="sxs-lookup"><span data-stu-id="a0223-200">Then submit the job as follows.</span></span> <span data-ttu-id="a0223-201">The job/task runs under $localUser on the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="a0223-201">The job/task runs under $localUser on the compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="a0223-202">If `–Credential` is not specified with `Submit-HpcJob`, the job or task runs under a local mapped user as the Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="a0223-202">If `–Credential` is not specified with `Submit-HpcJob`, the job or task runs under a local mapped user as the Azure AD account.</span></span> <span data-ttu-id="a0223-203">(The HPC cluster creates a local user with the same name as the Azure AD account to run the task.)</span><span class="sxs-lookup"><span data-stu-id="a0223-203">(The HPC cluster creates a local user with the same name as the Azure AD account to run the task.)</span></span>
    
3. <span data-ttu-id="a0223-204">Set extended data for the Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="a0223-204">Set extended data for the Azure AD account.</span></span> <span data-ttu-id="a0223-205">This is useful when running an MPI job on Linux nodes using the Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="a0223-205">This is useful when running an MPI job on Linux nodes using the Azure AD account.</span></span>

   * <span data-ttu-id="a0223-206">Set extended data for the Azure AD account itself</span><span class="sxs-lookup"><span data-stu-id="a0223-206">Set extended data for the Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="a0223-207">Set extended data and run as HPC cluster user</span><span class="sxs-lookup"><span data-stu-id="a0223-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```


