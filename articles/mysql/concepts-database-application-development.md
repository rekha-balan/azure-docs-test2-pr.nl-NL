---
title: Database application development overview for Azure Database for MySQL
description: Introduces design considerations that a developer should follow when writing application code to connect to Azure Database for MySQL
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: b733468d41afacb616c95f0628e7bad6b0c837f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966448"
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="ade09-103">Application development overview for Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="ade09-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="ade09-104">This article discusses design considerations that a developer should follow when writing application code to connect to Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="ade09-104">This article discusses design considerations that a developer should follow when writing application code to connect to Azure Database for MySQL.</span></span> 

> [!TIP]
> <span data-ttu-id="ade09-105">For a tutorial showing you how to create a server, create a server-based firewall, view server properties, create database, and connect and query by using workbench and mysql.exe, see [Design your first Azure Database for MySQL database](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ade09-105">For a tutorial showing you how to create a server, create a server-based firewall, view server properties, create database, and connect and query by using workbench and mysql.exe, see [Design your first Azure Database for MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="ade09-106">Language and platform</span><span class="sxs-lookup"><span data-stu-id="ade09-106">Language and platform</span></span>
<span data-ttu-id="ade09-107">There are code samples available for various programming languages and platforms.</span><span class="sxs-lookup"><span data-stu-id="ade09-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="ade09-108">You can find links to the code samples at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="ade09-108">You can find links to the code samples at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="ade09-109">Tools</span><span class="sxs-lookup"><span data-stu-id="ade09-109">Tools</span></span>
<span data-ttu-id="ade09-110">Azure Database for MySQL uses the MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span><span class="sxs-lookup"><span data-stu-id="ade09-110">Azure Database for MySQL uses the MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="ade09-111">You can also use the Azure portal, Azure CLI, and REST APIs to interact with the database service.</span><span class="sxs-lookup"><span data-stu-id="ade09-111">You can also use the Azure portal, Azure CLI, and REST APIs to interact with the database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="ade09-112">Resource limitations</span><span class="sxs-lookup"><span data-stu-id="ade09-112">Resource limitations</span></span>
<span data-ttu-id="ade09-113">Azure Database for MySQL manages the resources available to a server by using two different mechanisms:</span><span class="sxs-lookup"><span data-stu-id="ade09-113">Azure Database for MySQL manages the resources available to a server by using two different mechanisms:</span></span> 
- <span data-ttu-id="ade09-114">Resources Governance.</span><span class="sxs-lookup"><span data-stu-id="ade09-114">Resources Governance.</span></span>
- <span data-ttu-id="ade09-115">Enforcement of Limits.</span><span class="sxs-lookup"><span data-stu-id="ade09-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="ade09-116">Security</span><span class="sxs-lookup"><span data-stu-id="ade09-116">Security</span></span>
<span data-ttu-id="ade09-117">Azure Database for MySQL provides resources for limiting access, protecting data, configuring users and roles, and monitoring activities on a MySQL database.</span><span class="sxs-lookup"><span data-stu-id="ade09-117">Azure Database for MySQL provides resources for limiting access, protecting data, configuring users and roles, and monitoring activities on a MySQL database.</span></span>

## <a name="authentication"></a><span data-ttu-id="ade09-118">Authentication</span><span class="sxs-lookup"><span data-stu-id="ade09-118">Authentication</span></span>
<span data-ttu-id="ade09-119">Azure Database for MySQL supports server authentication of users and logins.</span><span class="sxs-lookup"><span data-stu-id="ade09-119">Azure Database for MySQL supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="ade09-120">Resiliency</span><span class="sxs-lookup"><span data-stu-id="ade09-120">Resiliency</span></span>
<span data-ttu-id="ade09-121">When a transient error occurs while connecting to a MySQL database, your code should retry the call.</span><span class="sxs-lookup"><span data-stu-id="ade09-121">When a transient error occurs while connecting to a MySQL database, your code should retry the call.</span></span> <span data-ttu-id="ade09-122">We recommend that the retry logic use back off logic so that it does not overwhelm the SQL database with multiple clients retrying simultaneously.</span><span class="sxs-lookup"><span data-stu-id="ade09-122">We recommend that the retry logic use back off logic so that it does not overwhelm the SQL database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="ade09-123">Code samples: For code samples that illustrate retry logic, see samples for the language of your choice at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="ade09-123">Code samples: For code samples that illustrate retry logic, see samples for the language of your choice at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="ade09-124">Managing connections</span><span class="sxs-lookup"><span data-stu-id="ade09-124">Managing connections</span></span>
<span data-ttu-id="ade09-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL database to achieve better performance.</span><span class="sxs-lookup"><span data-stu-id="ade09-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL database to achieve better performance.</span></span>
- <span data-ttu-id="ade09-126">Access the database by using connection pooling or persistent connections.</span><span class="sxs-lookup"><span data-stu-id="ade09-126">Access the database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="ade09-127">Access the database by using short connection life span.</span><span class="sxs-lookup"><span data-stu-id="ade09-127">Access the database by using short connection life span.</span></span> 
- <span data-ttu-id="ade09-128">Use retry logic in your application at the point of the connection attempt to catch failures resulting from concurrent connections have reached the maximum allowed.</span><span class="sxs-lookup"><span data-stu-id="ade09-128">Use retry logic in your application at the point of the connection attempt to catch failures resulting from concurrent connections have reached the maximum allowed.</span></span> <span data-ttu-id="ade09-129">In the retry logic, set a short delay, and then wait for a random time before the additional connection attempts.</span><span class="sxs-lookup"><span data-stu-id="ade09-129">In the retry logic, set a short delay, and then wait for a random time before the additional connection attempts.</span></span>