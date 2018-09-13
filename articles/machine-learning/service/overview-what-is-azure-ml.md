---
title: What is Azure Machine Learning? | Microsoft Docs
description: Explains basic concepts of machine learning in the cloud, describes what you can use it for, and defines machine learning terms. Overview of Azure Machine Learning -- an integrated, end-to-end data science solution for professional data scientists to develop, experiment and deploy advanced analytics applications at cloud scale.
services: machine-learning
author: mwinkle
ms.author: mwinkle
manager: cgronlun
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: overview
ms.date: 09/21/2017
ms.openlocfilehash: 3e744b0e4a7ccebcdedac5a822ff717bed6b1f72
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869888"
---
# <a name="what-is-machine-learning"></a><span data-ttu-id="51458-105">What is Machine Learning?</span><span class="sxs-lookup"><span data-stu-id="51458-105">What is Machine Learning?</span></span>

<span data-ttu-id="51458-106">Machine learning is a data science technique that allows computers to use existing data to forecast future behaviors, outcomes, and trends.</span><span class="sxs-lookup"><span data-stu-id="51458-106">Machine learning is a data science technique that allows computers to use existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="51458-107">Using machine learning, computers learn without being explicitly programmed.</span><span class="sxs-lookup"><span data-stu-id="51458-107">Using machine learning, computers learn without being explicitly programmed.</span></span>

<span data-ttu-id="51458-108">Forecasts or predictions from machine learning can make apps and devices smarter.</span><span class="sxs-lookup"><span data-stu-id="51458-108">Forecasts or predictions from machine learning can make apps and devices smarter.</span></span> <span data-ttu-id="51458-109">When you shop online, machine learning helps recommend other products you might like based on what you've purchased.</span><span class="sxs-lookup"><span data-stu-id="51458-109">When you shop online, machine learning helps recommend other products you might like based on what you've purchased.</span></span> <span data-ttu-id="51458-110">When your credit card is swiped, machine learning compares the transaction to a database of transactions and helps detect fraud.</span><span class="sxs-lookup"><span data-stu-id="51458-110">When your credit card is swiped, machine learning compares the transaction to a database of transactions and helps detect fraud.</span></span> <span data-ttu-id="51458-111">When your robot vacuum cleaner vacuums a room, machine learning helps it decide whether the job is done.</span><span class="sxs-lookup"><span data-stu-id="51458-111">When your robot vacuum cleaner vacuums a room, machine learning helps it decide whether the job is done.</span></span>

## <a name="what-is-azure-machine-learning"></a><span data-ttu-id="51458-112">What is Azure Machine Learning?</span><span class="sxs-lookup"><span data-stu-id="51458-112">What is Azure Machine Learning?</span></span>
<span data-ttu-id="51458-113">Azure Machine Learning is an integrated, end-to-end data science and advanced analytics solution.</span><span class="sxs-lookup"><span data-stu-id="51458-113">Azure Machine Learning is an integrated, end-to-end data science and advanced analytics solution.</span></span> <span data-ttu-id="51458-114">It enables data scientists to prepare data, develop experiments, and deploy models at cloud scale.</span><span class="sxs-lookup"><span data-stu-id="51458-114">It enables data scientists to prepare data, develop experiments, and deploy models at cloud scale.</span></span>

<span data-ttu-id="51458-115">The main components of Azure Machine Learning are:</span><span class="sxs-lookup"><span data-stu-id="51458-115">The main components of Azure Machine Learning are:</span></span>
- <span data-ttu-id="51458-116">Azure Machine Learning Workbench</span><span class="sxs-lookup"><span data-stu-id="51458-116">Azure Machine Learning Workbench</span></span>
- <span data-ttu-id="51458-117">Azure Machine Learning Experimentation Service</span><span class="sxs-lookup"><span data-stu-id="51458-117">Azure Machine Learning Experimentation Service</span></span>
- <span data-ttu-id="51458-118">Azure Machine Learning Model Management Service</span><span class="sxs-lookup"><span data-stu-id="51458-118">Azure Machine Learning Model Management Service</span></span>
- <span data-ttu-id="51458-119">Microsoft Machine Learning Libraries for Apache Spark (MMLSpark Library)</span><span class="sxs-lookup"><span data-stu-id="51458-119">Microsoft Machine Learning Libraries for Apache Spark (MMLSpark Library)</span></span>
- <span data-ttu-id="51458-120">Visual Studio Code Tools for AI</span><span class="sxs-lookup"><span data-stu-id="51458-120">Visual Studio Code Tools for AI</span></span>

