---
title: Deploy a web app using MSDeploy with hostname and ssl certificate
description: Use an Azure Resource Manager template to deploy a web app using MSDeploy and setting up custom hostname and a SSL certificate
services: app-service\web
manager: erikre
documentationcenter: ''
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: f836bffd0610224b5cb69f4f6836dbc55e0721a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551477"
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="6c160-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span><span class="sxs-lookup"><span data-stu-id="6c160-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="6c160-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate to the ARM template.</span><span class="sxs-lookup"><span data-stu-id="6c160-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate to the ARM template.</span></span>

<span data-ttu-id="6c160-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6c160-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="6c160-106">Create Sample Application</span><span class="sxs-lookup"><span data-stu-id="6c160-106">Create Sample Application</span></span>
<span data-ttu-id="6c160-107">You will be deploying an ASP.NET web application.</span><span class="sxs-lookup"><span data-stu-id="6c160-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="6c160-108">The first step is to create a simple web application (or you could choose to use an existing one - in which case you can skip this step).</span><span class="sxs-lookup"><span data-stu-id="6c160-108">The first step is to create a simple web application (or you could choose to use an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="6c160-109">Open Visual Studio 2015 and choose File > New Project.</span><span class="sxs-lookup"><span data-stu-id="6c160-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="6c160-110">On the dialog that appears choose Web > ASP.NET Web Application.</span><span class="sxs-lookup"><span data-stu-id="6c160-110">On the dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="6c160-111">Under Templates choose Web and choose the MVC template.</span><span class="sxs-lookup"><span data-stu-id="6c160-111">Under Templates choose Web and choose the MVC template.</span></span> <span data-ttu-id="6c160-112">Select *Change authentication type* to *No Authentication*.</span><span class="sxs-lookup"><span data-stu-id="6c160-112">Select *Change authentication type* to *No Authentication*.</span></span> <span data-ttu-id="6c160-113">This is just to make the sample application as simple as possible.</span><span class="sxs-lookup"><span data-stu-id="6c160-113">This is just to make the sample application as simple as possible.</span></span>

<span data-ttu-id="6c160-114">At this point you will have a basic ASP.Net web app ready to use as part of your deployment process.</span><span class="sxs-lookup"><span data-stu-id="6c160-114">At this point you will have a basic ASP.Net web app ready to use as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="6c160-115">Create MSDeploy package</span><span class="sxs-lookup"><span data-stu-id="6c160-115">Create MSDeploy package</span></span>
<span data-ttu-id="6c160-116">Next step is to create the package to deploy the web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="6c160-116">Next step is to create the package to deploy the web app to Azure.</span></span> <span data-ttu-id="6c160-117">To do this, save your project and then run the following from the command line:</span><span class="sxs-lookup"><span data-stu-id="6c160-117">To do this, save your project and then run the following from the command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="6c160-118">This will create a zipped package under the PackageLocation folder.</span><span class="sxs-lookup"><span data-stu-id="6c160-118">This will create a zipped package under the PackageLocation folder.</span></span> <span data-ttu-id="6c160-119">The application is now ready to be deployed, which you can now build out an Azure Resource Manager template to do that.</span><span class="sxs-lookup"><span data-stu-id="6c160-119">The application is now ready to be deployed, which you can now build out an Azure Resource Manager template to do that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="6c160-120">Create ARM Template</span><span class="sxs-lookup"><span data-stu-id="6c160-120">Create ARM Template</span></span>
<span data-ttu-id="6c160-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span><span class="sxs-lookup"><span data-stu-id="6c160-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

<span data-ttu-id="6c160-122">Next, you will need to modify the web app resource to take a nested MSDeploy resource.</span><span class="sxs-lookup"><span data-stu-id="6c160-122">Next, you will need to modify the web app resource to take a nested MSDeploy resource.</span></span> <span data-ttu-id="6c160-123">This will allow you to reference the package created earlier and tell Azure Resource Manager to use MSDeploy to deploy the package to the Azure WebApp.</span><span class="sxs-lookup"><span data-stu-id="6c160-123">This will allow you to reference the package created earlier and tell Azure Resource Manager to use MSDeploy to deploy the package to the Azure WebApp.</span></span> <span data-ttu-id="6c160-124">The following shows the Microsoft.Web/sites resource with the nested MSDeploy resource:</span><span class="sxs-lookup"><span data-stu-id="6c160-124">The following shows the Microsoft.Web/sites resource with the nested MSDeploy resource:</span></span>

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

