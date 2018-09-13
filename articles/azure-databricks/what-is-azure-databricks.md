---
title: What is Azure Databricks? | Microsoft Docs
description: Learn about what is Azure Databricks and how it brings Spark on Databricks into Azure. Azure Databricks is an Apache Spark-based analytics platform optimized for the Microsoft Azure cloud services platform.
services: azure-databricks
documentationcenter: ''
author: nitinme
manager: cgronlun
editor: cgronlun
ms.service: azure-databricks
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 05/29/2018
ms.author: nitinme
ms.custom: mvc
ms.openlocfilehash: c621962c8ff0dcdb5070a81c5732012cb0898394
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870248"
---
# <a name="what-is-azure-databricks"></a><span data-ttu-id="ed1d5-105">What is Azure Databricks?</span><span class="sxs-lookup"><span data-stu-id="ed1d5-105">What is Azure Databricks?</span></span>

<span data-ttu-id="ed1d5-106">Azure Databricks is an Apache Spark-based analytics platform optimized for the Microsoft Azure cloud services platform.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-106">Azure Databricks is an Apache Spark-based analytics platform optimized for the Microsoft Azure cloud services platform.</span></span> <span data-ttu-id="ed1d5-107">Designed with the founders of Apache Spark, Databricks is integrated with Azure to provide one-click setup, streamlined workflows, and an interactive workspace that enables collaboration between data scientists, data engineers, and business analysts.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-107">Designed with the founders of Apache Spark, Databricks is integrated with Azure to provide one-click setup, streamlined workflows, and an interactive workspace that enables collaboration between data scientists, data engineers, and business analysts.</span></span>

<span data-ttu-id="ed1d5-108">![What is Azure Databricks?](./media/what-is-azure-databricks/azure-databricks-overview.png "What is Azure Databricks?")</span><span class="sxs-lookup"><span data-stu-id="ed1d5-108">![What is Azure Databricks?](./media/what-is-azure-databricks/azure-databricks-overview.png "What is Azure Databricks?")</span></span>

## <a name="apache-spark-based-analytics-platform"></a><span data-ttu-id="ed1d5-109">Apache Spark-based analytics platform</span><span class="sxs-lookup"><span data-stu-id="ed1d5-109">Apache Spark-based analytics platform</span></span>

<span data-ttu-id="ed1d5-110">Azure Databricks comprises the complete open-source Apache Spark cluster technologies and capabilities.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-110">Azure Databricks comprises the complete open-source Apache Spark cluster technologies and capabilities.</span></span> <span data-ttu-id="ed1d5-111">Spark in Azure Databricks includes the following components:</span><span class="sxs-lookup"><span data-stu-id="ed1d5-111">Spark in Azure Databricks includes the following components:</span></span>

<span data-ttu-id="ed1d5-112">![Apache Spark in Azure Databricks](./media/what-is-azure-databricks/apache-spark-ecosystem-databricks.png "Apache Spark in Azure Databricks")</span><span class="sxs-lookup"><span data-stu-id="ed1d5-112">![Apache Spark in Azure Databricks](./media/what-is-azure-databricks/apache-spark-ecosystem-databricks.png "Apache Spark in Azure Databricks")</span></span>

* <span data-ttu-id="ed1d5-113">**Spark SQL and DataFrames**: Spark SQL is the Spark module for working with structured data.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-113">**Spark SQL and DataFrames**: Spark SQL is the Spark module for working with structured data.</span></span> <span data-ttu-id="ed1d5-114">A DataFrame is a distributed collection of data organized into named columns.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-114">A DataFrame is a distributed collection of data organized into named columns.</span></span> <span data-ttu-id="ed1d5-115">It is conceptually equivalent to a table in a relational database or a data frame in R/Python.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-115">It is conceptually equivalent to a table in a relational database or a data frame in R/Python.</span></span>

* <span data-ttu-id="ed1d5-116">**Streaming**: Real-time data processing and analysis for analytical and interactive applications.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-116">**Streaming**: Real-time data processing and analysis for analytical and interactive applications.</span></span> <span data-ttu-id="ed1d5-117">Integrates with HDFS, Flume, and Kafka.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-117">Integrates with HDFS, Flume, and Kafka.</span></span>

* <span data-ttu-id="ed1d5-118">**MLib**: Machine Learning library consisting of common learning algorithms and utilities, including classification, regression, clustering, collaborative filtering, dimensionality reduction, as well as underlying optimization primitives.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-118">**MLib**: Machine Learning library consisting of common learning algorithms and utilities, including classification, regression, clustering, collaborative filtering, dimensionality reduction, as well as underlying optimization primitives.</span></span>

* <span data-ttu-id="ed1d5-119">**GraphX**: Graphs and graph computation for a broad scope of use cases from cognitive analytics to data exploration.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-119">**GraphX**: Graphs and graph computation for a broad scope of use cases from cognitive analytics to data exploration.</span></span>

