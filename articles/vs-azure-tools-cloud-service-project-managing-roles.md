---
title: Managing roles in Azure cloud services with Visual Studio | Microsoft Docs
description: Learn how to add and remove roles in Azure cloud services with Visual Studio.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: e45d2c30e8b5522575aaa431292d435e5115f89f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660578"
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="29b87-103">Managing roles in Azure cloud services with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29b87-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="29b87-104">After you have created your Azure cloud service, you can add new roles to it or remove existing roles from it.</span><span class="sxs-lookup"><span data-stu-id="29b87-104">After you have created your Azure cloud service, you can add new roles to it or remove existing roles from it.</span></span> <span data-ttu-id="29b87-105">You can also import an existing project and convert it to a role.</span><span class="sxs-lookup"><span data-stu-id="29b87-105">You can also import an existing project and convert it to a role.</span></span> <span data-ttu-id="29b87-106">For example, you can import an ASP.NET web application and designate it as a web role.</span><span class="sxs-lookup"><span data-stu-id="29b87-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-to-an-azure-cloud-service"></a><span data-ttu-id="29b87-107">Adding a role to an Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="29b87-107">Adding a role to an Azure cloud service</span></span>
<span data-ttu-id="29b87-108">The following steps guide you through adding a web or worker role to an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29b87-108">The following steps guide you through adding a web or worker role to an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="29b87-109">Create or open an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29b87-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="29b87-110">In **Solution Explorer**, expand the project node</span><span class="sxs-lookup"><span data-stu-id="29b87-110">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="29b87-111">Right-click the **Roles** node to display the context menu.</span><span class="sxs-lookup"><span data-stu-id="29b87-111">Right-click the **Roles** node to display the context menu.</span></span> <span data-ttu-id="29b87-112">From the context menu, select **Add**, then select an existing web role or worker role from the current solution, or create a web or worker role project.</span><span class="sxs-lookup"><span data-stu-id="29b87-112">From the context menu, select **Add**, then select an existing web role or worker role from the current solution, or create a web or worker role project.</span></span> <span data-ttu-id="29b87-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span><span class="sxs-lookup"><span data-stu-id="29b87-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Menu options to add a role to an Azure cloud service project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="29b87-115">Removing a role from an Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="29b87-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="29b87-116">The following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29b87-116">The following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="29b87-117">Create or open an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29b87-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="29b87-118">In **Solution Explorer**, expand the project node</span><span class="sxs-lookup"><span data-stu-id="29b87-118">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="29b87-119">Expand the **Roles** node.</span><span class="sxs-lookup"><span data-stu-id="29b87-119">Expand the **Roles** node.</span></span>

1. <span data-ttu-id="29b87-120">Right-click the node you want to remove, and, from the context menu, select **Remove**.</span><span class="sxs-lookup"><span data-stu-id="29b87-120">Right-click the node you want to remove, and, from the context menu, select **Remove**.</span></span> 

    ![Menu options to add a role to an Azure cloud service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-to-an-azure-cloud-service-project"></a><span data-ttu-id="29b87-122">Readding a role to an Azure cloud service project</span><span class="sxs-lookup"><span data-stu-id="29b87-122">Readding a role to an Azure cloud service project</span></span>
<span data-ttu-id="29b87-123">If you remove a role from your cloud service project but later decide to add the role back to the project, only the role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span><span class="sxs-lookup"><span data-stu-id="29b87-123">If you remove a role from your cloud service project but later decide to add the role back to the project, only the role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="29b87-124">No additional resources or references are added to the `ServiceDefinition.csdef` file or to the `ServiceConfiguration.cscfg` file.</span><span class="sxs-lookup"><span data-stu-id="29b87-124">No additional resources or references are added to the `ServiceDefinition.csdef` file or to the `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="29b87-125">If you want to add this information, you need to manually add it back into these files.</span><span class="sxs-lookup"><span data-stu-id="29b87-125">If you want to add this information, you need to manually add it back into these files.</span></span>

<span data-ttu-id="29b87-126">For example, you might remove a web service role and later you decide to add this role back into your solution.</span><span class="sxs-lookup"><span data-stu-id="29b87-126">For example, you might remove a web service role and later you decide to add this role back into your solution.</span></span> <span data-ttu-id="29b87-127">If you do this, an error occurs.</span><span class="sxs-lookup"><span data-stu-id="29b87-127">If you do this, an error occurs.</span></span> <span data-ttu-id="29b87-128">To prevent this error, you have to add the `<LocalResources>` element shown in the following XML back into the `ServiceDefinition.csdef` file.</span><span class="sxs-lookup"><span data-stu-id="29b87-128">To prevent this error, you have to add the `<LocalResources>` element shown in the following XML back into the `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="29b87-129">Use the name of the web service role that you added back into the project as part of the name attribute for the **<LocalStorage>** element.</span><span class="sxs-lookup"><span data-stu-id="29b87-129">Use the name of the web service role that you added back into the project as part of the name attribute for the **<LocalStorage>** element.</span></span> <span data-ttu-id="29b87-130">In this example, the name of the web service role is **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="29b87-130">In this example, the name of the web service role is **WCFServiceWebRole1**.</span></span>

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a><span data-ttu-id="29b87-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="29b87-131">Next steps</span></span>
- [<span data-ttu-id="29b87-132">Configure the Roles for an Azure cloud service with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29b87-132">Configure the Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)


