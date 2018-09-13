## <a name="how-to-deploy-with-azure-cli"></a><span data-ttu-id="167d7-101">How to deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="167d7-101">How to deploy with Azure CLI</span></span>
1. <span data-ttu-id="167d7-102">Login to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="167d7-102">Login to your Azure account.</span></span>
   
        azure login
   
   <span data-ttu-id="167d7-103">After providing your credentials, the command returns the result of your login.</span><span class="sxs-lookup"><span data-stu-id="167d7-103">After providing your credentials, the command returns the result of your login.</span></span>
   
        ...
        info:    login command OK
2. <span data-ttu-id="167d7-104">If you have multiple subscriptions, provide the subscription id you wish to use for deployment.</span><span class="sxs-lookup"><span data-stu-id="167d7-104">If you have multiple subscriptions, provide the subscription id you wish to use for deployment.</span></span>
   
        azure account set <YourSubscriptionNameOrId>
3. <span data-ttu-id="167d7-105">Switch to Azure Resource Manager module</span><span class="sxs-lookup"><span data-stu-id="167d7-105">Switch to Azure Resource Manager module</span></span>
   
        azure config mode arm
   
   <span data-ttu-id="167d7-106">You will receive confirmation of the new mode.</span><span class="sxs-lookup"><span data-stu-id="167d7-106">You will receive confirmation of the new mode.</span></span>
   
        info:     New mode is arm
4. <span data-ttu-id="167d7-107">If you do not have an existing resource group, create a new resource group.</span><span class="sxs-lookup"><span data-stu-id="167d7-107">If you do not have an existing resource group, create a new resource group.</span></span> <span data-ttu-id="167d7-108">Provide the name of the resource group and location that you need for your solution.</span><span class="sxs-lookup"><span data-stu-id="167d7-108">Provide the name of the resource group and location that you need for your solution.</span></span>
   
        azure group create -n ExampleResourceGroup -l "West US"
   
   <span data-ttu-id="167d7-109">A summary of the new resource group is returned.</span><span class="sxs-lookup"><span data-stu-id="167d7-109">A summary of the new resource group is returned.</span></span>
   
        info:    Executing command group create
        + Getting resource group ExampleResourceGroup
        + Creating resource group ExampleResourceGroup
        info:    Created resource group ExampleResourceGroup
        data:    Id:                  /subscriptions/####/resourceGroups/ExampleResourceGroup
        data:    Name:                ExampleResourceGroup
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags:
        data:
        info:    group create command OK
5. <span data-ttu-id="167d7-110">To create a new deployment for your resource group, run the following command and provide the necessary parameters.</span><span class="sxs-lookup"><span data-stu-id="167d7-110">To create a new deployment for your resource group, run the following command and provide the necessary parameters.</span></span> <span data-ttu-id="167d7-111">The parameters will include a name for your deployment, the name of your resource group, the path or URL to the template you created, and any other parameters needed for your scenario.</span><span class="sxs-lookup"><span data-stu-id="167d7-111">The parameters will include a name for your deployment, the name of your resource group, the path or URL to the template you created, and any other parameters needed for your scenario.</span></span>
   
   <span data-ttu-id="167d7-112">You have the following options for providing parameter values:</span><span class="sxs-lookup"><span data-stu-id="167d7-112">You have the following options for providing parameter values:</span></span>
   
   * <span data-ttu-id="167d7-113">Use inline parameters and a local template.</span><span class="sxs-lookup"><span data-stu-id="167d7-113">Use inline parameters and a local template.</span></span>
     
             azure group deployment create -f <PathToTemplate> {"ParameterName":"ParameterValue"} -g ExampleResourceGroup -n ExampleDeployment
   * <span data-ttu-id="167d7-114">Use inline parameters and a link to a template.</span><span class="sxs-lookup"><span data-stu-id="167d7-114">Use inline parameters and a link to a template.</span></span>
     
             azure group deployment create --template-uri <LinkToTemplate> {"ParameterName":"ParameterValue"} -g ExampleResourceGroup -n ExampleDeployment
   * <span data-ttu-id="167d7-115">Use a parameter file.</span><span class="sxs-lookup"><span data-stu-id="167d7-115">Use a parameter file.</span></span>
     
             azure group deployment create -f <PathToTemplate> -e <PathToParameterFile> -g ExampleResourceGroup -n ExampleDeployment
   
   <span data-ttu-id="167d7-116">When the resource group has been deployed, you will see a summary of the deployment.</span><span class="sxs-lookup"><span data-stu-id="167d7-116">When the resource group has been deployed, you will see a summary of the deployment.</span></span>
   
         info:    Executing command group deployment create
         + Initializing template configurations and parameters
         + Creating a deployment
         ...
         info:    group deployment create command OK
6. <span data-ttu-id="167d7-117">To get information about your latest deployment.</span><span class="sxs-lookup"><span data-stu-id="167d7-117">To get information about your latest deployment.</span></span>
   
         azure group log show -l ExampleResourceGroup
7. <span data-ttu-id="167d7-118">To get detailed information about deployment failures.</span><span class="sxs-lookup"><span data-stu-id="167d7-118">To get detailed information about deployment failures.</span></span>
   
         azure group log show -l -v ExampleResourceGroup