* <span data-ttu-id="ed1d5-120">**Spark Core API**: Includes support for R, SQL, Python, Scala, and Java.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-120">**Spark Core API**: Includes support for R, SQL, Python, Scala, and Java.</span></span>

## <a name="apache-spark-in-azure-databricks"></a><span data-ttu-id="ed1d5-121">Apache Spark in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="ed1d5-121">Apache Spark in Azure Databricks</span></span>

<span data-ttu-id="ed1d5-122">Azure Databricks builds on the capabilities of Spark by providing a zero-management cloud platform that includes:</span><span class="sxs-lookup"><span data-stu-id="ed1d5-122">Azure Databricks builds on the capabilities of Spark by providing a zero-management cloud platform that includes:</span></span>

- <span data-ttu-id="ed1d5-123">Fully managed Spark clusters</span><span class="sxs-lookup"><span data-stu-id="ed1d5-123">Fully managed Spark clusters</span></span>
- <span data-ttu-id="ed1d5-124">An interactive workspace for exploration and visualization</span><span class="sxs-lookup"><span data-stu-id="ed1d5-124">An interactive workspace for exploration and visualization</span></span>
- <span data-ttu-id="ed1d5-125">A platform for powering your favorite Spark-based applications</span><span class="sxs-lookup"><span data-stu-id="ed1d5-125">A platform for powering your favorite Spark-based applications</span></span>

### <a name="fully-managed-apache-spark-clusters-in-the-cloud"></a><span data-ttu-id="ed1d5-126">Fully managed Apache Spark clusters in the cloud</span><span class="sxs-lookup"><span data-stu-id="ed1d5-126">Fully managed Apache Spark clusters in the cloud</span></span>

<span data-ttu-id="ed1d5-127">Azure Databricks has a secure and reliable production environment in the cloud, managed and supported by Spark experts.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-127">Azure Databricks has a secure and reliable production environment in the cloud, managed and supported by Spark experts.</span></span> <span data-ttu-id="ed1d5-128">You can:</span><span class="sxs-lookup"><span data-stu-id="ed1d5-128">You can:</span></span>

* <span data-ttu-id="ed1d5-129">Create clusters in seconds.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-129">Create clusters in seconds.</span></span>
* <span data-ttu-id="ed1d5-130">Dynamically autoscale clusters up and down, including serverless clusters, and share them across teams.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-130">Dynamically autoscale clusters up and down, including serverless clusters, and share them across teams.</span></span> 
* <span data-ttu-id="ed1d5-131">Use clusters programmatically by using the REST APIs.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-131">Use clusters programmatically by using the REST APIs.</span></span> 
* <span data-ttu-id="ed1d5-132">Use secure data integration capabilities built on top of Spark that enable you to unify your data without centralization.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-132">Use secure data integration capabilities built on top of Spark that enable you to unify your data without centralization.</span></span> 
* <span data-ttu-id="ed1d5-133">Get instant access to the latest Apache Spark features with each release.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-133">Get instant access to the latest Apache Spark features with each release.</span></span>

### <a name="databricks-runtime"></a><span data-ttu-id="ed1d5-134">Databricks Runtime</span><span class="sxs-lookup"><span data-stu-id="ed1d5-134">Databricks Runtime</span></span>
<span data-ttu-id="ed1d5-135">The Databricks Runtime is built on top of Apache Spark and is natively built for the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-135">The Databricks Runtime is built on top of Apache Spark and is natively built for the Azure cloud.</span></span> 

<span data-ttu-id="ed1d5-136">With the **Serverless** option, Azure Databricks completely abstracts out the infrastructure complexity and the need for specialized expertise to set up and configure your data infrastructure.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-136">With the **Serverless** option, Azure Databricks completely abstracts out the infrastructure complexity and the need for specialized expertise to set up and configure your data infrastructure.</span></span> <span data-ttu-id="ed1d5-137">The Serverless option helps data scientists iterate quickly as a team.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-137">The Serverless option helps data scientists iterate quickly as a team.</span></span>

<span data-ttu-id="ed1d5-138">For data engineers, who care about the performance of production jobs, Azure Databricks provides a Spark engine that is faster and performant through various optimizations at the I/O layer and processing layer (Databricks I/O).</span><span class="sxs-lookup"><span data-stu-id="ed1d5-138">For data engineers, who care about the performance of production jobs, Azure Databricks provides a Spark engine that is faster and performant through various optimizations at the I/O layer and processing layer (Databricks I/O).</span></span>

### <a name="workspace-for-collaboration"></a><span data-ttu-id="ed1d5-139">Workspace for collaboration</span><span class="sxs-lookup"><span data-stu-id="ed1d5-139">Workspace for collaboration</span></span>

