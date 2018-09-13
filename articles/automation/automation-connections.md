---
title: Connection assets in Azure Automation
description: Connection assets in Azure Automation contain the information required to connect to an external service or application from a runbook or DSC configuration. This article explains the details of connections and how to work with them in both textual and graphical authoring.
services: automation
ms.service: automation
ms.component: shared-capabilities
author: georgewallace
ms.author: gwallace
ms.date: 03/15/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 4ead83dc449f2b32461b0585f276c9f3bfd3f847
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44771647"
---
# <a name="connection-assets-in-azure-automation"></a><span data-ttu-id="00ce8-104">Connection assets in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="00ce8-104">Connection assets in Azure Automation</span></span>

<span data-ttu-id="00ce8-105">An Automation connection asset contains the information required to connect to an external service or application from a runbook or DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="00ce8-105">An Automation connection asset contains the information required to connect to an external service or application from a runbook or DSC configuration.</span></span> <span data-ttu-id="00ce8-106">This may include information required for authentication such as a username and password in addition to connection information such as a URL or a port.</span><span class="sxs-lookup"><span data-stu-id="00ce8-106">This may include information required for authentication such as a username and password in addition to connection information such as a URL or a port.</span></span> <span data-ttu-id="00ce8-107">The value of a connection is keeping all of the properties for connecting to a particular application in one asset as opposed to creating multiple variables.</span><span class="sxs-lookup"><span data-stu-id="00ce8-107">The value of a connection is keeping all of the properties for connecting to a particular application in one asset as opposed to creating multiple variables.</span></span> <span data-ttu-id="00ce8-108">The user can edit the values for a connection in one place, and you can pass the name of a connection to a runbook or DSC configuration in a single parameter.</span><span class="sxs-lookup"><span data-stu-id="00ce8-108">The user can edit the values for a connection in one place, and you can pass the name of a connection to a runbook or DSC configuration in a single parameter.</span></span> <span data-ttu-id="00ce8-109">The properties for a connection can be accessed in the runbook or DSC configuration with the **Get-AutomationConnection** activity.</span><span class="sxs-lookup"><span data-stu-id="00ce8-109">The properties for a connection can be accessed in the runbook or DSC configuration with the **Get-AutomationConnection** activity.</span></span> 

