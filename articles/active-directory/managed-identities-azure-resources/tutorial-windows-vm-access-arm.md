---
title: Use a Windows VM system-assigned managed identity to access Azure Resource Manager
description: A tutorial that walks you through the process of using a Windows VM system-assigned managed identity to access Azure Resource Manager.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: daveba
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/20/2017
ms.author: daveba
ms.openlocfilehash: f1a29766dec9c32896428035c9e5d78e43c4ed18
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857525"
---
# <a name="use-a-windows-vm-system-assigned-managed-identity-to-access-resource-manager"></a><span data-ttu-id="a8f0b-103">Use a Windows VM system-assigned managed identity to access Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8f0b-103">Use a Windows VM system-assigned managed identity to access Resource Manager</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="a8f0b-104">This quickstart shows you how to access the Azure Resource Manager API using a Windows virtual machine with system-assigned managed identity enabled.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-104">This quickstart shows you how to access the Azure Resource Manager API using a Windows virtual machine with system-assigned managed identity enabled.</span></span> <span data-ttu-id="a8f0b-105">Managed identities for Azure resources are automatically managed by Azure and enable you to authenticate to services that support Azure AD authentication without needing to insert credentials into your code.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-105">Managed identities for Azure resources are automatically managed by Azure and enable you to authenticate to services that support Azure AD authentication without needing to insert credentials into your code.</span></span> <span data-ttu-id="a8f0b-106">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="a8f0b-106">You learn how to:</span></span>

> [!div class="checklist"] 
> * <span data-ttu-id="a8f0b-107">Grant your VM access to a Resource Group in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8f0b-107">Grant your VM access to a Resource Group in Azure Resource Manager</span></span> 
> * <span data-ttu-id="a8f0b-108">Get an access token using the VM identity and use it to call Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8f0b-108">Get an access token using the VM identity and use it to call Azure Resource Manager</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8f0b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a8f0b-109">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="a8f0b-110">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="a8f0b-110">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="a8f0b-111">Create a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="a8f0b-111">Create a Windows virtual machine</span></span>](/azure/virtual-machines/windows/quick-create-portal)