<span data-ttu-id="ed1d5-140">Through a collaborative and integrated environment, Azure Databricks streamlines the process of exploring data, prototyping, and running data-driven applications in Spark.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-140">Through a collaborative and integrated environment, Azure Databricks streamlines the process of exploring data, prototyping, and running data-driven applications in Spark.</span></span>

* <span data-ttu-id="ed1d5-141">Determine how to use data with easy data exploration.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-141">Determine how to use data with easy data exploration.</span></span>
* <span data-ttu-id="ed1d5-142">Document your progress in notebooks in R, Python, Scala, or SQL.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-142">Document your progress in notebooks in R, Python, Scala, or SQL.</span></span>
* <span data-ttu-id="ed1d5-143">Visualize data in a few clicks, and use familiar tools like Matplotlib, ggplot, or d3.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-143">Visualize data in a few clicks, and use familiar tools like Matplotlib, ggplot, or d3.</span></span>
* <span data-ttu-id="ed1d5-144">Use interactive dashboards to create dynamic reports.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-144">Use interactive dashboards to create dynamic reports.</span></span>
* <span data-ttu-id="ed1d5-145">Use Spark and interact with the data simultaneously.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-145">Use Spark and interact with the data simultaneously.</span></span>

## <a name="enterprise-security"></a><span data-ttu-id="ed1d5-146">Enterprise security</span><span class="sxs-lookup"><span data-stu-id="ed1d5-146">Enterprise security</span></span>

<span data-ttu-id="ed1d5-147">Azure Databricks provides enterprise-grade Azure security, including Azure Active Directory integration, role-based controls, and SLAs that protect your data and your business.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-147">Azure Databricks provides enterprise-grade Azure security, including Azure Active Directory integration, role-based controls, and SLAs that protect your data and your business.</span></span>

* <span data-ttu-id="ed1d5-148">Integration with Azure Active Directory enables you to run complete Azure-based solutions using Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-148">Integration with Azure Active Directory enables you to run complete Azure-based solutions using Azure Databricks.</span></span>
* <span data-ttu-id="ed1d5-149">Azure Databricks roles-based access enables fine-grained user permissions for notebooks, clusters, jobs, and data.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-149">Azure Databricks roles-based access enables fine-grained user permissions for notebooks, clusters, jobs, and data.</span></span>
* <span data-ttu-id="ed1d5-150">Enterprise-grade SLAs.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-150">Enterprise-grade SLAs.</span></span> 

## <a name="integration-with-azure-services"></a><span data-ttu-id="ed1d5-151">Integration with Azure services</span><span class="sxs-lookup"><span data-stu-id="ed1d5-151">Integration with Azure services</span></span>

<span data-ttu-id="ed1d5-152">Azure Databricks integrates deeply with Azure databases and stores: SQL Data Warehouse, Cosmos DB, Data Lake Store, and Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-152">Azure Databricks integrates deeply with Azure databases and stores: SQL Data Warehouse, Cosmos DB, Data Lake Store, and Blob Storage.</span></span> 

## <a name="integration-with-power-bi"></a><span data-ttu-id="ed1d5-153">Integration with Power BI</span><span class="sxs-lookup"><span data-stu-id="ed1d5-153">Integration with Power BI</span></span>
<span data-ttu-id="ed1d5-154">Through rich integration with Power BI, Azure Databricks allows you to discover and share your impactful insights quickly and easily.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-154">Through rich integration with Power BI, Azure Databricks allows you to discover and share your impactful insights quickly and easily.</span></span> <span data-ttu-id="ed1d5-155">You can use other BI tools as well, such as Tableau Software via JDBC/ODBC cluster endpoints.</span><span class="sxs-lookup"><span data-stu-id="ed1d5-155">You can use other BI tools as well, such as Tableau Software via JDBC/ODBC cluster endpoints.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed1d5-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="ed1d5-156">Next steps</span></span>

* [<span data-ttu-id="ed1d5-157">Quickstart: Run a Spark job on Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="ed1d5-157">Quickstart: Run a Spark job on Azure Databricks</span></span>](quickstart-create-databricks-workspace-portal.md)
* [<span data-ttu-id="ed1d5-158">Work with Spark clusters</span><span class="sxs-lookup"><span data-stu-id="ed1d5-158">Work with Spark clusters</span></span>](https://docs.azuredatabricks.net/user-guide/clusters/index.html)
* [<span data-ttu-id="ed1d5-159">Work with notebooks</span><span class="sxs-lookup"><span data-stu-id="ed1d5-159">Work with notebooks</span></span>](https://docs.azuredatabricks.net/user-guide/notebooks/index.html)
* [<span data-ttu-id="ed1d5-160">Create Spark jobs</span><span class="sxs-lookup"><span data-stu-id="ed1d5-160">Create Spark jobs</span></span>](https://docs.azuredatabricks.net/user-guide/jobs.html)

 









