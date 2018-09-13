

<span data-ttu-id="87e4f-101">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span><span class="sxs-lookup"><span data-stu-id="87e4f-101">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="87e4f-102">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) are an Azure Compute resource to deploy and manage a collection of similar virtual machines with easily integrated options for auto-scale and load balancing.</span><span class="sxs-lookup"><span data-stu-id="87e4f-102">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) are an Azure Compute resource to deploy and manage a collection of similar virtual machines with easily integrated options for auto-scale and load balancing.</span></span> <span data-ttu-id="87e4f-103">You can provision and deploy VM Scale Sets using [Azure Resource Manager (ARM) Templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="87e4f-103">You can provision and deploy VM Scale Sets using [Azure Resource Manager (ARM) Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="87e4f-104">ARM Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87e4f-104">ARM Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="87e4f-105">Visual Studio provides a set of example Templates which can be deployed as part of an Azure Resource Group Deployment project.</span><span class="sxs-lookup"><span data-stu-id="87e4f-105">Visual Studio provides a set of example Templates which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="87e4f-106">Azure Resource Group deployments are a way to group together and publish a set of related Azure resources in a single deployment operation.</span><span class="sxs-lookup"><span data-stu-id="87e4f-106">Azure Resource Group deployments are a way to group together and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="87e4f-107">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../articles/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="87e4f-107">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../articles/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="87e4f-108">Pre-requisites</span><span class="sxs-lookup"><span data-stu-id="87e4f-108">Pre-requisites</span></span>
<span data-ttu-id="87e4f-109">To get started deploying VM Scale Sets in Visual Studio you need the following:</span><span class="sxs-lookup"><span data-stu-id="87e4f-109">To get started deploying VM Scale Sets in Visual Studio you need the following:</span></span>

* <span data-ttu-id="87e4f-110">Visual Studio 2013 or 2015</span><span class="sxs-lookup"><span data-stu-id="87e4f-110">Visual Studio 2013 or 2015</span></span>
* <span data-ttu-id="87e4f-111">Azure SDK 2.7 or 2.8</span><span class="sxs-lookup"><span data-stu-id="87e4f-111">Azure SDK 2.7 or 2.8</span></span>

<span data-ttu-id="87e4f-112">Note: These instructions assume you are using Visual Studio 2015 with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="87e4f-112">Note: These instructions assume you are using Visual Studio 2015 with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="87e4f-113">Creating a Project</span><span class="sxs-lookup"><span data-stu-id="87e4f-113">Creating a Project</span></span>
1. <span data-ttu-id="87e4f-114">Create a new project in Visual Studio 2015 by choosing **File | New | Project**.</span><span class="sxs-lookup"><span data-stu-id="87e4f-114">Create a new project in Visual Studio 2015 by choosing **File | New | Project**.</span></span>
   
    ![File New][file_new]
2. <span data-ttu-id="87e4f-116">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an ARM Template.</span><span class="sxs-lookup"><span data-stu-id="87e4f-116">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an ARM Template.</span></span>
   
    ![Create Project][create_project]
3. <span data-ttu-id="87e4f-118">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span><span class="sxs-lookup"><span data-stu-id="87e4f-118">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Select Template][select_Template]
4. <span data-ttu-id="87e4f-120">Once your project is created you’ll see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span><span class="sxs-lookup"><span data-stu-id="87e4f-120">Once your project is created you’ll see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span></span>
   
    ![Solution Explorer][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="87e4f-122">Customize your project</span><span class="sxs-lookup"><span data-stu-id="87e4f-122">Customize your project</span></span>
<span data-ttu-id="87e4f-123">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="87e4f-123">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="87e4f-124">By default the VM Scale Set Templates are configured to deploy the AzureDiagnostics extension which makes it easy to add autoscale rules.</span><span class="sxs-lookup"><span data-stu-id="87e4f-124">By default the VM Scale Set Templates are configured to deploy the AzureDiagnostics extension which makes it easy to add autoscale rules.</span></span> <span data-ttu-id="87e4f-125">It also deploys a load balancer with a public IP address, configured with inbound NAT rules which let you connect to the VM instances with SSH (Linux) or RDP (Windows) – the front end port range starts at 50000, which means in the case of Linux, if you SSH to port 50000 of the public IP address (or domain name) you will be routed to port 22 of the first VM in the Scale Set.</span><span class="sxs-lookup"><span data-stu-id="87e4f-125">It also deploys a load balancer with a public IP address, configured with inbound NAT rules which let you connect to the VM instances with SSH (Linux) or RDP (Windows) – the front end port range starts at 50000, which means in the case of Linux, if you SSH to port 50000 of the public IP address (or domain name) you will be routed to port 22 of the first VM in the Scale Set.</span></span> <span data-ttu-id="87e4f-126">Connecting to port 50001 will be routed to port 22 of the second VM and so on.</span><span class="sxs-lookup"><span data-stu-id="87e4f-126">Connecting to port 50001 will be routed to port 22 of the second VM and so on.</span></span>

 <span data-ttu-id="87e4f-127">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables and resources.</span><span class="sxs-lookup"><span data-stu-id="87e4f-127">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables and resources.</span></span> <span data-ttu-id="87e4f-128">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span><span class="sxs-lookup"><span data-stu-id="87e4f-128">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![JSON Explorer][json_explorer]

## <a name="deploy-the-project"></a><span data-ttu-id="87e4f-130">Deploy the project</span><span class="sxs-lookup"><span data-stu-id="87e4f-130">Deploy the project</span></span>
1. <span data-ttu-id="87e4f-131">Deploy the ARM Template to Azure to create the VM Scale Set resource.</span><span class="sxs-lookup"><span data-stu-id="87e4f-131">Deploy the ARM Template to Azure to create the VM Scale Set resource.</span></span> <span data-ttu-id="87e4f-132">Right click on the project node, choose **Deploy | New Deployment**.</span><span class="sxs-lookup"><span data-stu-id="87e4f-132">Right click on the project node, choose **Deploy | New Deployment**.</span></span>
   
    ![Deploy Template][5deploy_Template]
2. <span data-ttu-id="87e4f-134">Select your subscription in the “Deploy to Resource Group” dialog.</span><span class="sxs-lookup"><span data-stu-id="87e4f-134">Select your subscription in the “Deploy to Resource Group” dialog.</span></span>
   
    ![Deploy Template][6deploy_Template]
3. <span data-ttu-id="87e4f-136">From here you can also create a new Azure Resource Group to deploy your Template to.</span><span class="sxs-lookup"><span data-stu-id="87e4f-136">From here you can also create a new Azure Resource Group to deploy your Template to.</span></span>
   
    ![New Resource Group][new_resource]
4. <span data-ttu-id="87e4f-138">Next select the **Edit Parameters** button to enter parameters which will be passed to your Template, Certain values such as the username and password for the OS are required to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="87e4f-138">Next select the **Edit Parameters** button to enter parameters which will be passed to your Template, Certain values such as the username and password for the OS are required to create the deployment.</span></span>
   
    ![Edit Parameters][edit_parameters]
5. <span data-ttu-id="87e4f-140">Now click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="87e4f-140">Now click **Deploy**.</span></span> <span data-ttu-id="87e4f-141">The **Output** window will show the deployment progress.</span><span class="sxs-lookup"><span data-stu-id="87e4f-141">The **Output** window will show the deployment progress.</span></span> <span data-ttu-id="87e4f-142">Note that the the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="87e4f-142">Note that the the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Output Window][output_window]

## <a name="exploring-your-vm-scale-set"></a><span data-ttu-id="87e4f-144">Exploring your VM Scale Set</span><span class="sxs-lookup"><span data-stu-id="87e4f-144">Exploring your VM Scale Set</span></span>
<span data-ttu-id="87e4f-145">Once the deployment completes, you can view the new VM Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span><span class="sxs-lookup"><span data-stu-id="87e4f-145">Once the deployment completes, you can view the new VM Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span></span> <span data-ttu-id="87e4f-146">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span><span class="sxs-lookup"><span data-stu-id="87e4f-146">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="87e4f-147">You can also view your VM Scale Set in the Azure Portal and Azure Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="87e4f-147">You can also view your VM Scale Set in the Azure Portal and Azure Resource Explorer.</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="87e4f-149">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explorer and debug Azure resources, giving a window into the “instance view” and also showing PowerShell commands for the resources you are looking at.</span><span class="sxs-lookup"><span data-stu-id="87e4f-149">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explorer and debug Azure resources, giving a window into the “instance view” and also showing PowerShell commands for the resources you are looking at.</span></span> <span data-ttu-id="87e4f-150">While VM Scale Sets are in preview, the Resource Explorer will show the most detail for your VM Scale Sets.</span><span class="sxs-lookup"><span data-stu-id="87e4f-150">While VM Scale Sets are in preview, the Resource Explorer will show the most detail for your VM Scale Sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87e4f-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="87e4f-151">Next steps</span></span>
<span data-ttu-id="87e4f-152">Once you’ve successfully deployed VM Scale Sets through Visual Studio you can further customize your project to suit your application requirements.</span><span class="sxs-lookup"><span data-stu-id="87e4f-152">Once you’ve successfully deployed VM Scale Sets through Visual Studio you can further customize your project to suit your application requirements.</span></span> <span data-ttu-id="87e4f-153">For example setting up autoscale by adding an Insights resource, adding infrastructure to your Template like standalone VMs, or deploying applications using the custom script extension.</span><span class="sxs-lookup"><span data-stu-id="87e4f-153">For example setting up autoscale by adding an Insights resource, adding infrastructure to your Template like standalone VMs, or deploying applications using the custom script extension.</span></span> <span data-ttu-id="87e4f-154">A good source of example Templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span><span class="sxs-lookup"><span data-stu-id="87e4f-154">A good source of example Templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/1-FileNew.png
[create_project]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/2-CreateProject.png
[select_Template]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/3b-SelectTemplateLin.png
[solution_explorer]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/4-SolutionExplorer.png
[json_explorer]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/10-JsonExplorer.png
[5deploy_Template]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/5-DeployTemplate.png
[6deploy_Template]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/6-DeployTemplate.png
[new_resource]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/7-NewResourceGroup.png
[edit_parameters]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/8-EditParameter.png
[output_window]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/9-Output.png
[cloud_explorer]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-scale-sets-visual-studio/12-CloudExplorer.png










