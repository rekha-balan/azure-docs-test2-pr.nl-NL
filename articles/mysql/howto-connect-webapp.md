---
title: Connect existing Azure App Service to Azure Database for MySQL
description: Instructions for how to properly connect an existing Azure App Service to Azure Database for MySQL
services: mysql
author: ajlam
ms.author: andrela
editor: jasonwhowell
manager: kfile
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: ff4a28e2f9a0149016d0e47c24e4665ab2e0500d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857288"
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a><span data-ttu-id="a2ea1-103">Connect an existing Azure App Service to Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="a2ea1-103">Connect an existing Azure App Service to Azure Database for MySQL server</span></span>
<span data-ttu-id="a2ea1-104">This topic explains how to connect an existing Azure App Service to your Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-104">This topic explains how to connect an existing Azure App Service to your Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a2ea1-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a2ea1-105">Before you begin</span></span>
<span data-ttu-id="a2ea1-106">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2ea1-106">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a2ea1-107">Create an Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="a2ea1-108">For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a2ea1-108">For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="a2ea1-109">Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-109">Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL.</span></span> <span data-ttu-id="a2ea1-110">Both solutions involve setting up server-level firewall rules.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a><span data-ttu-id="a2ea1-111">Solution 1 - Create a firewall rule to allow all IPs</span><span class="sxs-lookup"><span data-stu-id="a2ea1-111">Solution 1 - Create a firewall rule to allow all IPs</span></span>
<span data-ttu-id="a2ea1-112">Azure Database for MySQL provides access security using a firewall to protect your data.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-112">Azure Database for MySQL provides access security using a firewall to protect your data.</span></span> <span data-ttu-id="a2ea1-113">When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-113">When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="a2ea1-114">To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-114">To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="a2ea1-115">Microsoft is working on a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-115">Microsoft is working on a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.</span></span>

1. <span data-ttu-id="a2ea1-116">On the MySQL server blade, under the Settings heading, click **Connection Security** to open the Connection Security blade for Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-116">On the MySQL server blade, under the Settings heading, click **Connection Security** to open the Connection Security blade for Azure Database for MySQL.</span></span>

   ![Azure portal - click Connection Security](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="a2ea1-118">Enter **RULE NAME**, **START IP**, and **END IP**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-118">Enter **RULE NAME**, **START IP**, and **END IP**, and then click **Save**.</span></span>
   - <span data-ttu-id="a2ea1-119">Rule name: Allow-All-IPs</span><span class="sxs-lookup"><span data-stu-id="a2ea1-119">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="a2ea1-120">Start IP: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="a2ea1-120">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="a2ea1-121">End IP: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="a2ea1-121">End IP: 255.255.255.255</span></span>

   ![Azure portal - Add all IPs](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a><span data-ttu-id="a2ea1-123">Solution 2 - Create a firewall rule to explicitly allow outbound IPs</span><span class="sxs-lookup"><span data-stu-id="a2ea1-123">Solution 2 - Create a firewall rule to explicitly allow outbound IPs</span></span>
<span data-ttu-id="a2ea1-124">You can explicitly add all the outbound IPs of your Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-124">You can explicitly add all the outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="a2ea1-125">On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-125">On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Azure portal - View outbound IPs](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="a2ea1-127">On the MySQL Connection security blade, add outbound IPs one by one.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-127">On the MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Azure portal - Add explicit IPs](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="a2ea1-129">Remember to **Save** your firewall rules.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-129">Remember to **Save** your firewall rules.</span></span>

<span data-ttu-id="a2ea1-130">Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-130">Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change.</span></span> <span data-ttu-id="a2ea1-131">For example, this can occur when the app recycles or a scale operation occurs, or when new computers are added in Azure regional data centers to increase capacity.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-131">For example, this can occur when the app recycles or a scale operation occurs, or when new computers are added in Azure regional data centers to increase capacity.</span></span> <span data-ttu-id="a2ea1-132">When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-132">When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server.</span></span> <span data-ttu-id="a2ea1-133">Keep this consideration in mind when choosing one of the preceding solutions.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-133">Keep this consideration in mind when choosing one of the preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="a2ea1-134">SSL configuration</span><span class="sxs-lookup"><span data-stu-id="a2ea1-134">SSL configuration</span></span>
<span data-ttu-id="a2ea1-135">Azure Database for MySQL has SSL enabled by default.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-135">Azure Database for MySQL has SSL enabled by default.</span></span> <span data-ttu-id="a2ea1-136">If your application is not using SSL to connect to the database, then you need to disable SSL on the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="a2ea1-136">If your application is not using SSL to connect to the database, then you need to disable SSL on the MySQL server.</span></span> <span data-ttu-id="a2ea1-137">For details on how to configure SSL, see [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a2ea1-137">For details on how to configure SSL, see [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2ea1-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2ea1-138">Next steps</span></span>
<span data-ttu-id="a2ea1-139">For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="a2ea1-139">For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).</span></span>
