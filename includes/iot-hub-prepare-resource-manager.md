## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a><span data-ttu-id="8af17-101">Prepare to authenticate Azure Resource Manager requests</span><span class="sxs-lookup"><span data-stu-id="8af17-101">Prepare to authenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="8af17-102">You must authenticate all the operations that you perform on resources using the [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="8af17-102">You must authenticate all the operations that you perform on resources using the [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="8af17-103">The easiest way to configure this is to use PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8af17-103">The easiest way to configure this is to use PowerShell or Azure CLI.</span></span>

<span data-ttu-id="8af17-104">You should install [Azure PowerShell 1.0][lnk-powershell-install] or later before you continue.</span><span class="sxs-lookup"><span data-stu-id="8af17-104">You should install [Azure PowerShell 1.0][lnk-powershell-install] or later before you continue.</span></span>

<span data-ttu-id="8af17-105">The following steps show how to set up password authentication for an AD application using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8af17-105">The following steps show how to set up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="8af17-106">You can run these commands in a standard PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="8af17-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="8af17-107">Log in to your Azure subscription using the following command:</span><span class="sxs-lookup"><span data-stu-id="8af17-107">Log in to your Azure subscription using the following command:</span></span>
   
    ```
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="8af17-108">Make a note of your **TenantId** and **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="8af17-108">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="8af17-109">You will need them later.</span><span class="sxs-lookup"><span data-stu-id="8af17-109">You will need them later.</span></span>
3. <span data-ttu-id="8af17-110">Create a new Azure Active Directory application using the following command, replacing the place holders:</span><span class="sxs-lookup"><span data-stu-id="8af17-110">Create a new Azure Active Directory application using the following command, replacing the place holders:</span></span>
   
   * <span data-ttu-id="8af17-111">**{Display name}:** a display name for your application such as **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="8af17-111">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="8af17-112">**{Home page URL}:** the URL of the home page of your app such as **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="8af17-112">**{Home page URL}:** the URL of the home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="8af17-113">This URL does not need to point to a real application.</span><span class="sxs-lookup"><span data-stu-id="8af17-113">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="8af17-114">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="8af17-114">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="8af17-115">This URL does not need to point to a real application.</span><span class="sxs-lookup"><span data-stu-id="8af17-115">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="8af17-116">**{Password}:** A password that you will use to authenticate with your app.</span><span class="sxs-lookup"><span data-stu-id="8af17-116">**{Password}:** A password that you will use to authenticate with your app.</span></span>
     
     ```
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="8af17-117">Make a note of the **ApplicationId** of the application you created.</span><span class="sxs-lookup"><span data-stu-id="8af17-117">Make a note of the **ApplicationId** of the application you created.</span></span> <span data-ttu-id="8af17-118">You will need this later.</span><span class="sxs-lookup"><span data-stu-id="8af17-118">You will need this later.</span></span>
5. <span data-ttu-id="8af17-119">Create a new service principal using the following command, replacing **{MyApplicationId}** with the **ApplicationId** from the previous step:</span><span class="sxs-lookup"><span data-stu-id="8af17-119">Create a new service principal using the following command, replacing **{MyApplicationId}** with the **ApplicationId** from the previous step:</span></span>
   
    ```
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="8af17-120">Setup a role assignment using the following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="8af17-120">Setup a role assignment using the following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="8af17-121">You have now finished creating the Azure AD application that will enable you to authenticate from your custom C# application.</span><span class="sxs-lookup"><span data-stu-id="8af17-121">You have now finished creating the Azure AD application that will enable you to authenticate from your custom C# application.</span></span> <span data-ttu-id="8af17-122">You will need the following values later in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="8af17-122">You will need the following values later in this tutorial:</span></span>

* <span data-ttu-id="8af17-123">TenantId</span><span class="sxs-lookup"><span data-stu-id="8af17-123">TenantId</span></span>
* <span data-ttu-id="8af17-124">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="8af17-124">SubscriptionId</span></span>
* <span data-ttu-id="8af17-125">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="8af17-125">ApplicationId</span></span>
* <span data-ttu-id="8af17-126">Password</span><span class="sxs-lookup"><span data-stu-id="8af17-126">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: /powershell/azureps-cmdlets-docs
