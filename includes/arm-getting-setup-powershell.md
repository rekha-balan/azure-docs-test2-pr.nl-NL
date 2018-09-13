## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="247db-101">Setting up PowerShell for Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="247db-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="247db-102">Before you can use Azure PowerShell with Resource Manager, you will need to have the right Windows PowerShell and Azure PowerShell versions.</span><span class="sxs-lookup"><span data-stu-id="247db-102">Before you can use Azure PowerShell with Resource Manager, you will need to have the right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="247db-103">Verify PowerShell versions</span><span class="sxs-lookup"><span data-stu-id="247db-103">Verify PowerShell versions</span></span>
<span data-ttu-id="247db-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span><span class="sxs-lookup"><span data-stu-id="247db-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="247db-105">To find the version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="247db-105">To find the version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="247db-106">You will receive the following type of information:</span><span class="sxs-lookup"><span data-stu-id="247db-106">You will receive the following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="247db-107">Verify that the value of **PSVersion** is 3.0 or 4.0.</span><span class="sxs-lookup"><span data-stu-id="247db-107">Verify that the value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="247db-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="247db-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="247db-109">Set your Azure account and subscription</span><span class="sxs-lookup"><span data-stu-id="247db-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="247db-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="247db-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="247db-111">Open an Azure PowerShell command prompt and log on to Azure with this command.</span><span class="sxs-lookup"><span data-stu-id="247db-111">Open an Azure PowerShell command prompt and log on to Azure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="247db-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span><span class="sxs-lookup"><span data-stu-id="247db-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="247db-113">You will receive the following type of information:</span><span class="sxs-lookup"><span data-stu-id="247db-113">You will receive the following type of information:</span></span>

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

<span data-ttu-id="247db-114">You can set the current Azure subscription by running these commands at the Azure PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="247db-114">You can set the current Azure subscription by running these commands at the Azure PowerShell command prompt.</span></span> <span data-ttu-id="247db-115">Replace everything within the quotes, including the < and > characters, with the correct name.</span><span class="sxs-lookup"><span data-stu-id="247db-115">Replace everything within the quotes, including the < and > characters, with the correct name.</span></span>

    $subscr="<SubscriptionName from the display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="247db-116">For more information about Azure subscriptions and accounts, see [How to: Connect to your subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="247db-116">For more information about Azure subscriptions and accounts, see [How to: Connect to your subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