<span data-ttu-id="51458-121">Together, these applications and services help significantly accelerate your data science project development and deployment.</span><span class="sxs-lookup"><span data-stu-id="51458-121">Together, these applications and services help significantly accelerate your data science project development and deployment.</span></span> 

![Azure Machine Learning Concepts](./media/overview-what-is-azure-ml/aml-concepts.png)


## <a name="open-source-compatible"></a><span data-ttu-id="51458-123">Open source compatible</span><span class="sxs-lookup"><span data-stu-id="51458-123">Open source compatible</span></span>

<span data-ttu-id="51458-124">Azure Machine Learning fully supports open source technologies.</span><span class="sxs-lookup"><span data-stu-id="51458-124">Azure Machine Learning fully supports open source technologies.</span></span> <span data-ttu-id="51458-125">You can use tens of thousands of open source Python packages, such as the following machine learning frameworks:</span><span class="sxs-lookup"><span data-stu-id="51458-125">You can use tens of thousands of open source Python packages, such as the following machine learning frameworks:</span></span>

- [<span data-ttu-id="51458-126">scikit-learn</span><span class="sxs-lookup"><span data-stu-id="51458-126">scikit-learn</span></span>](http://scikit-learn.org/)
- [<span data-ttu-id="51458-127">TensorFlow</span><span class="sxs-lookup"><span data-stu-id="51458-127">TensorFlow</span></span>](https://www.tensorflow.org/)
- [<span data-ttu-id="51458-128">Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="51458-128">Microsoft Cognitive Toolkit</span></span>](https://www.microsoft.com/en-us/cognitive-toolkit/)
- [<span data-ttu-id="51458-129">Spark ML</span><span class="sxs-lookup"><span data-stu-id="51458-129">Spark ML</span></span>](https://spark.apache.org/docs/2.1.1/ml-pipeline.html)

<span data-ttu-id="51458-130">You can execute your experiments in managed environments such as Docker containers and Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="51458-130">You can execute your experiments in managed environments such as Docker containers and Spark clusters.</span></span> <span data-ttu-id="51458-131">You can also use advanced hardware such as [GPU-enabled virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu) to accelerate your execution.</span><span class="sxs-lookup"><span data-stu-id="51458-131">You can also use advanced hardware such as [GPU-enabled virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu) to accelerate your execution.</span></span>

<span data-ttu-id="51458-132">Azure Machine Learning is built on top of the following open source technologies:</span><span class="sxs-lookup"><span data-stu-id="51458-132">Azure Machine Learning is built on top of the following open source technologies:</span></span>

- [<span data-ttu-id="51458-133">Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="51458-133">Jupyter Notebook</span></span>](http://jupyter.org/)
- [<span data-ttu-id="51458-134">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="51458-134">Apache Spark</span></span>](https://spark.apache.org/)
- [<span data-ttu-id="51458-135">Docker</span><span class="sxs-lookup"><span data-stu-id="51458-135">Docker</span></span>](https://www.docker.com/)
- [<span data-ttu-id="51458-136">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="51458-136">Kubernetes</span></span>](https://kubernetes.io/)
- [<span data-ttu-id="51458-137">Python</span><span class="sxs-lookup"><span data-stu-id="51458-137">Python</span></span>](https://www.python.org/)
- [<span data-ttu-id="51458-138">Conda</span><span class="sxs-lookup"><span data-stu-id="51458-138">Conda</span></span>](https://conda.io/docs/)

<span data-ttu-id="51458-139">It also includes Microsoft's own open source technologies, such as [Microsoft Machine Learning Library for Apache Spark](https://github.com/Azure/mmlspark) and Cognitive Toolkit.</span><span class="sxs-lookup"><span data-stu-id="51458-139">It also includes Microsoft's own open source technologies, such as [Microsoft Machine Learning Library for Apache Spark](https://github.com/Azure/mmlspark) and Cognitive Toolkit.</span></span>

<span data-ttu-id="51458-140">In addition, you also benefit from some of the most advanced, tried-and-true machine learning technologies developed by Microsoft designed to solve on large-scale problems.</span><span class="sxs-lookup"><span data-stu-id="51458-140">In addition, you also benefit from some of the most advanced, tried-and-true machine learning technologies developed by Microsoft designed to solve on large-scale problems.</span></span> <span data-ttu-id="51458-141">They are battle-tested in many Microsoft products, such as:</span><span class="sxs-lookup"><span data-stu-id="51458-141">They are battle-tested in many Microsoft products, such as:</span></span>

- <span data-ttu-id="51458-142">Windows</span><span class="sxs-lookup"><span data-stu-id="51458-142">Windows</span></span>
- <span data-ttu-id="51458-143">Bing</span><span class="sxs-lookup"><span data-stu-id="51458-143">Bing</span></span>
- <span data-ttu-id="51458-144">Xbox</span><span class="sxs-lookup"><span data-stu-id="51458-144">Xbox</span></span>
- <span data-ttu-id="51458-145">Office</span><span class="sxs-lookup"><span data-stu-id="51458-145">Office</span></span>
- <span data-ttu-id="51458-146">SQL Server</span><span class="sxs-lookup"><span data-stu-id="51458-146">SQL Server</span></span>

<span data-ttu-id="51458-147">The following are some of the Microsoft machine learning technologies included with Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="51458-147">The following are some of the Microsoft machine learning technologies included with Azure Machine Learning:</span></span>

- <span data-ttu-id="51458-148">[PROSE](https://microsoft.github.io/prose/) (PROgram Synthesis using Examples)</span><span class="sxs-lookup"><span data-stu-id="51458-148">[PROSE](https://microsoft.github.io/prose/) (PROgram Synthesis using Examples)</span></span>
- [<span data-ttu-id="51458-149">microsoftml</span><span class="sxs-lookup"><span data-stu-id="51458-149">microsoftml</span></span>](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)
- [<span data-ttu-id="51458-150">revoscalepy</span><span class="sxs-lookup"><span data-stu-id="51458-150">revoscalepy</span></span>](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

## <a name="azure-machine-learning-workbench"></a><span data-ttu-id="51458-151">Azure Machine Learning Workbench</span><span class="sxs-lookup"><span data-stu-id="51458-151">Azure Machine Learning Workbench</span></span>
<span data-ttu-id="51458-152">Azure Machine Learning Workbench is a desktop application plus command-line tools, supported on both Windows and macOS.</span><span class="sxs-lookup"><span data-stu-id="51458-152">Azure Machine Learning Workbench is a desktop application plus command-line tools, supported on both Windows and macOS.</span></span> <span data-ttu-id="51458-153">It allows you to manage machine learning solutions through the entire data science life cycle:</span><span class="sxs-lookup"><span data-stu-id="51458-153">It allows you to manage machine learning solutions through the entire data science life cycle:</span></span>

- <span data-ttu-id="51458-154">Data ingestion and preparation</span><span class="sxs-lookup"><span data-stu-id="51458-154">Data ingestion and preparation</span></span>
- <span data-ttu-id="51458-155">Model development and experiment management</span><span class="sxs-lookup"><span data-stu-id="51458-155">Model development and experiment management</span></span>
- <span data-ttu-id="51458-156">Model deployment in various target environments</span><span class="sxs-lookup"><span data-stu-id="51458-156">Model deployment in various target environments</span></span>

<span data-ttu-id="51458-157">Here are the core functionalities offered by Azure Machine Learning Workbench:</span><span class="sxs-lookup"><span data-stu-id="51458-157">Here are the core functionalities offered by Azure Machine Learning Workbench:</span></span>

- <span data-ttu-id="51458-158">Data preparation tool that can learn data transformation logic by example.</span><span class="sxs-lookup"><span data-stu-id="51458-158">Data preparation tool that can learn data transformation logic by example.</span></span>
- <span data-ttu-id="51458-159">Data source abstraction accessible through UX and Python code.</span><span class="sxs-lookup"><span data-stu-id="51458-159">Data source abstraction accessible through UX and Python code.</span></span>
- <span data-ttu-id="51458-160">Python SDK for invoking visually constructed data preparation packages.</span><span class="sxs-lookup"><span data-stu-id="51458-160">Python SDK for invoking visually constructed data preparation packages.</span></span>
- <span data-ttu-id="51458-161">Built-in Jupyter Notebook service and client UX.</span><span class="sxs-lookup"><span data-stu-id="51458-161">Built-in Jupyter Notebook service and client UX.</span></span>
- <span data-ttu-id="51458-162">Experiment monitoring and management through run history views.</span><span class="sxs-lookup"><span data-stu-id="51458-162">Experiment monitoring and management through run history views.</span></span>
- <span data-ttu-id="51458-163">Role-based access control that enables sharing and collaboration through Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="51458-163">Role-based access control that enables sharing and collaboration through Azure Active Directory.</span></span>
- <span data-ttu-id="51458-164">Automatic project snapshots for each run, and explicit version control enabled by native Git integration.</span><span class="sxs-lookup"><span data-stu-id="51458-164">Automatic project snapshots for each run, and explicit version control enabled by native Git integration.</span></span> 
- <span data-ttu-id="51458-165">Integration with popular Python IDEs.</span><span class="sxs-lookup"><span data-stu-id="51458-165">Integration with popular Python IDEs.</span></span>

<span data-ttu-id="51458-166">For more information, reference the following articles:</span><span class="sxs-lookup"><span data-stu-id="51458-166">For more information, reference the following articles:</span></span>
- [<span data-ttu-id="51458-167">Data Preparation User Guide</span><span class="sxs-lookup"><span data-stu-id="51458-167">Data Preparation User Guide</span></span>](../desktop-workbench/data-prep-user-guide.md)
- [<span data-ttu-id="51458-168">Using Git with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="51458-168">Using Git with Azure Machine Learning</span></span>](../desktop-workbench/using-git-ml-project.md)
- [<span data-ttu-id="51458-169">Using Jupyter Notebook in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="51458-169">Using Jupyter Notebook in Azure Machine Learning</span></span>](../desktop-workbench/how-to-use-jupyter-notebooks.md)
- [<span data-ttu-id="51458-170">Roaming and Sharing</span><span class="sxs-lookup"><span data-stu-id="51458-170">Roaming and Sharing</span></span>](../desktop-workbench/roaming-and-collaboration.md)
- [<span data-ttu-id="51458-171">Run History Guide</span><span class="sxs-lookup"><span data-stu-id="51458-171">Run History Guide</span></span>](../desktop-workbench/how-to-use-run-history-model-metrics.md)
- [<span data-ttu-id="51458-172">IDE Integration</span><span class="sxs-lookup"><span data-stu-id="51458-172">IDE Integration</span></span>](../desktop-workbench/how-to-configure-your-ide.md)

## <a name="azure-machine-learning-experimentation-service"></a><span data-ttu-id="51458-173">Azure Machine Learning Experimentation Service</span><span class="sxs-lookup"><span data-stu-id="51458-173">Azure Machine Learning Experimentation Service</span></span>
<span data-ttu-id="51458-174">The Experimentation Service handles the execution of machine learning experiments.</span><span class="sxs-lookup"><span data-stu-id="51458-174">The Experimentation Service handles the execution of machine learning experiments.</span></span> <span data-ttu-id="51458-175">It also supports the Workbench by providing project management, Git integration, access control, roaming, and sharing.</span><span class="sxs-lookup"><span data-stu-id="51458-175">It also supports the Workbench by providing project management, Git integration, access control, roaming, and sharing.</span></span> 

<span data-ttu-id="51458-176">Through easy configuration, you can execute your experiments across a range of compute environment options:</span><span class="sxs-lookup"><span data-stu-id="51458-176">Through easy configuration, you can execute your experiments across a range of compute environment options:</span></span>

- <span data-ttu-id="51458-177">Local native</span><span class="sxs-lookup"><span data-stu-id="51458-177">Local native</span></span>
- <span data-ttu-id="51458-178">Local Docker container</span><span class="sxs-lookup"><span data-stu-id="51458-178">Local Docker container</span></span>
- <span data-ttu-id="51458-179">Docker container on a remote VM</span><span class="sxs-lookup"><span data-stu-id="51458-179">Docker container on a remote VM</span></span>
- <span data-ttu-id="51458-180">Scale out Spark cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="51458-180">Scale out Spark cluster in Azure</span></span>

<span data-ttu-id="51458-181">The Experimentation Service constructs virtual environments to ensure that your script can be executed in isolation with reproducible results.</span><span class="sxs-lookup"><span data-stu-id="51458-181">The Experimentation Service constructs virtual environments to ensure that your script can be executed in isolation with reproducible results.</span></span> <span data-ttu-id="51458-182">It records run history information and presents the history to you visually.</span><span class="sxs-lookup"><span data-stu-id="51458-182">It records run history information and presents the history to you visually.</span></span> <span data-ttu-id="51458-183">You can easily select the best model out of your experiment runs.</span><span class="sxs-lookup"><span data-stu-id="51458-183">You can easily select the best model out of your experiment runs.</span></span> 

<span data-ttu-id="51458-184">For more information, please reference [Experimentation Service Configuration](../desktop-workbench/experimentation-service-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="51458-184">For more information, please reference [Experimentation Service Configuration](../desktop-workbench/experimentation-service-configuration.md).</span></span>

## <a name="azure-machine-learning-model-management-service"></a><span data-ttu-id="51458-185">Azure Machine Learning Model Management Service</span><span class="sxs-lookup"><span data-stu-id="51458-185">Azure Machine Learning Model Management Service</span></span>

<span data-ttu-id="51458-186">Model Management Service allows data scientists and dev-ops teams to deploy predictive models into a wide variety of environments.</span><span class="sxs-lookup"><span data-stu-id="51458-186">Model Management Service allows data scientists and dev-ops teams to deploy predictive models into a wide variety of environments.</span></span> <span data-ttu-id="51458-187">Model versions and lineage are tracked from training runs to deployments.</span><span class="sxs-lookup"><span data-stu-id="51458-187">Model versions and lineage are tracked from training runs to deployments.</span></span> <span data-ttu-id="51458-188">Models are stored, registered, and managed in the cloud.</span><span class="sxs-lookup"><span data-stu-id="51458-188">Models are stored, registered, and managed in the cloud.</span></span> 

<span data-ttu-id="51458-189">Using simple CLI commands, you can containerize your model, scoring scripts and dependencies into Docker images.</span><span class="sxs-lookup"><span data-stu-id="51458-189">Using simple CLI commands, you can containerize your model, scoring scripts and dependencies into Docker images.</span></span> <span data-ttu-id="51458-190">These images are registered in your own Docker registry hosted in Azure (Azure Container Registry).</span><span class="sxs-lookup"><span data-stu-id="51458-190">These images are registered in your own Docker registry hosted in Azure (Azure Container Registry).</span></span> <span data-ttu-id="51458-191">They can be reliably deployed to the following targets:</span><span class="sxs-lookup"><span data-stu-id="51458-191">They can be reliably deployed to the following targets:</span></span>

- <span data-ttu-id="51458-192">Local machines</span><span class="sxs-lookup"><span data-stu-id="51458-192">Local machines</span></span>
- <span data-ttu-id="51458-193">On-premises servers</span><span class="sxs-lookup"><span data-stu-id="51458-193">On-premises servers</span></span>
- <span data-ttu-id="51458-194">The cloud</span><span class="sxs-lookup"><span data-stu-id="51458-194">The cloud</span></span>
- <span data-ttu-id="51458-195">IoT edge devices</span><span class="sxs-lookup"><span data-stu-id="51458-195">IoT edge devices</span></span>

<span data-ttu-id="51458-196">Kubernetes running in the Azure Container Service (ACS) is used for cloud scale-out deployment.</span><span class="sxs-lookup"><span data-stu-id="51458-196">Kubernetes running in the Azure Container Service (ACS) is used for cloud scale-out deployment.</span></span> <span data-ttu-id="51458-197">Model execution telemetry is captured in AppInsights for visual analysis.</span><span class="sxs-lookup"><span data-stu-id="51458-197">Model execution telemetry is captured in AppInsights for visual analysis.</span></span> 

<span data-ttu-id="51458-198">For more information on Model Management Service, reference [Model Management Overview](../desktop-workbench/model-management-overview.md)</span><span class="sxs-lookup"><span data-stu-id="51458-198">For more information on Model Management Service, reference [Model Management Overview](../desktop-workbench/model-management-overview.md)</span></span>


## <a name="microsoft-machine-learning-library-for-apache-spark"></a><span data-ttu-id="51458-199">Microsoft Machine Learning Library for Apache Spark</span><span class="sxs-lookup"><span data-stu-id="51458-199">Microsoft Machine Learning Library for Apache Spark</span></span>

<span data-ttu-id="51458-200">The [MMLSpark](https://github.com/Azure/mmlspark)(Microsoft Machine Learning Library for Apache Spark) is an open-source Spark package that provides deep learning and data science tools for Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="51458-200">The [MMLSpark](https://github.com/Azure/mmlspark)(Microsoft Machine Learning Library for Apache Spark) is an open-source Spark package that provides deep learning and data science tools for Apache Spark.</span></span> <span data-ttu-id="51458-201">It integrates [Spark Machine Learning Pipelines](https://spark.apache.org/docs/2.1.1/ml-pipeline.html) with the [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/cognitive-toolkit/) and [OpenCV](http://opencv.org/) library.</span><span class="sxs-lookup"><span data-stu-id="51458-201">It integrates [Spark Machine Learning Pipelines](https://spark.apache.org/docs/2.1.1/ml-pipeline.html) with the [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/cognitive-toolkit/) and [OpenCV](http://opencv.org/) library.</span></span> <span data-ttu-id="51458-202">It enables you to quickly create powerful, highly scalable predictive, and analytical models for large image and text datasets.</span><span class="sxs-lookup"><span data-stu-id="51458-202">It enables you to quickly create powerful, highly scalable predictive, and analytical models for large image and text datasets.</span></span> <span data-ttu-id="51458-203">Some highlights include:</span><span class="sxs-lookup"><span data-stu-id="51458-203">Some highlights include:</span></span>

- <span data-ttu-id="51458-204">Easily ingest images from HDFS into Spark DataFrame</span><span class="sxs-lookup"><span data-stu-id="51458-204">Easily ingest images from HDFS into Spark DataFrame</span></span>
- <span data-ttu-id="51458-205">Pre-process image data using transforms from OpenCV</span><span class="sxs-lookup"><span data-stu-id="51458-205">Pre-process image data using transforms from OpenCV</span></span>
- <span data-ttu-id="51458-206">Featurize images using pre-trained deep neural nets using the Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="51458-206">Featurize images using pre-trained deep neural nets using the Microsoft Cognitive Toolkit</span></span> 
- <span data-ttu-id="51458-207">Use pre-trained bidirectional LSTMs from Keras for medical entity extraction</span><span class="sxs-lookup"><span data-stu-id="51458-207">Use pre-trained bidirectional LSTMs from Keras for medical entity extraction</span></span>
- <span data-ttu-id="51458-208">Train DNN-based image classification models on N-Series GPU VMs on Azure</span><span class="sxs-lookup"><span data-stu-id="51458-208">Train DNN-based image classification models on N-Series GPU VMs on Azure</span></span>
- <span data-ttu-id="51458-209">Featurize free-form text data using convenient APIs on top of primitives in SparkML via a single transformer</span><span class="sxs-lookup"><span data-stu-id="51458-209">Featurize free-form text data using convenient APIs on top of primitives in SparkML via a single transformer</span></span>
- <span data-ttu-id="51458-210">Train classification and regression models easily via implicit featurization of data</span><span class="sxs-lookup"><span data-stu-id="51458-210">Train classification and regression models easily via implicit featurization of data</span></span>
- <span data-ttu-id="51458-211">Compute a rich set of evaluation metrics including per-instance metrics</span><span class="sxs-lookup"><span data-stu-id="51458-211">Compute a rich set of evaluation metrics including per-instance metrics</span></span>

<span data-ttu-id="51458-212">For more information, reference [Using MMLSpark in Azure Machine Learning](../desktop-workbench/how-to-use-mmlspark.md).</span><span class="sxs-lookup"><span data-stu-id="51458-212">For more information, reference [Using MMLSpark in Azure Machine Learning](../desktop-workbench/how-to-use-mmlspark.md).</span></span>

## <a name="visual-studio-code-tools-for-ai"></a><span data-ttu-id="51458-213">Visual Studio Code Tools for AI</span><span class="sxs-lookup"><span data-stu-id="51458-213">Visual Studio Code Tools for AI</span></span>
<span data-ttu-id="51458-214">Visual Studio Code Tools for AI is an extension in Visual Studio Code to build, test, and deploy Deep Learning and AI solutions.</span><span class="sxs-lookup"><span data-stu-id="51458-214">Visual Studio Code Tools for AI is an extension in Visual Studio Code to build, test, and deploy Deep Learning and AI solutions.</span></span> <span data-ttu-id="51458-215">It features many integration points with Azure Machine Learning, including:</span><span class="sxs-lookup"><span data-stu-id="51458-215">It features many integration points with Azure Machine Learning, including:</span></span>
- <span data-ttu-id="51458-216">A run history view displaying the performance of training runs and logged metrics.</span><span class="sxs-lookup"><span data-stu-id="51458-216">A run history view displaying the performance of training runs and logged metrics.</span></span>
- <span data-ttu-id="51458-217">A gallery view allowing users to browse and bootstrap new projects with the Microsoft Cognitive Toolkit, TensorFlow, and many other deep-learning frameworks.</span><span class="sxs-lookup"><span data-stu-id="51458-217">A gallery view allowing users to browse and bootstrap new projects with the Microsoft Cognitive Toolkit, TensorFlow, and many other deep-learning frameworks.</span></span> 
- <span data-ttu-id="51458-218">An explorer view for selecting compute targets for your scripts to execute.</span><span class="sxs-lookup"><span data-stu-id="51458-218">An explorer view for selecting compute targets for your scripts to execute.</span></span>
 

## <a name="what-are-the-machine-learning-options-from-microsoft"></a><span data-ttu-id="51458-219">What are the machine learning options from Microsoft?</span><span class="sxs-lookup"><span data-stu-id="51458-219">What are the machine learning options from Microsoft?</span></span>
<span data-ttu-id="51458-220">Besides Azure Machine Learning, there are a wide variety of options in Azure to build, deploy, and manage machine learning models.</span><span class="sxs-lookup"><span data-stu-id="51458-220">Besides Azure Machine Learning, there are a wide variety of options in Azure to build, deploy, and manage machine learning models.</span></span> [<span data-ttu-id="51458-221">Learn about them here.</span><span class="sxs-lookup"><span data-stu-id="51458-221">Learn about them here.</span></span>](../desktop-workbench/overview-more-machine-learning.md)

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="next-steps"></a><span data-ttu-id="51458-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="51458-222">Next steps</span></span>
* [<span data-ttu-id="51458-223">Install and create Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="51458-223">Install and create Azure Machine Learning</span></span>](quickstart-installation.md)
