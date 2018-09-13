---
title: Enable Remote Desktop in an Azure Cloud Service | Microsoft Docs
description: How to configure your azure cloud service application to allow remote desktop connections
services: cloud-services
documentationcenter: ''
author: thraka
manager: timlt
editor: ''
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 1e513b9e39c49d9f4d68146e795d3deac2b8bd52
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540972"
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="05230-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="05230-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Azure classic portal](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="05230-108">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span><span class="sxs-lookup"><span data-stu-id="05230-108">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="05230-109">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span><span class="sxs-lookup"><span data-stu-id="05230-109">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-classic-portal"></a><span data-ttu-id="05230-110">Configure Remote Desktop from the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="05230-110">Configure Remote Desktop from the Azure classic portal</span></span>
<span data-ttu-id="05230-111">The Azure classic portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span><span class="sxs-lookup"><span data-stu-id="05230-111">The Azure classic portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="05230-112">The **Configure** page for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span><span class="sxs-lookup"><span data-stu-id="05230-112">The **Configure** page for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="05230-113">Click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="05230-113">Click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="05230-114">Click the **Remote** button at the bottom.</span><span class="sxs-lookup"><span data-stu-id="05230-114">Click the **Remote** button at the bottom.</span></span>

    ![Cloud services remote](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark). To prevent a reboot, the certificate used to encrypt the password must be installed on the role. To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.

3. <span data-ttu-id="05230-119">In **Roles**, select the role you want to update or select **All** for all roles.</span><span class="sxs-lookup"><span data-stu-id="05230-119">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>
4. <span data-ttu-id="05230-120">Make any of the following changes:</span><span class="sxs-lookup"><span data-stu-id="05230-120">Make any of the following changes:</span></span>

   * <span data-ttu-id="05230-121">To enable Remote Desktop, select the **Enable Remote Desktop** check box.</span><span class="sxs-lookup"><span data-stu-id="05230-121">To enable Remote Desktop, select the **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="05230-122">To disable Remote Desktop, clear the check box.</span><span class="sxs-lookup"><span data-stu-id="05230-122">To disable Remote Desktop, clear the check box.</span></span>
   * <span data-ttu-id="05230-123">Create an account to use in Remote Desktop connections to the role instances.</span><span class="sxs-lookup"><span data-stu-id="05230-123">Create an account to use in Remote Desktop connections to the role instances.</span></span>
   * <span data-ttu-id="05230-124">Update the password for the existing account.</span><span class="sxs-lookup"><span data-stu-id="05230-124">Update the password for the existing account.</span></span>
   * <span data-ttu-id="05230-125">Select an uploaded certificate to use for authentication (upload the certificate using **Upload** on the **Certificates** page) or create a new certificate.</span><span class="sxs-lookup"><span data-stu-id="05230-125">Select an uploaded certificate to use for authentication (upload the certificate using **Upload** on the **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="05230-126">Change the expiration date for the Remote Desktop configuration.</span><span class="sxs-lookup"><span data-stu-id="05230-126">Change the expiration date for the Remote Desktop configuration.</span></span>

5. <span data-ttu-id="05230-127">When you finish your configuration updates, click **OK** (checkmark).</span><span class="sxs-lookup"><span data-stu-id="05230-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="05230-128">Remote into role instances</span><span class="sxs-lookup"><span data-stu-id="05230-128">Remote into role instances</span></span>
<span data-ttu-id="05230-129">Once Remote Desktop is enabled on the roles you can remote into a role instance through various tools.</span><span class="sxs-lookup"><span data-stu-id="05230-129">Once Remote Desktop is enabled on the roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="05230-130">To connect to a role instance from the Azure classic portal:</span><span class="sxs-lookup"><span data-stu-id="05230-130">To connect to a role instance from the Azure classic portal:</span></span>

1. <span data-ttu-id="05230-131">Click **Instances** to open the **Instances** page.</span><span class="sxs-lookup"><span data-stu-id="05230-131">Click **Instances** to open the **Instances** page.</span></span>
2. <span data-ttu-id="05230-132">Select a role instance that has Remote Desktop configured.</span><span class="sxs-lookup"><span data-stu-id="05230-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="05230-133">Click **Connect**, and follow the instructions to open the desktop.</span><span class="sxs-lookup"><span data-stu-id="05230-133">Click **Connect**, and follow the instructions to open the desktop.</span></span>
4. <span data-ttu-id="05230-134">Click **Open** and then **Connect** to start the Remote Desktop connection.</span><span class="sxs-lookup"><span data-stu-id="05230-134">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

### <a name="use-visual-studio-to-remote-into-a-role-instance"></a><span data-ttu-id="05230-135">Use Visual Studio to remote into a role instance</span><span class="sxs-lookup"><span data-stu-id="05230-135">Use Visual Studio to remote into a role instance</span></span>
<span data-ttu-id="05230-136">In Visual Studio, Server Explorer:</span><span class="sxs-lookup"><span data-stu-id="05230-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="05230-137">Expand the **Azure** > **Cloud Services** > **[cloud service name]** node.</span><span class="sxs-lookup"><span data-stu-id="05230-137">Expand the **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="05230-138">Expand either **Staging** or **Production**.</span><span class="sxs-lookup"><span data-stu-id="05230-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="05230-139">Expand the individual role.</span><span class="sxs-lookup"><span data-stu-id="05230-139">Expand the individual role.</span></span>
4. <span data-ttu-id="05230-140">Right-click one of the role instances, click **Connect using Remote Desktop...**, and then enter the user name and password.</span><span class="sxs-lookup"><span data-stu-id="05230-140">Right-click one of the role instances, click **Connect using Remote Desktop...**, and then enter the user name and password.</span></span>

![Server explorer remote desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-to-get-the-rdp-file"></a><span data-ttu-id="05230-142">Use PowerShell to get the RDP file</span><span class="sxs-lookup"><span data-stu-id="05230-142">Use PowerShell to get the RDP file</span></span>
<span data-ttu-id="05230-143">You can use the [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet to retrieve the RDP file.</span><span class="sxs-lookup"><span data-stu-id="05230-143">You can use the [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet to retrieve the RDP file.</span></span> <span data-ttu-id="05230-144">You can then use the RDP file with Remote Desktop Connection to access the cloud service.</span><span class="sxs-lookup"><span data-stu-id="05230-144">You can then use the RDP file with Remote Desktop Connection to access the cloud service.</span></span>

### <a name="programmatically-download-the-rdp-file-through-the-service-management-rest-api"></a><span data-ttu-id="05230-145">Programmatically download the RDP file through the Service Management REST API</span><span class="sxs-lookup"><span data-stu-id="05230-145">Programmatically download the RDP file through the Service Management REST API</span></span>
<span data-ttu-id="05230-146">You can use the [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation to download the RDP file.</span><span class="sxs-lookup"><span data-stu-id="05230-146">You can use the [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation to download the RDP file.</span></span>

## <a name="to-configure-remote-desktop-in-the-service-definition-file"></a><span data-ttu-id="05230-147">To configure Remote Desktop in the service definition file</span><span class="sxs-lookup"><span data-stu-id="05230-147">To configure Remote Desktop in the service definition file</span></span>
<span data-ttu-id="05230-148">This method allows you to enable Remote Desktop for the application during development.</span><span class="sxs-lookup"><span data-stu-id="05230-148">This method allows you to enable Remote Desktop for the application during development.</span></span> <span data-ttu-id="05230-149">This approach requires encrypted passwords be stored in your service configuration file and any updates to the remote desktop configuration would require a redeployment of the application.</span><span class="sxs-lookup"><span data-stu-id="05230-149">This approach requires encrypted passwords be stored in your service configuration file and any updates to the remote desktop configuration would require a redeployment of the application.</span></span> <span data-ttu-id="05230-150">If you want to avoid these downsides you should use the remote desktop extension based approach described above.</span><span class="sxs-lookup"><span data-stu-id="05230-150">If you want to avoid these downsides you should use the remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="05230-151">You can use Visual Studio to [enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using the service definition file approach.</span><span class="sxs-lookup"><span data-stu-id="05230-151">You can use Visual Studio to [enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using the service definition file approach.</span></span>  
<span data-ttu-id="05230-152">The steps below describe the changes needed to the service model files to enable remote desktop.</span><span class="sxs-lookup"><span data-stu-id="05230-152">The steps below describe the changes needed to the service model files to enable remote desktop.</span></span> <span data-ttu-id="05230-153">Visual Studio will automatically makes these changes when publishing.</span><span class="sxs-lookup"><span data-stu-id="05230-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-the-connection-in-the-service-model"></a><span data-ttu-id="05230-154">Set up the connection in the service model</span><span class="sxs-lookup"><span data-stu-id="05230-154">Set up the connection in the service model</span></span>
<span data-ttu-id="05230-155">Use the **Imports** element to import the **RemoteAccess** module and the **RemoteForwarder** module to the [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span><span class="sxs-lookup"><span data-stu-id="05230-155">Use the **Imports** element to import the **RemoteAccess** module and the **RemoteForwarder** module to the [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="05230-156">The service definition file should be similar to the following example with the `<Imports>` element added.</span><span class="sxs-lookup"><span data-stu-id="05230-156">The service definition file should be similar to the following example with the `<Imports>` element added.</span></span>

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
<span data-ttu-id="05230-157">The [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar to the following example, note the `<ConfigurationSettings>` and `<Certificates>` elements.</span><span class="sxs-lookup"><span data-stu-id="05230-157">The [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar to the following example, note the `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="05230-158">The Certificate specified must be [uploaded to the cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="05230-158">The Certificate specified must be [uploaded to the cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a><span data-ttu-id="05230-159">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="05230-159">Additional Resources</span></span>
<span data-ttu-id="05230-160">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md#remote-desktop)</span><span class="sxs-lookup"><span data-stu-id="05230-160">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md#remote-desktop)</span></span>


