## <a name="how-to-deploy-with-powershell"></a><span data-ttu-id="ddfc8-101">How to deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddfc8-101">How to deploy with PowerShell</span></span>
1. <span data-ttu-id="ddfc8-102">Login to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-102">Login to your Azure account.</span></span>
   
          Add-AzureAccount
   
   <span data-ttu-id="ddfc8-103">After providing your credentials, the command returns information about your account.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-103">After providing your credentials, the command returns information about your account.</span></span>
   
          Id                             Type       ...
          --                             ----    
          example@contoso.com            User       ...   
2. <span data-ttu-id="ddfc8-104">If you have multiple subscriptions, provide the subscription id you wish to use for deployment.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-104">If you have multiple subscriptions, provide the subscription id you wish to use for deployment.</span></span> 
   
          Select-AzureSubscription -SubscriptionID <YourSubscriptionId>
3. <span data-ttu-id="ddfc8-105">Switch to the Azure Resource Manager module.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-105">Switch to the Azure Resource Manager module.</span></span>
   
          Switch-AzureMode AzureResourceManager
4. <span data-ttu-id="ddfc8-106">If you do not have an existing resource group, create a new resource group.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-106">If you do not have an existing resource group, create a new resource group.</span></span> <span data-ttu-id="ddfc8-107">Provide the name of the resource group and location that you need for your solution.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-107">Provide the name of the resource group and location that you need for your solution.</span></span>
   
        New-AzureResourceGroup -Name ExampleResourceGroup -Location "West US"
   
   <span data-ttu-id="ddfc8-108">A summary of the new resource group is returned.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-108">A summary of the new resource group is returned.</span></span>
   
        ResourceGroupName : ExampleResourceGroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                    Actions  NotActions
                    =======  ==========
                    *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup
5. <span data-ttu-id="ddfc8-109">To create a new deployment for your resource group, run the **New-AzureResourceGroupDeployment** command and provide the necessary parameters.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-109">To create a new deployment for your resource group, run the **New-AzureResourceGroupDeployment** command and provide the necessary parameters.</span></span> <span data-ttu-id="ddfc8-110">The parameters will include a name for your deployment, the name of your resource group, the path or URL to the template you created, and any other parameters needed for your scenario.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-110">The parameters will include a name for your deployment, the name of your resource group, the path or URL to the template you created, and any other parameters needed for your scenario.</span></span> 
   
   <span data-ttu-id="ddfc8-111">You have the following options for providing parameter values:</span><span class="sxs-lookup"><span data-stu-id="ddfc8-111">You have the following options for providing parameter values:</span></span> 
   
   * <span data-ttu-id="ddfc8-112">Use inline parameters.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-112">Use inline parameters.</span></span>
     
            New-AzureResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup -TemplateFile <PathOrLinkToTemplate> -myParameterName "parameterValue"
   * <span data-ttu-id="ddfc8-113">Use a parameter object.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-113">Use a parameter object.</span></span>
     
            $parameters = @{"<ParameterName>"="<Parameter Value>"}
            New-AzureResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup -TemplateFile <PathOrLinkToTemplate> -TemplateParameterObject $parameters
   * <span data-ttu-id="ddfc8-114">Using a parameter file.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-114">Using a parameter file.</span></span>
     
            New-AzureResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup -TemplateFile <PathOrLinkToTemplate> -TemplateParameterFile <PathOrLinkToParameterFile>
   
   <span data-ttu-id="ddfc8-115">When the resource group has been deployed, you will see a summary of the deployment.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-115">When the resource group has been deployed, you will see a summary of the deployment.</span></span>
   
             DeploymentName    : ExampleDeployment
             ResourceGroupName : ExampleResourceGroup
             ProvisioningState : Succeeded
             Timestamp         : 4/14/2015 7:00:27 PM
             Mode              : Incremental
             ...
6. <span data-ttu-id="ddfc8-116">To get information about deployment failures.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-116">To get information about deployment failures.</span></span>
   
        Get-AzureResourceGroupLog -ResourceGroup ExampleResourceGroup -Status Failed
7. <span data-ttu-id="ddfc8-117">To get detailed information about deployment failures.</span><span class="sxs-lookup"><span data-stu-id="ddfc8-117">To get detailed information about deployment failures.</span></span>
   
        Get-AzureResourceGroupLog -ResourceGroup ExampleResourceGroup -Status Failed -DetailedOutput