- [<span data-ttu-id="a8f0b-112">Enable system-assigned managed identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="a8f0b-112">Enable system-assigned managed identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

## <a name="grant-your-vm-access-to-a-resource-group-in-resource-manager"></a><span data-ttu-id="a8f0b-113">Grant your VM access to a resource group in Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8f0b-113">Grant your VM access to a resource group in Resource Manager</span></span>
<span data-ttu-id="a8f0b-114">Using managed identities for Azure resources, your code can get access tokens to authenticate to resources that support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-114">Using managed identities for Azure resources, your code can get access tokens to authenticate to resources that support Azure AD authentication.</span></span>  <span data-ttu-id="a8f0b-115">The Azure Resource Manager supports Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-115">The Azure Resource Manager supports Azure AD authentication.</span></span>  <span data-ttu-id="a8f0b-116">First, we need to grant this VM’s system-assigned managed identity access to a resource in Resource Manager, in this case the Resource Group in which the VM is contained.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-116">First, we need to grant this VM’s system-assigned managed identity access to a resource in Resource Manager, in this case the Resource Group in which the VM is contained.</span></span>  

1.  <span data-ttu-id="a8f0b-117">Navigate to the tab for **Resource Groups**.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-117">Navigate to the tab for **Resource Groups**.</span></span> 
2.  <span data-ttu-id="a8f0b-118">Select the specific **Resource Group** you created for your **Windows VM**.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-118">Select the specific **Resource Group** you created for your **Windows VM**.</span></span> 
3.  <span data-ttu-id="a8f0b-119">Go to **Access control (IAM)** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-119">Go to **Access control (IAM)** in the left panel.</span></span> 
4.  <span data-ttu-id="a8f0b-120">Then **Add** a new role assignment for your **Windows VM**.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-120">Then **Add** a new role assignment for your **Windows VM**.</span></span>  <span data-ttu-id="a8f0b-121">Choose **Role** as **Reader**.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-121">Choose **Role** as **Reader**.</span></span> 
5.  <span data-ttu-id="a8f0b-122">In the next drop-down, **Assign access to** the resource **Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-122">In the next drop-down, **Assign access to** the resource **Virtual Machine**.</span></span> 
6.  <span data-ttu-id="a8f0b-123">Next, ensure the proper subscription is listed in the **Subscription** dropdown.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-123">Next, ensure the proper subscription is listed in the **Subscription** dropdown.</span></span> <span data-ttu-id="a8f0b-124">And for **Resource Group**, select **All resource groups**.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-124">And for **Resource Group**, select **All resource groups**.</span></span> 
7.  <span data-ttu-id="a8f0b-125">Finally, in **Select** choose your Windows VM in the dropdown and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-125">Finally, in **Select** choose your Windows VM in the dropdown and click **Save**.</span></span>

    ![Alt image text](media/msi-tutorial-windows-vm-access-arm/msi-windows-permissions.png)

## <a name="get-an-access-token-using-the-vms-system-assigned-managed-identity-and-use-it-to-call-azure-resource-manager"></a><span data-ttu-id="a8f0b-127">Get an access token using the VM's system-assigned managed identity and use it to call Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8f0b-127">Get an access token using the VM's system-assigned managed identity and use it to call Azure Resource Manager</span></span> 

<span data-ttu-id="a8f0b-128">You will need to use **PowerShell** in this portion.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-128">You will need to use **PowerShell** in this portion.</span></span>  <span data-ttu-id="a8f0b-129">If you don’t have **PowerShell** installed, download it [here](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span><span class="sxs-lookup"><span data-stu-id="a8f0b-129">If you don’t have **PowerShell** installed, download it [here](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span> 

1.  <span data-ttu-id="a8f0b-130">In the portal, navigate to **Virtual Machines** and go to your Windows virtual machine and in the **Overview**, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-130">In the portal, navigate to **Virtual Machines** and go to your Windows virtual machine and in the **Overview**, click **Connect**.</span></span> 
2.  <span data-ttu-id="a8f0b-131">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-131">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span></span> 
3.  <span data-ttu-id="a8f0b-132">Now that you have created a **Remote Desktop Connection** with the virtual machine, open **PowerShell** in the remote session.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-132">Now that you have created a **Remote Desktop Connection** with the virtual machine, open **PowerShell** in the remote session.</span></span> 
4.  <span data-ttu-id="a8f0b-133">Using Powershell’s Invoke-WebRequest, make a request to the local managed identity for Azure resources endpoint to get an access token for Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-133">Using Powershell’s Invoke-WebRequest, make a request to the local managed identity for Azure resources endpoint to get an access token for Azure Resource Manager.</span></span>

    ```powershell
       $response = Invoke-WebRequest -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -Method GET -Headers @{Metadata="true"}
    ```
    
    > [!NOTE]
    > <span data-ttu-id="a8f0b-134">The value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-134">The value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span></span> <span data-ttu-id="a8f0b-135">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-135">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span></span>
    
    <span data-ttu-id="a8f0b-136">Next, extract the full response, which is stored as a JavaScript Object Notation (JSON) formatted string in the $response object.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-136">Next, extract the full response, which is stored as a JavaScript Object Notation (JSON) formatted string in the $response object.</span></span> 
    
    ```powershell
    $content = $response.Content | ConvertFrom-Json
    ```
    <span data-ttu-id="a8f0b-137">Next, extract the access token from the response.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-137">Next, extract the access token from the response.</span></span>
    
    ```powershell
    $ArmToken = $content.access_token
    ```
    
    <span data-ttu-id="a8f0b-138">Finally, call Azure Resource Manager using the access token.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-138">Finally, call Azure Resource Manager using the access token.</span></span> <span data-ttu-id="a8f0b-139">In this example, we're also using PowerShell's Invoke-WebRequest to make the call to Azure Resource Manager, and include the access token in the Authorization header.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-139">In this example, we're also using PowerShell's Invoke-WebRequest to make the call to Azure Resource Manager, and include the access token in the Authorization header.</span></span>
    
    ```powershell
    (Invoke-WebRequest -Uri https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>?api-version=2016-06-01 -Method GET -ContentType "application/json" -Headers @{ Authorization ="Bearer $ArmToken"}).content
    ```
    > [!NOTE] 
    > <span data-ttu-id="a8f0b-140">The URL is case-sensitive, so ensure if you are using the exact same case as you used earlier when you named the Resource Group, and the uppercase "G" in "resourceGroups."</span><span class="sxs-lookup"><span data-stu-id="a8f0b-140">The URL is case-sensitive, so ensure if you are using the exact same case as you used earlier when you named the Resource Group, and the uppercase "G" in "resourceGroups."</span></span>
        
    <span data-ttu-id="a8f0b-141">The following command returns the details of the Resource Group:</span><span class="sxs-lookup"><span data-stu-id="a8f0b-141">The following command returns the details of the Resource Group:</span></span>

    ```powershell
    {"id":"/subscriptions/98f51385-2edc-4b79-bed9-7718de4cb861/resourceGroups/DevTest","name":"DevTest","location":"westus","properties":{"provisioningState":"Succeeded"}}
    ```

## <a name="next-steps"></a><span data-ttu-id="a8f0b-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8f0b-142">Next steps</span></span>

<span data-ttu-id="a8f0b-143">In this quickstart, you learned how to use a system-assigned managed identity to access the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="a8f0b-143">In this quickstart, you learned how to use a system-assigned managed identity to access the Azure Resource Manager API.</span></span>  <span data-ttu-id="a8f0b-144">To learn more about Azure Resource Manager see:</span><span class="sxs-lookup"><span data-stu-id="a8f0b-144">To learn more about Azure Resource Manager see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="a8f0b-145">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8f0b-145">Azure Resource Manager</span></span>](/azure/azure-resource-manager/resource-group-overview)

