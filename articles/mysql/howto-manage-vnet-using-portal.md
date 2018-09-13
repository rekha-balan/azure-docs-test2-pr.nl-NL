---
title: Create and manage Azure Database for MySQL VNet service endpoints and rules using the Azure portal | Microsoft Docs
description: Create and manage Azure Database for MySQL VNet service endpoints and rules using the Azure portal
services: mysql
author: mbolz
ms.author: mbolz
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 08/15/2018
ms.openlocfilehash: df703f30119e0cb421b21c524f779b4f43a42b3f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966617"
---
# <a name="create-and-manage-azure-database-for-mysql-vnet-service-endpoints-and-vnet-rules-by-using-the-azure-portal"></a><span data-ttu-id="d7bbd-103">Create and manage Azure Database for MySQL VNet service endpoints and VNet rules by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d7bbd-103">Create and manage Azure Database for MySQL VNet service endpoints and VNet rules by using the Azure portal</span></span>
<span data-ttu-id="d7bbd-104">Virtual Network (VNet) services endpoints and rules extend the private address space of a Virtual Network to your Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-104">Virtual Network (VNet) services endpoints and rules extend the private address space of a Virtual Network to your Azure Database for MySQL server.</span></span> <span data-ttu-id="d7bbd-105">For an overview of Azure Database for MySQL VNet service endpoints, including limitations, see [Azure Database for MySQL Server VNet service endpoints](concepts-data-access-and-security-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="d7bbd-105">For an overview of Azure Database for MySQL VNet service endpoints, including limitations, see [Azure Database for MySQL Server VNet service endpoints](concepts-data-access-and-security-vnet.md).</span></span> <span data-ttu-id="d7bbd-106">VNet service endpoints are available in all supported regions for Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-106">VNet service endpoints are available in all supported regions for Azure Database for MySQL.</span></span>

> [!NOTE]
> <span data-ttu-id="d7bbd-107">Support for VNet service endpoints is only for General Purpose and Memory Optimized servers.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-107">Support for VNet service endpoints is only for General Purpose and Memory Optimized servers.</span></span>

## <a name="create-a-vnet-rule-and-enable-service-endpoints-in-the-azure-portal"></a><span data-ttu-id="d7bbd-108">Create a VNet rule and enable service endpoints in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d7bbd-108">Create a VNet rule and enable service endpoints in the Azure portal</span></span>

1. <span data-ttu-id="d7bbd-109">On the MySQL server page, under the Settings heading, click **Connection Security** to open the Connection Security pane for Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-109">On the MySQL server page, under the Settings heading, click **Connection Security** to open the Connection Security pane for Azure Database for MySQL.</span></span> <span data-ttu-id="d7bbd-110">Next, click on **+ Adding existing virtual network**.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-110">Next, click on **+ Adding existing virtual network**.</span></span> <span data-ttu-id="d7bbd-111">If you do not have an existing VNet you can click **+ Create new virtual network** to create one.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-111">If you do not have an existing VNet you can click **+ Create new virtual network** to create one.</span></span> <span data-ttu-id="d7bbd-112">See [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d7bbd-112">See [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md)</span></span>

   ![Azure portal - click Connection security](./media/howto-manage-vnet-using-portal/1-connection-security.png)

2. <span data-ttu-id="d7bbd-114">Enter a VNet rule name, select the subscription, Virtual network and Subnet name and then click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-114">Enter a VNet rule name, select the subscription, Virtual network and Subnet name and then click **Enable**.</span></span> <span data-ttu-id="d7bbd-115">This automatically enables VNet service endpoints on the subnet using the **Microsoft.SQL** service tag.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-115">This automatically enables VNet service endpoints on the subnet using the **Microsoft.SQL** service tag.</span></span>

   ![Azure portal - configure VNet](./media/howto-manage-vnet-using-portal/2-configure-vnet.png)

   > [!IMPORTANT]
   > <span data-ttu-id="d7bbd-117">It is highly recommended to read this article about service endpoint configurations and considerations before configuring service endpoints.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-117">It is highly recommended to read this article about service endpoint configurations and considerations before configuring service endpoints.</span></span> <span data-ttu-id="d7bbd-118">**Virtual Network service endpoint:** A [Virtual Network service endpoint](../virtual-network/virtual-network-service-endpoints-overview.md) is a subnet whose property values include one or more formal Azure service type names.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-118">**Virtual Network service endpoint:** A [Virtual Network service endpoint](../virtual-network/virtual-network-service-endpoints-overview.md) is a subnet whose property values include one or more formal Azure service type names.</span></span> <span data-ttu-id="d7bbd-119">VNet services endpoints use the service type name **Microsoft.Sql**, which refers to the Azure service named SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-119">VNet services endpoints use the service type name **Microsoft.Sql**, which refers to the Azure service named SQL Database.</span></span> <span data-ttu-id="d7bbd-120">This service tag also applies to the Azure SQL Database, Azure Database for PostgreSQL and MySQL services.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-120">This service tag also applies to the Azure SQL Database, Azure Database for PostgreSQL and MySQL services.</span></span> <span data-ttu-id="d7bbd-121">It is important to note when applying the **Microsoft.Sql** service tag to a VNet service endpoint it configures service endpoint traffic for all Azure Database services, including Azure SQL Database, Azure Database for PostgreSQL and Azure Database for MySQL servers on the subnet.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-121">It is important to note when applying the **Microsoft.Sql** service tag to a VNet service endpoint it configures service endpoint traffic for all Azure Database services, including Azure SQL Database, Azure Database for PostgreSQL and Azure Database for MySQL servers on the subnet.</span></span> 
   > 

3. <span data-ttu-id="d7bbd-122">Once enabled, click **OK** and you will see that VNet service endpoints are enabled along with a VNet rule.</span><span class="sxs-lookup"><span data-stu-id="d7bbd-122">Once enabled, click **OK** and you will see that VNet service endpoints are enabled along with a VNet rule.</span></span>

   ![VNet service endpoints enabled and VNet rule created](./media/howto-manage-vnet-using-portal/3-vnet-service-endpoints-enabled-vnet-rule-created.png)

## <a name="next-steps"></a><span data-ttu-id="d7bbd-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7bbd-124">Next steps</span></span>
- <span data-ttu-id="d7bbd-125">Similarly, you can script to [Enable VNet service endpoints and create a VNET rule for Azure Database for MySQL using Azure CLI](howto-manage-vnet-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d7bbd-125">Similarly, you can script to [Enable VNet service endpoints and create a VNET rule for Azure Database for MySQL using Azure CLI](howto-manage-vnet-using-cli.md).</span></span>
- <span data-ttu-id="d7bbd-126">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="d7bbd-126">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