<span data-ttu-id="00ce8-110">When you create a connection, you must specify a *connection type*.</span><span class="sxs-lookup"><span data-stu-id="00ce8-110">When you create a connection, you must specify a *connection type*.</span></span> <span data-ttu-id="00ce8-111">The connection type is a template that defines a set of properties.</span><span class="sxs-lookup"><span data-stu-id="00ce8-111">The connection type is a template that defines a set of properties.</span></span> <span data-ttu-id="00ce8-112">The connection defines values for each property defined in its connection type.</span><span class="sxs-lookup"><span data-stu-id="00ce8-112">The connection defines values for each property defined in its connection type.</span></span> <span data-ttu-id="00ce8-113">Connection types are added to Azure Automation in integration modules or created with the [Azure Automation API](http://msdn.microsoft.com/library/azure/mt163818.aspx) if the integration module includes a connection type and is imported into your Automation account.</span><span class="sxs-lookup"><span data-stu-id="00ce8-113">Connection types are added to Azure Automation in integration modules or created with the [Azure Automation API](http://msdn.microsoft.com/library/azure/mt163818.aspx) if the integration module includes a connection type and is imported into your Automation account.</span></span> <span data-ttu-id="00ce8-114">Otherwise, you will need to create a metadata file to specify an Automation connection type.</span><span class="sxs-lookup"><span data-stu-id="00ce8-114">Otherwise, you will need to create a metadata file to specify an Automation connection type.</span></span>  <span data-ttu-id="00ce8-115">For further information regarding this, see [Integration Modules](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="00ce8-115">For further information regarding this, see [Integration Modules](automation-integration-modules.md).</span></span>  

>[!NOTE]
><span data-ttu-id="00ce8-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span><span class="sxs-lookup"><span data-stu-id="00ce8-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="00ce8-117">These assets are encrypted and stored in Azure Automation using a unique key that is generated for each automation account.</span><span class="sxs-lookup"><span data-stu-id="00ce8-117">These assets are encrypted and stored in Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="00ce8-118">This key is stored in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="00ce8-118">This key is stored in Key Vault.</span></span> <span data-ttu-id="00ce8-119">Before storing a secure asset, the key is loaded from Key Vault and then used to encrypt the asset.</span><span class="sxs-lookup"><span data-stu-id="00ce8-119">Before storing a secure asset, the key is loaded from Key Vault and then used to encrypt the asset.</span></span>

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="00ce8-120">Windows PowerShell Cmdlets</span><span class="sxs-lookup"><span data-stu-id="00ce8-120">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="00ce8-121">The cmdlets in the following table are used to create and manage Automation connections with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00ce8-121">The cmdlets in the following table are used to create and manage Automation connections with Windows PowerShell.</span></span> <span data-ttu-id="00ce8-122">They ship as part of the [Azure PowerShell module](/powershell/azure/overview) which is available for use in Automation runbooks and DSC configurations.</span><span class="sxs-lookup"><span data-stu-id="00ce8-122">They ship as part of the [Azure PowerShell module](/powershell/azure/overview) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="00ce8-123">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="00ce8-123">Cmdlet</span></span>|<span data-ttu-id="00ce8-124">Description</span><span class="sxs-lookup"><span data-stu-id="00ce8-124">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="00ce8-125">Get-AzureRmAutomationConnection</span><span class="sxs-lookup"><span data-stu-id="00ce8-125">Get-AzureRmAutomationConnection</span></span>](/powershell/module/azurerm.automation/get-azurermautomationconnection)|<span data-ttu-id="00ce8-126">Retrieves a connection.</span><span class="sxs-lookup"><span data-stu-id="00ce8-126">Retrieves a connection.</span></span> <span data-ttu-id="00ce8-127">Includes a hash table with the values of the connection’s fields.</span><span class="sxs-lookup"><span data-stu-id="00ce8-127">Includes a hash table with the values of the connection’s fields.</span></span>|
|[<span data-ttu-id="00ce8-128">New-AzureRmAutomationConnection</span><span class="sxs-lookup"><span data-stu-id="00ce8-128">New-AzureRmAutomationConnection</span></span>](/powershell/module/azurerm.automation/new-azurermautomationconnection)|<span data-ttu-id="00ce8-129">Creates a new connection.</span><span class="sxs-lookup"><span data-stu-id="00ce8-129">Creates a new connection.</span></span>|
|[<span data-ttu-id="00ce8-130">Remove-AzureRmAutomationConnection</span><span class="sxs-lookup"><span data-stu-id="00ce8-130">Remove-AzureRmAutomationConnection</span></span>](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|<span data-ttu-id="00ce8-131">Remove an existing connection.</span><span class="sxs-lookup"><span data-stu-id="00ce8-131">Remove an existing connection.</span></span>|
|[<span data-ttu-id="00ce8-132">Set-AzureRmAutomationConnectionFieldValue</span><span class="sxs-lookup"><span data-stu-id="00ce8-132">Set-AzureRmAutomationConnectionFieldValue</span></span>](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|<span data-ttu-id="00ce8-133">Sets the value of a particular field for an existing connection.</span><span class="sxs-lookup"><span data-stu-id="00ce8-133">Sets the value of a particular field for an existing connection.</span></span>|

## <a name="activities"></a><span data-ttu-id="00ce8-134">Activities</span><span class="sxs-lookup"><span data-stu-id="00ce8-134">Activities</span></span>

<span data-ttu-id="00ce8-135">The activities in the following table are used to access connections in a runbook or DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="00ce8-135">The activities in the following table are used to access connections in a runbook or DSC configuration.</span></span>

|<span data-ttu-id="00ce8-136">Activities</span><span class="sxs-lookup"><span data-stu-id="00ce8-136">Activities</span></span>|<span data-ttu-id="00ce8-137">Description</span><span class="sxs-lookup"><span data-stu-id="00ce8-137">Description</span></span>|
|---|---|
|[<span data-ttu-id="00ce8-138">Get-AutomationConnection</span><span class="sxs-lookup"><span data-stu-id="00ce8-138">Get-AutomationConnection</span></span>](/powershell/module/servicemanagement/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|<span data-ttu-id="00ce8-139">Gets a connection to use.</span><span class="sxs-lookup"><span data-stu-id="00ce8-139">Gets a connection to use.</span></span> <span data-ttu-id="00ce8-140">Returns a hash table with the properties of the connection.</span><span class="sxs-lookup"><span data-stu-id="00ce8-140">Returns a hash table with the properties of the connection.</span></span>|

>[!NOTE] 
><span data-ttu-id="00ce8-141">You should avoid using variables with the –Name parameter of **Get- AutomationConnection** since this can complicate discovering dependencies between runbooks or DSC configurations, and connection assets at design time.</span><span class="sxs-lookup"><span data-stu-id="00ce8-141">You should avoid using variables with the –Name parameter of **Get- AutomationConnection** since this can complicate discovering dependencies between runbooks or DSC configurations, and connection assets at design time.</span></span>

 
## <a name="python2-functions"></a><span data-ttu-id="00ce8-142">Python2 functions</span><span class="sxs-lookup"><span data-stu-id="00ce8-142">Python2 functions</span></span> 
<span data-ttu-id="00ce8-143">The function in the following table is used to access connections in a Python2 runbook.</span><span class="sxs-lookup"><span data-stu-id="00ce8-143">The function in the following table is used to access connections in a Python2 runbook.</span></span> 

| <span data-ttu-id="00ce8-144">Function</span><span class="sxs-lookup"><span data-stu-id="00ce8-144">Function</span></span> | <span data-ttu-id="00ce8-145">Description</span><span class="sxs-lookup"><span data-stu-id="00ce8-145">Description</span></span> | 
|:---|:---| 
| <span data-ttu-id="00ce8-146">automationassets.get_automation_connection</span><span class="sxs-lookup"><span data-stu-id="00ce8-146">automationassets.get_automation_connection</span></span> | <span data-ttu-id="00ce8-147">Retrieves a connection.</span><span class="sxs-lookup"><span data-stu-id="00ce8-147">Retrieves a connection.</span></span> <span data-ttu-id="00ce8-148">Returns a dictionary with the properties of the connection.</span><span class="sxs-lookup"><span data-stu-id="00ce8-148">Returns a dictionary with the properties of the connection.</span></span> | 

> [!NOTE] 
> <span data-ttu-id="00ce8-149">You must import the "automationassets" module at the top of your Python runbook in order to access the asset functions.</span><span class="sxs-lookup"><span data-stu-id="00ce8-149">You must import the "automationassets" module at the top of your Python runbook in order to access the asset functions.</span></span>

## <a name="creating-a-new-connection"></a><span data-ttu-id="00ce8-150">Creating a New Connection</span><span class="sxs-lookup"><span data-stu-id="00ce8-150">Creating a New Connection</span></span>

### <a name="to-create-a-new-connection-with-the-azure-portal"></a><span data-ttu-id="00ce8-151">To create a new connection with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="00ce8-151">To create a new connection with the Azure portal</span></span>

1. <span data-ttu-id="00ce8-152">From your automation account, click the **Assets** part to open the **Assets** blade.</span><span class="sxs-lookup"><span data-stu-id="00ce8-152">From your automation account, click the **Assets** part to open the **Assets** blade.</span></span>
2. <span data-ttu-id="00ce8-153">Click the **Connections** part to open the **Connections** blade.</span><span class="sxs-lookup"><span data-stu-id="00ce8-153">Click the **Connections** part to open the **Connections** blade.</span></span>
3. <span data-ttu-id="00ce8-154">Click **Add a connection** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="00ce8-154">Click **Add a connection** at the top of the blade.</span></span>
4. <span data-ttu-id="00ce8-155">In the **Type** dropdown, select the type of connection you want to create.</span><span class="sxs-lookup"><span data-stu-id="00ce8-155">In the **Type** dropdown, select the type of connection you want to create.</span></span> <span data-ttu-id="00ce8-156">The form will present the properties for that particular type.</span><span class="sxs-lookup"><span data-stu-id="00ce8-156">The form will present the properties for that particular type.</span></span>
5. <span data-ttu-id="00ce8-157">Complete the form and click **Create** to save the new connection.</span><span class="sxs-lookup"><span data-stu-id="00ce8-157">Complete the form and click **Create** to save the new connection.</span></span>

### <a name="to-create-a-new-connection-with-windows-powershell"></a><span data-ttu-id="00ce8-158">To create a new connection with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="00ce8-158">To create a new connection with Windows PowerShell</span></span>

<span data-ttu-id="00ce8-159">Create a new connection with Windows PowerShell using the [New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="00ce8-159">Create a new connection with Windows PowerShell using the [New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet.</span></span> <span data-ttu-id="00ce8-160">This cmdlet has a parameter named **ConnectionFieldValues** that expects a [hash table](http://technet.microsoft.com/library/hh847780.aspx) defining values for each of the properties defined by the connection type.</span><span class="sxs-lookup"><span data-stu-id="00ce8-160">This cmdlet has a parameter named **ConnectionFieldValues** that expects a [hash table](http://technet.microsoft.com/library/hh847780.aspx) defining values for each of the properties defined by the connection type.</span></span>

<span data-ttu-id="00ce8-161">If you are familiar with the Automation [Run As account](automation-sec-configure-azure-runas-account.md) to authenticate runbooks using the service principal, the PowerShell script, provided as an alternative to creating the Run As account from the portal, creates a new connection asset using the following sample commands.</span><span class="sxs-lookup"><span data-stu-id="00ce8-161">If you are familiar with the Automation [Run As account](automation-sec-configure-azure-runas-account.md) to authenticate runbooks using the service principal, the PowerShell script, provided as an alternative to creating the Run As account from the portal, creates a new connection asset using the following sample commands.</span></span>  

```powershell
$ConnectionAssetName = "AzureRunAsConnection"
$ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues
```

<span data-ttu-id="00ce8-162">You are able to use the script to create the connection asset because when you create your Automation account, it automatically includes several global modules by default along with the connection type **AzureServicePrincipal** to create the **AzureRunAsConnection** connection asset.</span><span class="sxs-lookup"><span data-stu-id="00ce8-162">You are able to use the script to create the connection asset because when you create your Automation account, it automatically includes several global modules by default along with the connection type **AzureServicePrincipal** to create the **AzureRunAsConnection** connection asset.</span></span>  <span data-ttu-id="00ce8-163">This is important to keep in mind, because if you attempt to create a new connection asset to connect to a service or application with a different authentication method, it will fail because the connection type is not already defined in your Automation account.</span><span class="sxs-lookup"><span data-stu-id="00ce8-163">This is important to keep in mind, because if you attempt to create a new connection asset to connect to a service or application with a different authentication method, it will fail because the connection type is not already defined in your Automation account.</span></span>  <span data-ttu-id="00ce8-164">For further information on how to create your own connection type for your custom or module from the [PowerShell Gallery](https://www.powershellgallery.com), see [Integration Modules](automation-integration-modules.md)</span><span class="sxs-lookup"><span data-stu-id="00ce8-164">For further information on how to create your own connection type for your custom or module from the [PowerShell Gallery](https://www.powershellgallery.com), see [Integration Modules](automation-integration-modules.md)</span></span>
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="00ce8-165">Using a connection in a runbook or DSC configuration</span><span class="sxs-lookup"><span data-stu-id="00ce8-165">Using a connection in a runbook or DSC configuration</span></span>

<span data-ttu-id="00ce8-166">You retrieve a connection in a runbook or DSC configuration with the **Get-AutomationConnection** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="00ce8-166">You retrieve a connection in a runbook or DSC configuration with the **Get-AutomationConnection** cmdlet.</span></span>  <span data-ttu-id="00ce8-167">You cannot use the [Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection) activity.</span><span class="sxs-lookup"><span data-stu-id="00ce8-167">You cannot use the [Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection) activity.</span></span>  <span data-ttu-id="00ce8-168">This activity retrieves the values of the different fields in the connection and returns them as a [hash table](http://go.microsoft.com/fwlink/?LinkID=324844) which can then be used with the appropriate commands in the runbook or DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="00ce8-168">This activity retrieves the values of the different fields in the connection and returns them as a [hash table](http://go.microsoft.com/fwlink/?LinkID=324844) which can then be used with the appropriate commands in the runbook or DSC configuration.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="00ce8-169">Textual runbook sample</span><span class="sxs-lookup"><span data-stu-id="00ce8-169">Textual runbook sample</span></span>

<span data-ttu-id="00ce8-170">The following sample commands show how to use the Run As account mentioned earlier, to authenticate with Azure Resource Manager resources in your runbook.</span><span class="sxs-lookup"><span data-stu-id="00ce8-170">The following sample commands show how to use the Run As account mentioned earlier, to authenticate with Azure Resource Manager resources in your runbook.</span></span>  <span data-ttu-id="00ce8-171">It uses the connection asset representing the Run As account, which references the certificate-based service principal, not credentials.</span><span class="sxs-lookup"><span data-stu-id="00ce8-171">It uses the connection asset representing the Run As account, which references the certificate-based service principal, not credentials.</span></span>  

```powershell
$Conn = Get-AutomationConnection -Name AzureRunAsConnection 
Connect-AzureRmAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
```

> [!IMPORTANT]
> <span data-ttu-id="00ce8-172">**Add-AzureRmAccount** is now an alias for **Connect-AzureRMAccount**.</span><span class="sxs-lookup"><span data-stu-id="00ce8-172">**Add-AzureRmAccount** is now an alias for **Connect-AzureRMAccount**.</span></span> <span data-ttu-id="00ce8-173">When searching your library items, if you do not see **Connect-AzureRMAccount**, you can use **Add-AzureRmAccount**, or you can update your modules in your Automation Account.</span><span class="sxs-lookup"><span data-stu-id="00ce8-173">When searching your library items, if you do not see **Connect-AzureRMAccount**, you can use **Add-AzureRmAccount**, or you can update your modules in your Automation Account.</span></span>

### <a name="graphical-runbook-samples"></a><span data-ttu-id="00ce8-174">Graphical runbook samples</span><span class="sxs-lookup"><span data-stu-id="00ce8-174">Graphical runbook samples</span></span>

<span data-ttu-id="00ce8-175">You add a **Get-AutomationConnection** activity to a graphical runbook by right-clicking on the connection in the Library pane of the graphical editor and selecting **Add to canvas**.</span><span class="sxs-lookup"><span data-stu-id="00ce8-175">You add a **Get-AutomationConnection** activity to a graphical runbook by right-clicking on the connection in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![](media/automation-connections/connection-add-canvas.png)

<span data-ttu-id="00ce8-176">The following image shows an example of using a connection in a graphical runbook.</span><span class="sxs-lookup"><span data-stu-id="00ce8-176">The following image shows an example of using a connection in a graphical runbook.</span></span>  <span data-ttu-id="00ce8-177">This is the same example shown above for authenticating using the Run As account with a textual runbook.</span><span class="sxs-lookup"><span data-stu-id="00ce8-177">This is the same example shown above for authenticating using the Run As account with a textual runbook.</span></span>  <span data-ttu-id="00ce8-178">This example uses the **Constant value** data set for the **Get RunAs Connection** activity that uses a connection object for authentication.</span><span class="sxs-lookup"><span data-stu-id="00ce8-178">This example uses the **Constant value** data set for the **Get RunAs Connection** activity that uses a connection object for authentication.</span></span>  <span data-ttu-id="00ce8-179">A [pipeline link](automation-graphical-authoring-intro.md#links-and-workflow) is used here since the ServicePrincipalCertificate parameter set is expecting a single object.</span><span class="sxs-lookup"><span data-stu-id="00ce8-179">A [pipeline link](automation-graphical-authoring-intro.md#links-and-workflow) is used here since the ServicePrincipalCertificate parameter set is expecting a single object.</span></span>

![](media/automation-connections/automation-get-connection-object.png)

### <a name="python2-runbook-sample"></a><span data-ttu-id="00ce8-180">Python2 runbook sample</span><span class="sxs-lookup"><span data-stu-id="00ce8-180">Python2 runbook sample</span></span>
<span data-ttu-id="00ce8-181">The following sample shows how to authenticate using the Run As connection in a Python2 runbook.</span><span class="sxs-lookup"><span data-stu-id="00ce8-181">The following sample shows how to authenticate using the Run As connection in a Python2 runbook.</span></span>

```python
""" Tutorial to show how to authenticate against Azure resource manager resources """
import azure.mgmt.resource
import automationassets

def get_automation_runas_credential(runas_connection):
  """ Returns credentials to authenticate against Azure resoruce manager """
  from OpenSSL import crypto
  from msrestazure import azure_active_directory
  import adal

  # Get the Azure Automation Run As service principal certificate
  cert = automationassets.get_automation_certificate("AzureRunAsCertificate")
  pks12_cert = crypto.load_pkcs12(cert)
  pem_pkey = crypto.dump_privatekey(crypto.FILETYPE_PEM, pks12_cert.get_privatekey())

  # Get Run As connection information for the Azure Automation service principal
  application_id = runas_connection["ApplicationId"]
  thumbprint = runas_connection["CertificateThumbprint"]
  tenant_id = runas_connection["TenantId"]

  # Authenticate with service principal certificate
  resource = "https://management.core.windows.net/"
  authority_url = ("https://login.microsoftonline.com/" + tenant_id)
  context = adal.AuthenticationContext(authority_url)
  return azure_active_directory.AdalAuthentication(
    lambda: context.acquire_token_with_client_certificate(
      resource,
      application_id,
      pem_pkey,
      thumbprint)
  )

# Authenticate to Azure using the Azure Automation Run As service principal
runas_connection = automationassets.get_automation_connection("AzureRunAsConnection")
azure_credential = get_automation_runas_credential(runas_connection)
```

## <a name="next-steps"></a><span data-ttu-id="00ce8-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="00ce8-182">Next steps</span></span>

- <span data-ttu-id="00ce8-183">Review [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow) to understand how to direct and control the flow of logic in your runbooks.</span><span class="sxs-lookup"><span data-stu-id="00ce8-183">Review [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow) to understand how to direct and control the flow of logic in your runbooks.</span></span>  

- <span data-ttu-id="00ce8-184">To learn more about Azure Automation's use of PowerShell modules and best practices for creating your own PowerShell modules to work as Integration Modules within Azure Automation, see [Integration Modules](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="00ce8-184">To learn more about Azure Automation's use of PowerShell modules and best practices for creating your own PowerShell modules to work as Integration Modules within Azure Automation, see [Integration Modules](automation-integration-modules.md).</span></span>  