<span data-ttu-id="6c160-125">Now you will notice that the MSDeploy resource takes a **packageUri** property which is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="6c160-125">Now you will notice that the MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="6c160-126">This **packageUri** takes the storage account uri which points to the storage account where you will upload your package zip to.</span><span class="sxs-lookup"><span data-stu-id="6c160-126">This **packageUri** takes the storage account uri which points to the storage account where you will upload your package zip to.</span></span> <span data-ttu-id="6c160-127">The Azure Resource Manager will leverage [Shared Access Signatures](../storage/storage-dotnet-shared-access-signature-part-1.md) to pull the package down locally from the storage account when you deploy the template.</span><span class="sxs-lookup"><span data-stu-id="6c160-127">The Azure Resource Manager will leverage [Shared Access Signatures](../storage/storage-dotnet-shared-access-signature-part-1.md) to pull the package down locally from the storage account when you deploy the template.</span></span> <span data-ttu-id="6c160-128">This process will be automated via a PowerShell script that will upload the package and call the Azure Management API to create the keys required and pass those into the template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="6c160-128">This process will be automated via a PowerShell script that will upload the package and call the Azure Management API to create the keys required and pass those into the template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="6c160-129">You will need to define parameters for the folder and filename the package is uploaded to under the storage container.</span><span class="sxs-lookup"><span data-stu-id="6c160-129">You will need to define parameters for the folder and filename the package is uploaded to under the storage container.</span></span>

<span data-ttu-id="6c160-130">Next you need to add in another nested resource to setup the hostname bindings to leverage a custom domain.</span><span class="sxs-lookup"><span data-stu-id="6c160-130">Next you need to add in another nested resource to setup the hostname bindings to leverage a custom domain.</span></span> <span data-ttu-id="6c160-131">You will first need to ensure that you own the hostname and set it up to be verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="6c160-131">You will first need to ensure that you own the hostname and set it up to be verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="6c160-132">Once that is done you can add the following to your template under the Microsoft.Web/sites resource section:</span><span class="sxs-lookup"><span data-stu-id="6c160-132">Once that is done you can add the following to your template under the Microsoft.Web/sites resource section:</span></span>

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

<span data-ttu-id="6c160-133">Finally you need to add another top level resource, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="6c160-133">Finally you need to add another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="6c160-134">This resource will contain your SSL certificate and will exist at the same level as your web app and hosting plan.</span><span class="sxs-lookup"><span data-stu-id="6c160-134">This resource will contain your SSL certificate and will exist at the same level as your web app and hosting plan.</span></span>

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

<span data-ttu-id="6c160-135">You will need to have a valid SSL certificate in order to set up this resource.</span><span class="sxs-lookup"><span data-stu-id="6c160-135">You will need to have a valid SSL certificate in order to set up this resource.</span></span> <span data-ttu-id="6c160-136">Once you have that valid certificate then you need to extract the pfx bytes as a base64 string.</span><span class="sxs-lookup"><span data-stu-id="6c160-136">Once you have that valid certificate then you need to extract the pfx bytes as a base64 string.</span></span> <span data-ttu-id="6c160-137">One option to extract this is to use the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="6c160-137">One option to extract this is to use the following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="6c160-138">You could then pass this as a parameter to your ARM deployment template.</span><span class="sxs-lookup"><span data-stu-id="6c160-138">You could then pass this as a parameter to your ARM deployment template.</span></span>

<span data-ttu-id="6c160-139">At this point the ARM template is ready.</span><span class="sxs-lookup"><span data-stu-id="6c160-139">At this point the ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="6c160-140">Deploy Template</span><span class="sxs-lookup"><span data-stu-id="6c160-140">Deploy Template</span></span>
<span data-ttu-id="6c160-141">The final steps are to piece this all together into a full end-to-end deployment.</span><span class="sxs-lookup"><span data-stu-id="6c160-141">The final steps are to piece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="6c160-142">To make deployment easier you can leverage the **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio to help with uploading of any artifacts required in the template.</span><span class="sxs-lookup"><span data-stu-id="6c160-142">To make deployment easier you can leverage the **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio to help with uploading of any artifacts required in the template.</span></span> <span data-ttu-id="6c160-143">It requires you to have created a storage account you want to use ahead of time.</span><span class="sxs-lookup"><span data-stu-id="6c160-143">It requires you to have created a storage account you want to use ahead of time.</span></span> <span data-ttu-id="6c160-144">For this example, I created a shared storage account for the package.zip to be uploaded.</span><span class="sxs-lookup"><span data-stu-id="6c160-144">For this example, I created a shared storage account for the package.zip to be uploaded.</span></span> <span data-ttu-id="6c160-145">The script will leverage AzCopy to upload the package to the storage account.</span><span class="sxs-lookup"><span data-stu-id="6c160-145">The script will leverage AzCopy to upload the package to the storage account.</span></span> <span data-ttu-id="6c160-146">You pass in your artifact folder location and the script will automatically upload all files within that directory to the named storage container.</span><span class="sxs-lookup"><span data-stu-id="6c160-146">You pass in your artifact folder location and the script will automatically upload all files within that directory to the named storage container.</span></span> <span data-ttu-id="6c160-147">After calling Deploy-AzureResourceGroup.ps1 you have to then update the SSL bindings to map the custom hostname with your SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="6c160-147">After calling Deploy-AzureResourceGroup.ps1 you have to then update the SSL bindings to map the custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="6c160-148">The following PowerShell shows the complete deployment calling the Deploy-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="6c160-148">The following PowerShell shows the complete deployment calling the Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="6c160-149">At this point your application should have been deployed and you should be able to browse to it via https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="6c160-149">At this point your application should have been deployed and you should be able to browse to it via https://www.yourcustomdomain.com</span></span>

