### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="61c83-101">Troubleshoot Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="61c83-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="61c83-102">If you receive the following error message, the Microsoft.insights resource provider is not registered:</span><span class="sxs-lookup"><span data-stu-id="61c83-102">If you receive the following error message, the Microsoft.insights resource provider is not registered:</span></span>

`Failed to update diagnostics for 'resource'. {"code":"Forbidden","message":"Please register the subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="61c83-103">To register the resource provider, perform the following steps in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="61c83-103">To register the resource provider, perform the following steps in the Azure portal:</span></span>

1.  <span data-ttu-id="61c83-104">In the navigation pane on the left, click *Subscriptions*</span><span class="sxs-lookup"><span data-stu-id="61c83-104">In the navigation pane on the left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="61c83-105">Select the subscription identified in the error message</span><span class="sxs-lookup"><span data-stu-id="61c83-105">Select the subscription identified in the error message</span></span>
3.  <span data-ttu-id="61c83-106">Click *Resource Providers*</span><span class="sxs-lookup"><span data-stu-id="61c83-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="61c83-107">Find the *Microsoft.insights* provider</span><span class="sxs-lookup"><span data-stu-id="61c83-107">Find the *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="61c83-108">Click the *Register* link</span><span class="sxs-lookup"><span data-stu-id="61c83-108">Click the *Register* link</span></span>

![Register microsoft.insights resource provider](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="61c83-110">Once the *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span><span class="sxs-lookup"><span data-stu-id="61c83-110">Once the *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="61c83-111">In PowerShell, if you receive the following error message, you need to update your version of PowerShell:</span><span class="sxs-lookup"><span data-stu-id="61c83-111">In PowerShell, if you receive the following error message, you need to update your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="61c83-112">Update your version of PowerShell to the November 2016 (v2.3.0), or later, release using the instructions in the [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span><span class="sxs-lookup"><span data-stu-id="61c83-112">Update your version of PowerShell to the November 2016 (v2.3.0), or later, release using the instructions in the [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>

