---
title: Quickstart article for Visual Studio Tools for Machine Learning on Azure | Microsoft Docs
description: This article describe how to get started using Visual Studio Tools for Machine Learning, from creating an experiment, training a model, and operationalizing a web-service.
services: machine-learning
ms.workload: data-services
author: chris-lauren
ms.author: chris.lauren
ms.service: machine-learning
ms.component: core
ms.custom: mvc, vs-azure
ms.topic: quickstart
ms.date: 11/15/2017
ms.openlocfilehash: 94bca4d7670b1ec6fba5057b8295f7a3caac2968
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865758"
---
# <a name="visual-studio-tools-for-ai"></a>Visual Studio Tools for AI
Visual Studio Tools for AI is a development extension to build, test, and deploy Deep Learning / AI solutions. It features a seamless integration with Azure Machine Learning, notably a run history view, detailing the performance of previous trainings and custom metrics. It offers a samples explorer view, allowing to browse and bootstrap new project with  [Microsoft Cognitive Toolkit (previously known as CNTK)](http://www.microsoft.com/en-us/cognitive-toolkit), [Google TensorFlow](https://www.tensorflow.org), and other deep-learning framework. Finally, it provides an explorer for compute targets, which enables you to submit jobs to train models on remote environments like Azure Virtual Machines or Linux servers with GPU. It also provides a facilitated access to [Azure Batch AI (Preview)](https://docs.microsoft.com/azure/batch-ai/).
 
## <a name="getting-started"></a>Getting started 
To get started, you first need to download and install [Visual Studio](https://www.visualstudio.com/downloads/). Once you have Visual Studio open, do the following steps:
1. Click "Tools" on the menu bar in Visual Studio and select "Extensions and Updates..."
2. Click on "Online" tab and select "Search Visual Studio Marketplace."
3. Search for "Visual Studio for AI." 
3. Click on the **Download** button. 
4. After installation, restart Visual Studio. 

Once Visual Studio is reloaded, the extension is active. [Learn more about finding extensions](hhttps://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions).

> [!NOTE]
> Visual Studio Tools for AI needs Visual Studio 2015 or 2017, professional or enterprise edition. It does not support Apple OSX version. 


## <a name="exploring-project-samples"></a>Exploring project samples
Visual Studio Tools for AI comes with a samples explorer. The samples explorer makes it easy to discover sample and try them with only a few clicks. To open the explorer, do as follows:   
1. In the menu bar, click on **AI Tools**.
2. Click on "Azure Machine Learning Gallery."

A tab with all the Azure ML Samples opens.

## <a name="creating-a-new-project-from-the-sample-explorer"></a>Creating a new project from the sample explorer 
You can browse different samples and get more information about them. Let's browse until finding the "Classifying Iris" sample. To create a new project based on this sample do as follows:
1. Click on **install** button on the project sample, this will open a new dialogue. 
2. Select a resource group, an account, and a workspace.
3. You can leave project type as General.
4. Enter a project path and a project name, then press enter. 
5. A dialogue opens prompting to save a solution, click save. 

Once complete, a new project opens in a new instance of Visual Studio. 

> [!TIP]
> You need to be logged-in to access your Azure resource. From the embedded terminal enter "az login" and follow the instruction. 

## <a name="submitting-experiment-with-the-new-project"></a>Submitting experiment with the new project
The new project being open in Visual Studio, submit a job to a compute target (local or VM with docker).
To submit the job, do as follow: 
1. From the solution explorer, right-click on the file you want to submit, and select **Set as Startup File**.
2. Select the project name, right-click and select **Submit Job...**
3. A new dialogue will open, letting you choose the cluster (or compute target) to execute your script.
4. Click on **Submit**

Once the job is submitted, the embedded-terminal displays the progress of the runs.

## <a name="view-list-of-jobs"></a>View list of jobs
Once the job is submitted, you can list the jobs from the run history.
1. In **Server Explorer**, click on **AI Tools**.
2. Then select **Azure Machine Learning**
3. Click on the **Jobs** menu.

The Job explorer list all the submitted experiment for this project. 

## <a name="view-job-details"></a>View job details
With the Job explorer view open, click on the first run in the list.
This will load the Job Summary panel, and the Logs and Outputs panel.

## <a name="next-steps"></a>Next steps
> [!div class="nextstepaction"]
> [How to configure Azure Machine Learning to work with an IDE](./how-to-configure-your-IDE.md)
