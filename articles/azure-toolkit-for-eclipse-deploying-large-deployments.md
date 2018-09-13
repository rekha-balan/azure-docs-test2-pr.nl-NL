---
title: Deploying Large Deployments
description: Learn how to deploy large deployments using the Azure Toolkit for Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 9d2096048043b6a64bb5a535b6843e8ebd7e20fd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550415"
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="40124-103">Deploying Large Deployments</span><span class="sxs-lookup"><span data-stu-id="40124-103">Deploying Large Deployments</span></span>
<span data-ttu-id="40124-104">If your deployment is too large to be contained in the default approot folder, you can use a local storage resource as the deployment root folder for your JDK and application server.</span><span class="sxs-lookup"><span data-stu-id="40124-104">If your deployment is too large to be contained in the default approot folder, you can use a local storage resource as the deployment root folder for your JDK and application server.</span></span>

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="40124-105">To use a local storage resource as the deployment root folder for large deployments</span><span class="sxs-lookup"><span data-stu-id="40124-105">To use a local storage resource as the deployment root folder for large deployments</span></span>
1. <span data-ttu-id="40124-106">Create a new local storage resource.</span><span class="sxs-lookup"><span data-stu-id="40124-106">Create a new local storage resource.</span></span> <span data-ttu-id="40124-107">The name of the resource does not matter.</span><span class="sxs-lookup"><span data-stu-id="40124-107">The name of the resource does not matter.</span></span> <span data-ttu-id="40124-108">Storage resources are defined at the role level.</span><span class="sxs-lookup"><span data-stu-id="40124-108">Storage resources are defined at the role level.</span></span> <span data-ttu-id="40124-109">The quickest way to access the local storage configuration dialog, from which you could create a new local storage resource, is by using the following steps: Right-click the role in the **Project Explorer** view (expand your Azure project node if you don't see the role), click **Azure**, and then click **Local Storage**.</span><span class="sxs-lookup"><span data-stu-id="40124-109">The quickest way to access the local storage configuration dialog, from which you could create a new local storage resource, is by using the following steps: Right-click the role in the **Project Explorer** view (expand your Azure project node if you don't see the role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="40124-110">Within the **Local Storage** dialog, click **Add** to create a new local storage resource.</span><span class="sxs-lookup"><span data-stu-id="40124-110">Within the **Local Storage** dialog, click **Add** to create a new local storage resource.</span></span>
2. <span data-ttu-id="40124-111">Set the desired size to at least 2048 MB (anything less may cause the same file size problems as you would encounter in the approot).</span><span class="sxs-lookup"><span data-stu-id="40124-111">Set the desired size to at least 2048 MB (anything less may cause the same file size problems as you would encounter in the approot).</span></span>
3. <span data-ttu-id="40124-112">Ensure that **Clean the contents when the role instance is recycled** is checked; this will help prevent the deployment's startup logic from running into conflicts with pre-existing files in the resource when the role instance is recycled.</span><span class="sxs-lookup"><span data-stu-id="40124-112">Ensure that **Clean the contents when the role instance is recycled** is checked; this will help prevent the deployment's startup logic from running into conflicts with pre-existing files in the resource when the role instance is recycled.</span></span>
4. <span data-ttu-id="40124-113">Ensure that the **Environment variable storing the resource's directory path after deployment** value is set to the string **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="40124-113">Ensure that the **Environment variable storing the resource's directory path after deployment** value is set to the string **DEPLOYROOT**.</span></span> <span data-ttu-id="40124-114">Your local storage resource dialog will look similar to the following.</span><span class="sxs-lookup"><span data-stu-id="40124-114">Your local storage resource dialog will look similar to the following.</span></span>
    ![][ic667943]

<span data-ttu-id="40124-115">Alternatively, if you use **DEPLOYROOT** as the *name* of your local resource and you do not change the automatically-generated environment variable name (which will be set to **DEPLOYROOT_PATH** in that case), that would work for your application as well.</span><span class="sxs-lookup"><span data-stu-id="40124-115">Alternatively, if you use **DEPLOYROOT** as the *name* of your local resource and you do not change the automatically-generated environment variable name (which will be set to **DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="40124-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="40124-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="40124-117">See Also</span><span class="sxs-lookup"><span data-stu-id="40124-117">See Also</span></span>
<span data-ttu-id="40124-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="40124-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="40124-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="40124-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="40124-120">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="40124-120">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="40124-121">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="40124-121">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->

