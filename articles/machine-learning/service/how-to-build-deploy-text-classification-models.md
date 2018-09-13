---
title: Build and deploy a text classification model using Azure Machine Learning Package for Text Analytics.
description: Learn how to build, train, test and deploy a text classification model using the Azure Machine Learning Package for Text Analytics.
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.reviewer: jmartens
ms.author: netahw
author: nhaiby
ms.date: 05/07/2018
ms.openlocfilehash: 2b37ec9facebcdcb6b40d6cfe35eb46b5c5801bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866141"
---
# <a name="build-and-deploy-text-classification-models-with-azure-machine-learning"></a><span data-ttu-id="9f1e0-103">Build and deploy text classification models with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9f1e0-103">Build and deploy text classification models with Azure Machine Learning</span></span>

<span data-ttu-id="9f1e0-104">In this article, you can learn how to train and deploy a text classification model with **Azure Machine Learning Package for Text Analytics** (AMLPTA).</span><span class="sxs-lookup"><span data-stu-id="9f1e0-104">In this article, you can learn how to train and deploy a text classification model with **Azure Machine Learning Package for Text Analytics** (AMLPTA).</span></span> <span data-ttu-id="9f1e0-105">The goal of text classification is to assign a piece of text to one or more predefined classes or categories.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-105">The goal of text classification is to assign a piece of text to one or more predefined classes or categories.</span></span> <span data-ttu-id="9f1e0-106">This text could, for example, be a document, news article, search query, email, tweet, support tickets.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-106">This text could, for example, be a document, news article, search query, email, tweet, support tickets.</span></span>

<span data-ttu-id="9f1e0-107">There are broad applications of text classification such as:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-107">There are broad applications of text classification such as:</span></span> 
+ <span data-ttu-id="9f1e0-108">Categorizing newspaper articles and news wire contents into topics</span><span class="sxs-lookup"><span data-stu-id="9f1e0-108">Categorizing newspaper articles and news wire contents into topics</span></span>
+ <span data-ttu-id="9f1e0-109">Organizing web pages into hierarchical categories</span><span class="sxs-lookup"><span data-stu-id="9f1e0-109">Organizing web pages into hierarchical categories</span></span> 
+ <span data-ttu-id="9f1e0-110">Filtering spam email</span><span class="sxs-lookup"><span data-stu-id="9f1e0-110">Filtering spam email</span></span>
+ <span data-ttu-id="9f1e0-111">Sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="9f1e0-111">Sentiment analysis</span></span>
+ <span data-ttu-id="9f1e0-112">Predicting user intent from search queries</span><span class="sxs-lookup"><span data-stu-id="9f1e0-112">Predicting user intent from search queries</span></span>
+ <span data-ttu-id="9f1e0-113">Routing support tickets</span><span class="sxs-lookup"><span data-stu-id="9f1e0-113">Routing support tickets</span></span>
+ <span data-ttu-id="9f1e0-114">Analyzing customer feedback</span><span class="sxs-lookup"><span data-stu-id="9f1e0-114">Analyzing customer feedback</span></span> 

<span data-ttu-id="9f1e0-115">The text classification model building and deployment workflow for a model with AMLPTA is as follows:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-115">The text classification model building and deployment workflow for a model with AMLPTA is as follows:</span></span>

1. <span data-ttu-id="9f1e0-116">Load the data</span><span class="sxs-lookup"><span data-stu-id="9f1e0-116">Load the data</span></span>
2. <span data-ttu-id="9f1e0-117">Train the model</span><span class="sxs-lookup"><span data-stu-id="9f1e0-117">Train the model</span></span>
3. <span data-ttu-id="9f1e0-118">Apply the classifier</span><span class="sxs-lookup"><span data-stu-id="9f1e0-118">Apply the classifier</span></span> 
4. <span data-ttu-id="9f1e0-119">Evaluate model performance</span><span class="sxs-lookup"><span data-stu-id="9f1e0-119">Evaluate model performance</span></span>
5. <span data-ttu-id="9f1e0-120">Save the pipeline</span><span class="sxs-lookup"><span data-stu-id="9f1e0-120">Save the pipeline</span></span>
6. <span data-ttu-id="9f1e0-121">Test the pipeline</span><span class="sxs-lookup"><span data-stu-id="9f1e0-121">Test the pipeline</span></span>
8. <span data-ttu-id="9f1e0-122">Deploy the model as a web service</span><span class="sxs-lookup"><span data-stu-id="9f1e0-122">Deploy the model as a web service</span></span>

<span data-ttu-id="9f1e0-123">Consult the [package reference documentation](https://aka.ms/aml-packages/text) for the detailed reference for each module and class.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-123">Consult the [package reference documentation](https://aka.ms/aml-packages/text) for the detailed reference for each module and class.</span></span>

<span data-ttu-id="9f1e0-124">The sample code in this article uses a scikit-learn pipeline.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-124">The sample code in this article uses a scikit-learn pipeline.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f1e0-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9f1e0-125">Prerequisites</span></span> 

1. <span data-ttu-id="9f1e0-126">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-126">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

1. <span data-ttu-id="9f1e0-127">The following accounts and application must be set up and installed:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-127">The following accounts and application must be set up and installed:</span></span>
   - <span data-ttu-id="9f1e0-128">Azure Machine Learning Experimentation account</span><span class="sxs-lookup"><span data-stu-id="9f1e0-128">Azure Machine Learning Experimentation account</span></span> 
   - <span data-ttu-id="9f1e0-129">An Azure Machine Learning Model Management account</span><span class="sxs-lookup"><span data-stu-id="9f1e0-129">An Azure Machine Learning Model Management account</span></span>
   - <span data-ttu-id="9f1e0-130">Azure Machine Learning Workbench installed</span><span class="sxs-lookup"><span data-stu-id="9f1e0-130">Azure Machine Learning Workbench installed</span></span>

   <span data-ttu-id="9f1e0-131">If these three are not yet created or installed, follow the [Azure Machine Learning Quickstart and Workbench installation](../service/quickstart-installation.md) article.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-131">If these three are not yet created or installed, follow the [Azure Machine Learning Quickstart and Workbench installation](../service/quickstart-installation.md) article.</span></span> 

1. <span data-ttu-id="9f1e0-132">The Azure Machine Learning Package for Text Analytics must be installed.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-132">The Azure Machine Learning Package for Text Analytics must be installed.</span></span> <span data-ttu-id="9f1e0-133">Learn how to [install this package here](https://aka.ms/aml-packages/text).</span><span class="sxs-lookup"><span data-stu-id="9f1e0-133">Learn how to [install this package here](https://aka.ms/aml-packages/text).</span></span>


## <a name="sample-data-and-jupyter-notebook"></a><span data-ttu-id="9f1e0-134">Sample data and Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="9f1e0-134">Sample data and Jupyter notebook</span></span>

### <a name="get-the-jupyter-notebook"></a><span data-ttu-id="9f1e0-135">Get the Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="9f1e0-135">Get the Jupyter notebook</span></span>

<span data-ttu-id="9f1e0-136">Try it out yourself.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-136">Try it out yourself.</span></span> <span data-ttu-id="9f1e0-137">Download the notebook and run it yourself.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-137">Download the notebook and run it yourself.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9f1e0-138">Get the Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="9f1e0-138">Get the Jupyter notebook</span></span>](https://aka.ms/aml-packages/text/notebooks/text_classification_sentiment_data)

### <a name="download-and-explore-the-sample-data"></a><span data-ttu-id="9f1e0-139">Download and Explore the sample data</span><span class="sxs-lookup"><span data-stu-id="9f1e0-139">Download and Explore the sample data</span></span>
<span data-ttu-id="9f1e0-140">The following example uses the [20 newsgroups dataset](http://qwone.com/~jason/20Newsgroups/)  that is available through the scikit-learn library to demonstrate how to create a text classifier with Azure Machine Learning Package for Text Analytics.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-140">The following example uses the [20 newsgroups dataset](http://qwone.com/~jason/20Newsgroups/)  that is available through the scikit-learn library to demonstrate how to create a text classifier with Azure Machine Learning Package for Text Analytics.</span></span> 

<span data-ttu-id="9f1e0-141">The 20 newsgroups dataset has around 18,000 newsgroups posts on 20 different topics divided into two subsets: one for training and the other one for performance evaluation.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-141">The 20 newsgroups dataset has around 18,000 newsgroups posts on 20 different topics divided into two subsets: one for training and the other one for performance evaluation.</span></span> <span data-ttu-id="9f1e0-142">The split into train and test is based upon each message post date whether before or after a specific date.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-142">The split into train and test is based upon each message post date whether before or after a specific date.</span></span>

```python
# Import Packages 
# Use Azure Machine Learning history magic to control history collection
# History is off by default, options are "on", "off", or "show"
#%azureml history on
%matplotlib inline
# Use the Azure Machine Learning data collector to log various metrics
from azureml.logging import get_azureml_logger
import os

logger = get_azureml_logger()

# Log cell runs into run history
logger.log('Cell','Set up run')
# from tatk.utils import load_newsgroups_data, data_dir, dictionaries_dir, models_dir
import pip
pip.main(["show", "azureml-tatk"])
```

### <a name="set-the-location-of-the-data"></a><span data-ttu-id="9f1e0-143">Set the location of the data</span><span class="sxs-lookup"><span data-stu-id="9f1e0-143">Set the location of the data</span></span>
<span data-ttu-id="9f1e0-144">Set the location where you have downloaded the data in the data dir parameter.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-144">Set the location where you have downloaded the data in the data dir parameter.</span></span> <span data-ttu-id="9f1e0-145">You can also use your own data, the input dataset must be a \*.tsv file format.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-145">You can also use your own data, the input dataset must be a \*.tsv file format.</span></span>

```python
import os
import pandas as pd

#set the working directory where to save the training data files
resources_dir = os.path.join(os.path.expanduser("~"), "tatk", "resources")
data_dir = os.path.join(os.path.expanduser("~"), "tatk", "data")

from sklearn.datasets import fetch_20newsgroups
twenty_train = fetch_20newsgroups(data_home=data_dir, subset='train')
X_train, y_train = twenty_train.data, twenty_train.target
df_train = pd.DataFrame({"text":X_train, "label":y_train})

twenty_test = fetch_20newsgroups(data_home=data_dir, subset='test')
X_test, y_test = twenty_test.data, twenty_test.target   
df_test = pd.DataFrame({"text":X_test, "label":y_test})
    
# Training Dataset Location
#training_file_path = <specify-your-own-training-data-file-path-here>
# df_train = pd.read_csv(training_file_path,
#                        sep = '\t',                        
#                        header = 0, names= <specify-your-column-name-list-here>)
df_train.head()
print("df_train.shape= {}".format(df_train.shape))

# Test Dataset Location
#test_file_path = <specify-your-own-test-data-file-path-here>
# df_test = pd.read_csv(test_file_path,
#                       sep = '\t',                        
#                       header = 0, names= <specify-your-column-name-list-here>)

print("df_test.shape= {}".format(df_test.shape))
df_test.head()
```
    df_train.shape= (11314, 2)
    df_test.shape= (7532, 2)
 
 <span data-ttu-id="9f1e0-146">The data consists of label and text</span><span class="sxs-lookup"><span data-stu-id="9f1e0-146">The data consists of label and text</span></span>
    
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th><span data-ttu-id="9f1e0-147">label</span><span class="sxs-lookup"><span data-stu-id="9f1e0-147">label</span></span></th>
      <th><span data-ttu-id="9f1e0-148">text</span><span class="sxs-lookup"><span data-stu-id="9f1e0-148">text</span></span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><span data-ttu-id="9f1e0-149">0</span><span class="sxs-lookup"><span data-stu-id="9f1e0-149">0</span></span></th>
      <td><span data-ttu-id="9f1e0-150">7</span><span class="sxs-lookup"><span data-stu-id="9f1e0-150">7</span></span></td>
      <td><span data-ttu-id="9f1e0-151">From: v064mb9k@ubvmsd.cc.buffalo.edu (NEIL B. ...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-151">From: v064mb9k@ubvmsd.cc.buffalo.edu (NEIL B. ...</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-152">1</span><span class="sxs-lookup"><span data-stu-id="9f1e0-152">1</span></span></th>
      <td><span data-ttu-id="9f1e0-153">5</span><span class="sxs-lookup"><span data-stu-id="9f1e0-153">5</span></span></td>
      <td><span data-ttu-id="9f1e0-154">From: Rick Miller &lt;rick@ee.uwm.edu&gt;\nSubject: ...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-154">From: Rick Miller &lt;rick@ee.uwm.edu&gt;\nSubject: ...</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-155">2</span><span class="sxs-lookup"><span data-stu-id="9f1e0-155">2</span></span></th>
      <td><span data-ttu-id="9f1e0-156">0</span><span class="sxs-lookup"><span data-stu-id="9f1e0-156">0</span></span></td>
      <td><span data-ttu-id="9f1e0-157">From: mathew &lt;mathew@mantis.co.uk&gt;\nSubject: R...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-157">From: mathew &lt;mathew@mantis.co.uk&gt;\nSubject: R...</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-158">3</span><span class="sxs-lookup"><span data-stu-id="9f1e0-158">3</span></span></th>
      <td><span data-ttu-id="9f1e0-159">17</span><span class="sxs-lookup"><span data-stu-id="9f1e0-159">17</span></span></td>
      <td><span data-ttu-id="9f1e0-160">From: bakken@cs.arizona.edu (Dave Bakken)\nSub...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-160">From: bakken@cs.arizona.edu (Dave Bakken)\nSub...</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-161">4</span><span class="sxs-lookup"><span data-stu-id="9f1e0-161">4</span></span></th>
      <td><span data-ttu-id="9f1e0-162">19</span><span class="sxs-lookup"><span data-stu-id="9f1e0-162">19</span></span></td>
      <td><span data-ttu-id="9f1e0-163">From: livesey@solntze.wpd.sgi.com (Jon Livesey...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-163">From: livesey@solntze.wpd.sgi.com (Jon Livesey...</span></span></td>
    </tr>
  </tbody>
</table>
</div>

<span data-ttu-id="9f1e0-164">Get the correspondance between categories and their name.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-164">Get the correspondance between categories and their name.</span></span>

```python
int_to_categories = pd.DataFrame({'category':range(20), 'category_name': list(twenty_train.target_names)})
int_to_categories 
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th><span data-ttu-id="9f1e0-165">category</span><span class="sxs-lookup"><span data-stu-id="9f1e0-165">category</span></span></th>
      <th><span data-ttu-id="9f1e0-166">category_name</span><span class="sxs-lookup"><span data-stu-id="9f1e0-166">category_name</span></span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><span data-ttu-id="9f1e0-167">0</span><span class="sxs-lookup"><span data-stu-id="9f1e0-167">0</span></span></th>
      <td><span data-ttu-id="9f1e0-168">0</span><span class="sxs-lookup"><span data-stu-id="9f1e0-168">0</span></span></td>
      <td><span data-ttu-id="9f1e0-169">alt.atheism</span><span class="sxs-lookup"><span data-stu-id="9f1e0-169">alt.atheism</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-170">1</span><span class="sxs-lookup"><span data-stu-id="9f1e0-170">1</span></span></th>
      <td><span data-ttu-id="9f1e0-171">1</span><span class="sxs-lookup"><span data-stu-id="9f1e0-171">1</span></span></td>
      <td><span data-ttu-id="9f1e0-172">comp.graphics</span><span class="sxs-lookup"><span data-stu-id="9f1e0-172">comp.graphics</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-173">2</span><span class="sxs-lookup"><span data-stu-id="9f1e0-173">2</span></span></th>
      <td><span data-ttu-id="9f1e0-174">2</span><span class="sxs-lookup"><span data-stu-id="9f1e0-174">2</span></span></td>
      <td><span data-ttu-id="9f1e0-175">comp.os.ms-windows.misc</span><span class="sxs-lookup"><span data-stu-id="9f1e0-175">comp.os.ms-windows.misc</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-176">3</span><span class="sxs-lookup"><span data-stu-id="9f1e0-176">3</span></span></th>
      <td><span data-ttu-id="9f1e0-177">3</span><span class="sxs-lookup"><span data-stu-id="9f1e0-177">3</span></span></td>
      <td><span data-ttu-id="9f1e0-178">comp.sys.ibm.pc.hardware</span><span class="sxs-lookup"><span data-stu-id="9f1e0-178">comp.sys.ibm.pc.hardware</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-179">4</span><span class="sxs-lookup"><span data-stu-id="9f1e0-179">4</span></span></th>
      <td><span data-ttu-id="9f1e0-180">4</span><span class="sxs-lookup"><span data-stu-id="9f1e0-180">4</span></span></td>
      <td><span data-ttu-id="9f1e0-181">comp.sys.mac.hardware</span><span class="sxs-lookup"><span data-stu-id="9f1e0-181">comp.sys.mac.hardware</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-182">5</span><span class="sxs-lookup"><span data-stu-id="9f1e0-182">5</span></span></th>
      <td><span data-ttu-id="9f1e0-183">5</span><span class="sxs-lookup"><span data-stu-id="9f1e0-183">5</span></span></td>
      <td><span data-ttu-id="9f1e0-184">comp.windows.x</span><span class="sxs-lookup"><span data-stu-id="9f1e0-184">comp.windows.x</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-185">6</span><span class="sxs-lookup"><span data-stu-id="9f1e0-185">6</span></span></th>
      <td><span data-ttu-id="9f1e0-186">6</span><span class="sxs-lookup"><span data-stu-id="9f1e0-186">6</span></span></td>
      <td><span data-ttu-id="9f1e0-187">misc.forsale</span><span class="sxs-lookup"><span data-stu-id="9f1e0-187">misc.forsale</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-188">7</span><span class="sxs-lookup"><span data-stu-id="9f1e0-188">7</span></span></th>
      <td><span data-ttu-id="9f1e0-189">7</span><span class="sxs-lookup"><span data-stu-id="9f1e0-189">7</span></span></td>
      <td><span data-ttu-id="9f1e0-190">rec.autos</span><span class="sxs-lookup"><span data-stu-id="9f1e0-190">rec.autos</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-191">8</span><span class="sxs-lookup"><span data-stu-id="9f1e0-191">8</span></span></th>
      <td><span data-ttu-id="9f1e0-192">8</span><span class="sxs-lookup"><span data-stu-id="9f1e0-192">8</span></span></td>
      <td><span data-ttu-id="9f1e0-193">rec.motorcycles</span><span class="sxs-lookup"><span data-stu-id="9f1e0-193">rec.motorcycles</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-194">9</span><span class="sxs-lookup"><span data-stu-id="9f1e0-194">9</span></span></th>
      <td><span data-ttu-id="9f1e0-195">9</span><span class="sxs-lookup"><span data-stu-id="9f1e0-195">9</span></span></td>
      <td><span data-ttu-id="9f1e0-196">rec.sport.baseball</span><span class="sxs-lookup"><span data-stu-id="9f1e0-196">rec.sport.baseball</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-197">10</span><span class="sxs-lookup"><span data-stu-id="9f1e0-197">10</span></span></th>
      <td><span data-ttu-id="9f1e0-198">10</span><span class="sxs-lookup"><span data-stu-id="9f1e0-198">10</span></span></td>
      <td><span data-ttu-id="9f1e0-199">rec.sport.hockey</span><span class="sxs-lookup"><span data-stu-id="9f1e0-199">rec.sport.hockey</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-200">11</span><span class="sxs-lookup"><span data-stu-id="9f1e0-200">11</span></span></th>
      <td><span data-ttu-id="9f1e0-201">11</span><span class="sxs-lookup"><span data-stu-id="9f1e0-201">11</span></span></td>
      <td><span data-ttu-id="9f1e0-202">sci.crypt</span><span class="sxs-lookup"><span data-stu-id="9f1e0-202">sci.crypt</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-203">12</span><span class="sxs-lookup"><span data-stu-id="9f1e0-203">12</span></span></th>
      <td><span data-ttu-id="9f1e0-204">12</span><span class="sxs-lookup"><span data-stu-id="9f1e0-204">12</span></span></td>
      <td><span data-ttu-id="9f1e0-205">sci.electronics</span><span class="sxs-lookup"><span data-stu-id="9f1e0-205">sci.electronics</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-206">13</span><span class="sxs-lookup"><span data-stu-id="9f1e0-206">13</span></span></th>
      <td><span data-ttu-id="9f1e0-207">13</span><span class="sxs-lookup"><span data-stu-id="9f1e0-207">13</span></span></td>
      <td><span data-ttu-id="9f1e0-208">sci.med</span><span class="sxs-lookup"><span data-stu-id="9f1e0-208">sci.med</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-209">14</span><span class="sxs-lookup"><span data-stu-id="9f1e0-209">14</span></span></th>
      <td><span data-ttu-id="9f1e0-210">14</span><span class="sxs-lookup"><span data-stu-id="9f1e0-210">14</span></span></td>
      <td><span data-ttu-id="9f1e0-211">sci.space</span><span class="sxs-lookup"><span data-stu-id="9f1e0-211">sci.space</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-212">15</span><span class="sxs-lookup"><span data-stu-id="9f1e0-212">15</span></span></th>
      <td><span data-ttu-id="9f1e0-213">15</span><span class="sxs-lookup"><span data-stu-id="9f1e0-213">15</span></span></td>
      <td><span data-ttu-id="9f1e0-214">soc.religion.christian</span><span class="sxs-lookup"><span data-stu-id="9f1e0-214">soc.religion.christian</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-215">16</span><span class="sxs-lookup"><span data-stu-id="9f1e0-215">16</span></span></th>
      <td><span data-ttu-id="9f1e0-216">16</span><span class="sxs-lookup"><span data-stu-id="9f1e0-216">16</span></span></td>
      <td><span data-ttu-id="9f1e0-217">talk.politics.guns</span><span class="sxs-lookup"><span data-stu-id="9f1e0-217">talk.politics.guns</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-218">17</span><span class="sxs-lookup"><span data-stu-id="9f1e0-218">17</span></span></th>
      <td><span data-ttu-id="9f1e0-219">17</span><span class="sxs-lookup"><span data-stu-id="9f1e0-219">17</span></span></td>
      <td><span data-ttu-id="9f1e0-220">talk.politics.mideast</span><span class="sxs-lookup"><span data-stu-id="9f1e0-220">talk.politics.mideast</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-221">18</span><span class="sxs-lookup"><span data-stu-id="9f1e0-221">18</span></span></th>
      <td><span data-ttu-id="9f1e0-222">18</span><span class="sxs-lookup"><span data-stu-id="9f1e0-222">18</span></span></td>
      <td><span data-ttu-id="9f1e0-223">talk.politics.misc</span><span class="sxs-lookup"><span data-stu-id="9f1e0-223">talk.politics.misc</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-224">19</span><span class="sxs-lookup"><span data-stu-id="9f1e0-224">19</span></span></th>
      <td><span data-ttu-id="9f1e0-225">19</span><span class="sxs-lookup"><span data-stu-id="9f1e0-225">19</span></span></td>
      <td><span data-ttu-id="9f1e0-226">talk.religion.misc</span><span class="sxs-lookup"><span data-stu-id="9f1e0-226">talk.religion.misc</span></span></td>
    </tr>
  </tbody>
</table>
</div>

<span data-ttu-id="9f1e0-227">Now, you can create a preliminary exploration plot histogram of the class frequency in training and test data sets.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-227">Now, you can create a preliminary exploration plot histogram of the class frequency in training and test data sets.</span></span> 

```python
import numpy as np
import math
from matplotlib import pyplot as plt

data = df_train["label"].values
labels = set(data)
print(labels)
bins = range(len(labels)+1) 

#plt.xlim([min(data)-5, max(data)+5])

plt.hist(data, bins=bins, alpha=0.8)
plt.title('training data distribution over the class labels)')
plt.xlabel('class label')
plt.ylabel('frequency')
plt.grid(True)
plt.show()

data = df_test["label"].values
labels = set(data)
print(labels)
bins = range(len(labels)+1) 

#plt.xlim([min(data)-5, max(data)+5])

plt.hist(data, bins=bins, alpha=0.8)
plt.title('test data distribution over the class labels)')
plt.xlabel('class label')
plt.ylabel('frequency')
plt.grid(True)
plt.show()
```

<span data-ttu-id="9f1e0-228">When running the Jupypter notebook, plots are displayed after the preceding code block is run.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-228">When running the Jupypter notebook, plots are displayed after the preceding code block is run.</span></span>


## <a name="train-the-model"></a><span data-ttu-id="9f1e0-229">Train the model</span><span class="sxs-lookup"><span data-stu-id="9f1e0-229">Train the model</span></span>

### <a name="specify-scikit-learn-algorithm-and-define-the-text-classifier"></a><span data-ttu-id="9f1e0-230">Specify scikit-learn algorithm and define the text classifier</span><span class="sxs-lookup"><span data-stu-id="9f1e0-230">Specify scikit-learn algorithm and define the text classifier</span></span>

<span data-ttu-id="9f1e0-231">This step involves training a scikit-learn text classification model using One-versus-Rest Logistic Regression learning algorithm.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-231">This step involves training a scikit-learn text classification model using One-versus-Rest Logistic Regression learning algorithm.</span></span>

<span data-ttu-id="9f1e0-232">For the full list of learnings, refer to the [Scikit Learners](http://scikit-learn.org/stable/supervised_learning) documentation.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-232">For the full list of learnings, refer to the [Scikit Learners](http://scikit-learn.org/stable/supervised_learning) documentation.</span></span>

```python
from sklearn.linear_model import LogisticRegression
import tatk
from tatk.pipelines.text_classification.text_classifier import TextClassifier

log_reg_learner =  LogisticRegression(penalty='l2', dual=False, tol=0.0001, 
                            C=1.0, fit_intercept=True, intercept_scaling=1, 
                            class_weight=None, random_state=None, 
                            solver='lbfgs', max_iter=100, multi_class='ovr',
                            verbose=1, warm_start=False, n_jobs=3) 

#train the model a text column "tweets"
text_classifier = TextClassifier(estimator=log_reg_learner, 
                                text_cols = ["text"], 
                                label_cols = ["label"], 
#                                 numeric_cols = None,
#                                 cat_cols = None, 
                                extract_word_ngrams=True, extract_char_ngrams=True)

```

    TextClassifier::create_pipeline ==> start
    :: number of jobs for the pipeline : 12
    0   text_nltk_preprocessor
    1   text_word_ngrams
    2   text_char_ngrams
    3   assembler
    4   learner
    TextClassifier::create_pipeline ==> end
    
### <a name="fit-the-model"></a><span data-ttu-id="9f1e0-233">Fit the model</span><span class="sxs-lookup"><span data-stu-id="9f1e0-233">Fit the model</span></span>

<span data-ttu-id="9f1e0-234">Use the default parameters of the package.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-234">Use the default parameters of the package.</span></span> <span data-ttu-id="9f1e0-235">By default, the text classifier extracts:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-235">By default, the text classifier extracts:</span></span>
+ <span data-ttu-id="9f1e0-236">Word unigrams and bigrams</span><span class="sxs-lookup"><span data-stu-id="9f1e0-236">Word unigrams and bigrams</span></span>
+ <span data-ttu-id="9f1e0-237">Character 4 grams</span><span class="sxs-lookup"><span data-stu-id="9f1e0-237">Character 4 grams</span></span>

```python
text_classifier.fit(df_train)        
```
   
    TextClassifier::fit ==> start
    schema: col=label:I4:0 col=text:TX:1 header+
    NltkPreprocessor::tatk_fit_transform ==> start
    NltkPreprocessor::tatk_fit_transform ==> end     Time taken: 0.08 mins
    NGramsVectorizer::tatk_fit_transform ==> startNGramsVectorizer::tatk_fit_transform ==> start
    
                vocabulary size=216393
    NGramsVectorizer::tatk_fit_transform ==> end     Time taken: 0.41 mins
                vocabulary size=67230
    NGramsVectorizer::tatk_fit_transform ==> end     Time taken: 0.49 mins
    VectorAssembler::transform ==> start, num of input records=11314
    (11314, 216393)
    (11314, 67230)
    all_features::
    (11314, 283623)
    Time taken: 0.06 mins
    VectorAssembler::transform ==> end
    LogisticRegression::tatk_fit ==> start
    
    [Parallel(n_jobs=3)]: Done  20 out of  20 | elapsed:  2.4min finished
    
    LogisticRegression::tatk_fit ==> end     Time taken: 2.4 mins
    Time taken: 3.04 mins
    TextClassifier::fit ==> end

    TextClassifier(add_index_col=False, callable_proprocessors_list=None,
            cat_cols=None, char_hashing_original=False, col_prefix='tmp_00_',
            decompose_n_grams=False, detect_phrases=False,
            dictionary_categories=None, dictionary_file_path=None,
            embedding_file_path=None, embedding_file_path_fastText=None,
            estimator=None, estimator_vectorizers_list=None,
            extract_char_ngrams=True, extract_word_ngrams=True,
            label_cols=['label'], numeric_cols=None,
            pos_tagger_vectorizer=False,
            preprocessor_dictionary_file_path=None, regex_replcaement='',
            replace_regex_pattern=None, scale_numeric_cols=False,
            text_callable_list=None, text_cols=['text'], text_regex_list=None,
            weight_col=None)


<span data-ttu-id="9f1e0-238">During training, you must have both text and label columns.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-238">During training, you must have both text and label columns.</span></span> <span data-ttu-id="9f1e0-239">While, only the text column is needed for predictions.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-239">While, only the text column is needed for predictions.</span></span> 

### <a name="examine-and-set-the-parameters-of-the-different-pipeline-steps"></a><span data-ttu-id="9f1e0-240">Examine and set the parameters of the different pipeline steps</span><span class="sxs-lookup"><span data-stu-id="9f1e0-240">Examine and set the parameters of the different pipeline steps</span></span>
    
<span data-ttu-id="9f1e0-241">Typically, you set the parameters before you fit a model.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-241">Typically, you set the parameters before you fit a model.</span></span> 

<span data-ttu-id="9f1e0-242">***Example shown with text_word_ngrams***</span><span class="sxs-lookup"><span data-stu-id="9f1e0-242">***Example shown with text_word_ngrams***</span></span> 

<span data-ttu-id="9f1e0-243">The following code samples show you how to train the model using the default pipeline and model parameters.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-243">The following code samples show you how to train the model using the default pipeline and model parameters.</span></span> 

<span data-ttu-id="9f1e0-244">To see what parameters are included for "text_word_ngrams", use [get_step_param_names_by_name](https://docs.microsoft.com/python/api/tatk.core.base_text_model.basetextmodel).</span><span class="sxs-lookup"><span data-stu-id="9f1e0-244">To see what parameters are included for "text_word_ngrams", use [get_step_param_names_by_name](https://docs.microsoft.com/python/api/tatk.core.base_text_model.basetextmodel).</span></span> <span data-ttu-id="9f1e0-245">This function returns the parameters such as lowercase, input_col, output_col and so on.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-245">This function returns the parameters such as lowercase, input_col, output_col and so on.</span></span> 

```python
text_classifier.get_step_param_names_by_name("text_word_ngrams")
```

    ['min_df',
     'strip_accents',
     'max_df',
     'decode_error',
     'max_features',
     'binary',
     'input',
     'vocabulary',
     'analyzer',
     'token_pattern',
     'encoding',
     'use_idf',
     'save_overwrite',
     'output_col',
     'stop_words',
     'sublinear_tf',
     'input_col',
     'lowercase',
     'ngram_range',
     'preprocessor',
     'tokenizer',
     'hashing',
     'dtype',
     'norm',
     'smooth_idf',
     'n_hashing_features']

<span data-ttu-id="9f1e0-246">Next, check the parameter values for "text_char_ngrams":</span><span class="sxs-lookup"><span data-stu-id="9f1e0-246">Next, check the parameter values for "text_char_ngrams":</span></span>

```python
text_classifier.get_step_params_by_name("text_char_ngrams")        
```
    {'analyzer': 'char_wb',
     'binary': False,
     'decode_error': 'strict',
     'dtype': numpy.float32,
     'encoding': 'utf-8',
     'hashing': False,
     'input': 'content',
     'input_col': 'NltkPreprocessor5283a730506549cc880f074e750607b0',
     'lowercase': True,
     'max_df': 1.0,
     'max_features': None,
     'min_df': 3,
     'n_hashing_features': None,
     'ngram_range': (4, 4),
     'norm': 'l2',
     'output_col': 'NGramsVectorizer8eb11031f6b64eaaad9ff0fd3b0f5b80',
     'preprocessor': None,
     'save_overwrite': True,
     'smooth_idf': True,
     'stop_words': None,
     'strip_accents': None,
     'sublinear_tf': False,
     'token_pattern': '(?u)\\b\\w\\w+\\b',
     'tokenizer': None,
     'use_idf': True,
     'vocabulary': None}

<span data-ttu-id="9f1e0-247">If necessary, you can change the default parameters.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-247">If necessary, you can change the default parameters.</span></span>  <span data-ttu-id="9f1e0-248">With the following code, you can change the range of extracted character n-grams from (4,4) to (3,4) to extract both character tri-grams and 4 grams:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-248">With the following code, you can change the range of extracted character n-grams from (4,4) to (3,4) to extract both character tri-grams and 4 grams:</span></span>

```python
text_classifier.set_step_params_by_name("text_char_ngrams", ngram_range =(3,4)) 
text_classifier.get_step_params_by_name("text_char_ngrams")
```
    {'analyzer': 'char_wb',
     'binary': False,
     'decode_error': 'strict',
     'dtype': numpy.float32,
     'encoding': 'utf-8',
     'hashing': False,
     'input': 'content',
     'input_col': 'NltkPreprocessor5283a730506549cc880f074e750607b0',
     'lowercase': True,
     'max_df': 1.0,
     'max_features': None,
     'min_df': 3,
     'n_hashing_features': None,
     'ngram_range': (3, 4),
     'norm': 'l2',
     'output_col': 'NGramsVectorizer8eb11031f6b64eaaad9ff0fd3b0f5b80',
     'preprocessor': None,
     'save_overwrite': True,
     'smooth_idf': True,
     'stop_words': None,
     'strip_accents': None,
     'sublinear_tf': False,
     'token_pattern': '(?u)\\b\\w\\w+\\b',
     'tokenizer': None,
     'use_idf': True,
     'vocabulary': None}

### <a name="export-the-parameters-to-a-file"></a><span data-ttu-id="9f1e0-249">Export the parameters to a file</span><span class="sxs-lookup"><span data-stu-id="9f1e0-249">Export the parameters to a file</span></span>
<span data-ttu-id="9f1e0-250">If needed, you can optimize model performance by rerunning the model fitting step with revised parameters:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-250">If needed, you can optimize model performance by rerunning the model fitting step with revised parameters:</span></span>

```python
import os
params_file_path = os.path.join(data_dir, "params.tsv")
text_classifier.export_params(params_file_path)
```

## <a name="apply-the-classifier"></a><span data-ttu-id="9f1e0-251">Apply the classifier</span><span class="sxs-lookup"><span data-stu-id="9f1e0-251">Apply the classifier</span></span>

<span data-ttu-id="9f1e0-252">Apply the trained text classifier on the test dataset to generate class predictions:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-252">Apply the trained text classifier on the test dataset to generate class predictions:</span></span>

```python
 df_test = text_classifier.predict(df_test)
```

    TextClassifier ::predict ==> start
    NltkPreprocessor::tatk_transform ==> start
    NltkPreprocessor::tatk_transform ==> end     Time taken: 0.05 mins
    NGramsVectorizer::tatk_transform ==> startNGramsVectorizer::tatk_transform ==> start
    
    NGramsVectorizer::tatk_transform ==> end     Time taken: 0.15 mins
    NGramsVectorizer::tatk_transform ==> end     Time taken: 0.37 mins
    VectorAssembler::transform ==> start, num of input records=7532
    (7532, 216393)
    (7532, 67230)
    all_features::
    (7532, 283623)
    Time taken: 0.03 mins
    VectorAssembler::transform ==> end
    LogisticRegression::tatk_predict_proba ==> start
    LogisticRegression::tatk_predict_proba ==> end   Time taken: 0.01 mins
    LogisticRegression::tatk_predict ==> start
    LogisticRegression::tatk_predict ==> end     Time taken: 0.01 mins
    Time taken: 0.46 mins
    TextClassifier ::predict ==> end
    Order of Labels in predicted probabilities saved to attribute label_order of the class object
    
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th><span data-ttu-id="9f1e0-253">label</span><span class="sxs-lookup"><span data-stu-id="9f1e0-253">label</span></span></th>
      <th><span data-ttu-id="9f1e0-254">text</span><span class="sxs-lookup"><span data-stu-id="9f1e0-254">text</span></span></th>
      <th><span data-ttu-id="9f1e0-255">probabilities</span><span class="sxs-lookup"><span data-stu-id="9f1e0-255">probabilities</span></span></th>
      <th><span data-ttu-id="9f1e0-256">prediction</span><span class="sxs-lookup"><span data-stu-id="9f1e0-256">prediction</span></span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><span data-ttu-id="9f1e0-257">0</span><span class="sxs-lookup"><span data-stu-id="9f1e0-257">0</span></span></th>
      <td><span data-ttu-id="9f1e0-258">7</span><span class="sxs-lookup"><span data-stu-id="9f1e0-258">7</span></span></td>
      <td><span data-ttu-id="9f1e0-259">From: v064mb9k@ubvmsd.cc.buffalo.edu (NEIL B. ...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-259">From: v064mb9k@ubvmsd.cc.buffalo.edu (NEIL B. ...</span></span></td>
      <td><span data-ttu-id="9f1e0-260">[0.0165036341329, 0.0548664746458, 0.020549685...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-260">[0.0165036341329, 0.0548664746458, 0.020549685...</span></span></td>
      <td><span data-ttu-id="9f1e0-261">12</span><span class="sxs-lookup"><span data-stu-id="9f1e0-261">12</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-262">1</span><span class="sxs-lookup"><span data-stu-id="9f1e0-262">1</span></span></th>
      <td><span data-ttu-id="9f1e0-263">5</span><span class="sxs-lookup"><span data-stu-id="9f1e0-263">5</span></span></td>
      <td><span data-ttu-id="9f1e0-264">From: Rick Miller &lt;rick@ee.uwm.edu&gt;\nSubject: ...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-264">From: Rick Miller &lt;rick@ee.uwm.edu&gt;\nSubject: ...</span></span></td>
      <td><span data-ttu-id="9f1e0-265">[0.025145498995, 0.125877400021, 0.03947047877...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-265">[0.025145498995, 0.125877400021, 0.03947047877...</span></span></td>
      <td><span data-ttu-id="9f1e0-266">1</span><span class="sxs-lookup"><span data-stu-id="9f1e0-266">1</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-267">2</span><span class="sxs-lookup"><span data-stu-id="9f1e0-267">2</span></span></th>
      <td><span data-ttu-id="9f1e0-268">0</span><span class="sxs-lookup"><span data-stu-id="9f1e0-268">0</span></span></td>
      <td><span data-ttu-id="9f1e0-269">From: mathew &lt;mathew@mantis.co.uk&gt;\nSubject: R...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-269">From: mathew &lt;mathew@mantis.co.uk&gt;\nSubject: R...</span></span></td>
      <td><span data-ttu-id="9f1e0-270">[0.67566338235, 0.0150749738583, 0.00992439163...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-270">[0.67566338235, 0.0150749738583, 0.00992439163...</span></span></td>
      <td><span data-ttu-id="9f1e0-271">0</span><span class="sxs-lookup"><span data-stu-id="9f1e0-271">0</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-272">3</span><span class="sxs-lookup"><span data-stu-id="9f1e0-272">3</span></span></th>
      <td><span data-ttu-id="9f1e0-273">17</span><span class="sxs-lookup"><span data-stu-id="9f1e0-273">17</span></span></td>
      <td><span data-ttu-id="9f1e0-274">From: bakken@cs.arizona.edu (Dave Bakken)\nSub...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-274">From: bakken@cs.arizona.edu (Dave Bakken)\nSub...</span></span></td>
      <td><span data-ttu-id="9f1e0-275">[0.146063943868, 0.00232465192179, 0.002442807...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-275">[0.146063943868, 0.00232465192179, 0.002442807...</span></span></td>
      <td><span data-ttu-id="9f1e0-276">18</span><span class="sxs-lookup"><span data-stu-id="9f1e0-276">18</span></span></td>
    </tr>
    <tr>
      <th><span data-ttu-id="9f1e0-277">4</span><span class="sxs-lookup"><span data-stu-id="9f1e0-277">4</span></span></th>
      <td><span data-ttu-id="9f1e0-278">19</span><span class="sxs-lookup"><span data-stu-id="9f1e0-278">19</span></span></td>
      <td><span data-ttu-id="9f1e0-279">From: livesey@solntze.wpd.sgi.com (Jon Livesey...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-279">From: livesey@solntze.wpd.sgi.com (Jon Livesey...</span></span></td>
      <td><span data-ttu-id="9f1e0-280">[0.670712265297, 0.017332269703, 0.01062429663...</span><span class="sxs-lookup"><span data-stu-id="9f1e0-280">[0.670712265297, 0.017332269703, 0.01062429663...</span></span></td>
      <td><span data-ttu-id="9f1e0-281">0</span><span class="sxs-lookup"><span data-stu-id="9f1e0-281">0</span></span></td>
    </tr>
  </tbody>
</table>
</div>

## <a name="evaluate-model-performance"></a><span data-ttu-id="9f1e0-282">Evaluate model performance</span><span class="sxs-lookup"><span data-stu-id="9f1e0-282">Evaluate model performance</span></span>
<span data-ttu-id="9f1e0-283">The [evaluation module](https://docs.microsoft.com/python/api/tatk.evaluation) evaluates the accuracy of the trained text classifier on the test dataset.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-283">The [evaluation module](https://docs.microsoft.com/python/api/tatk.evaluation) evaluates the accuracy of the trained text classifier on the test dataset.</span></span> <span data-ttu-id="9f1e0-284">The evaluate function generates a confusion matrix and provides a macro-F1 score.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-284">The evaluate function generates a confusion matrix and provides a macro-F1 score.</span></span>

```python
 text_classifier.evaluate(df_test)          
```

    TextClassifier ::evaluate ==> start
    Time taken: 0.0 mins
    TextClassifier ::evaluate ==> end
    

<span data-ttu-id="9f1e0-285">Plot the confusion without normalization matrix for visualization.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-285">Plot the confusion without normalization matrix for visualization.</span></span>


```python
evaluator.plot_confusion_matrix(normalize=False,
                                title='Confusion matrix, without normalization', 
                                print_confusion_matrix=False,
                                figsize=(8,8),
                                colors=None)
```

<span data-ttu-id="9f1e0-286">Confusion matrix, without normalization</span><span class="sxs-lookup"><span data-stu-id="9f1e0-286">Confusion matrix, without normalization</span></span>
    
<span data-ttu-id="9f1e0-287">When running the notebook the confusion matrix will be displayed</span><span class="sxs-lookup"><span data-stu-id="9f1e0-287">When running the notebook the confusion matrix will be displayed</span></span>



<span data-ttu-id="9f1e0-288">Plot the normalized confusion matrix for visualization.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-288">Plot the normalized confusion matrix for visualization.</span></span>


```python
evaluator.plot_confusion_matrix(normalize=True,
                                title='Normalized Confusion matrix', 
                                print_confusion_matrix=False,
                                figsize=(8,8),
                                colors=None)
```

    Normalized confusion matrix
   
<span data-ttu-id="9f1e0-289">When running the notebook the confusion matrix will be displayed</span><span class="sxs-lookup"><span data-stu-id="9f1e0-289">When running the notebook the confusion matrix will be displayed</span></span>

## <a name="save-the-pipeline"></a><span data-ttu-id="9f1e0-290">Save the pipeline</span><span class="sxs-lookup"><span data-stu-id="9f1e0-290">Save the pipeline</span></span>
<span data-ttu-id="9f1e0-291">Save the classification pipeline into a zip file.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-291">Save the classification pipeline into a zip file.</span></span> <span data-ttu-id="9f1e0-292">Also, save the word-ngrams and character n-grams as text files.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-292">Also, save the word-ngrams and character n-grams as text files.</span></span>

```python
import os
working_dir = os.path.join(data_dir, 'outputs')  
if not os.path.exists(working_dir):
    os.makedirs(working_dir)

# you can save the trained model as a folder or a zip file
model_file = os.path.join(working_dir, 'sk_model.zip')    
text_classifier.save(model_file)
# %azureml upload outputs/models/sk_model.zip

```
    BaseTextModel::save ==> start
    TatkPipeline::save ==> start
    Time taken: 0.28 mins
    TatkPipeline::save ==> end
    Time taken: 0.38 mins
    BaseTextModel::save ==> end
    
```python
# for debugging, you can save the word n-grams vocabulary to a text file
word_vocab_file_path = os.path.join(working_dir, 'word_ngrams_vocabulary.tsv')
text_classifier.get_step_by_name("text_word_ngrams").save_vocabulary(word_vocab_file_path) 
# %azureml upload outputs/dictionaries/word_ngrams_vocabulary.pkl

# for debugging, you can save the character n-grams vocabulary to a text file
char_vocab_file_path = os.path.join(working_dir, 'char_ngrams_vocabulary.tsv')
text_classifier.get_step_by_name("text_char_ngrams").save_vocabulary(char_vocab_file_path) 
# %azureml upload outputs/dictionaries/char_ngrams_vocabulary.pkl
```

    save_vocabulary ==> start
    saving 216393 n-grams ...
    Time taken: 0.01 mins
    save_vocabulary ==> end
    save_vocabulary ==> start
    saving 67230 n-grams ...
    Time taken: 0.0 mins
    save_vocabulary ==> end
 
## <a name="load-the-pipeline"></a><span data-ttu-id="9f1e0-293">Load the pipeline</span><span class="sxs-lookup"><span data-stu-id="9f1e0-293">Load the pipeline</span></span>
<span data-ttu-id="9f1e0-294">Load the classification pipeline and the word-ngrams and character n-grams for inferencing:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-294">Load the classification pipeline and the word-ngrams and character n-grams for inferencing:</span></span>

```python
# in order to deploy the trained model, you have to load the zip file of the classifier pipeline
loaded_text_classifier = TextClassifier.load(model_file)

from tatk.feature_extraction import NGramsVectorizer
word_ngram_vocab = NGramsVectorizer.load_vocabulary(word_vocab_file_path)
char_ngram_vocab = NGramsVectorizer.load_vocabulary(char_vocab_file_path)
```
    BaseTextModel::load ==> start
    TatkPipeline::load ==> start
    Time taken: 0.14 mins
    TatkPipeline::load ==> end
    Time taken: 0.15 mins
    BaseTextModel::load ==> end
    loading 216393 n-grams ...
    loading 67230 n-grams ...
    

## <a name="test-the-pipeline"></a><span data-ttu-id="9f1e0-295">Test the pipeline</span><span class="sxs-lookup"><span data-stu-id="9f1e0-295">Test the pipeline</span></span>

<span data-ttu-id="9f1e0-296">To evaluate a test dataset, apply the loaded text classification pipeline:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-296">To evaluate a test dataset, apply the loaded text classification pipeline:</span></span>

```python
predictions = loaded_text_classifier.predict(df_test)
loaded_evaluator = loaded_text_classifier.evaluate(predictions)
loaded_evaluator.get_metrics('macro_f1')
```
    TextClassifier ::predict ==> start
    NltkPreprocessor::tatk_transform ==> start
    NltkPreprocessor::tatk_transform ==> end     Time taken: 0.05 mins
    NGramsVectorizer::tatk_transform ==> startNGramsVectorizer::tatk_transform ==> start
    
    NGramsVectorizer::tatk_transform ==> end     Time taken: 0.14 mins
    NGramsVectorizer::tatk_transform ==> end     Time taken: 0.36 mins
    VectorAssembler::transform ==> start, num of input records=7532
    (7532, 216393)
    (7532, 67230)
    all_features::
    (7532, 283623)
    Time taken: 0.03 mins
    VectorAssembler::transform ==> end
    LogisticRegression::tatk_predict_proba ==> start
    LogisticRegression::tatk_predict_proba ==> end   Time taken: 0.01 mins
    LogisticRegression::tatk_predict ==> start
    LogisticRegression::tatk_predict ==> end     Time taken: 0.01 mins
    Time taken: 0.45 mins
    TextClassifier ::predict ==> end
    Order of Labels in predicted probabilities saved to attribute label_order of the class object
    TextClassifier ::evaluate ==> start
    Time taken: 0.0 mins
    TextClassifier ::evaluate ==> en
    
    0.82727029243808903

## <a name="operationalization-deploy-and-consume"></a><span data-ttu-id="9f1e0-297">Operationalization: deploy and consume</span><span class="sxs-lookup"><span data-stu-id="9f1e0-297">Operationalization: deploy and consume</span></span>

<span data-ttu-id="9f1e0-298">In this section, you deploy the text classification pipeline as an Azure Machine Learning web service using [Azure Machine Learning CLI](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/cli-for-azure-machine-learning).</span><span class="sxs-lookup"><span data-stu-id="9f1e0-298">In this section, you deploy the text classification pipeline as an Azure Machine Learning web service using [Azure Machine Learning CLI](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/cli-for-azure-machine-learning).</span></span> <span data-ttu-id="9f1e0-299">Then, you consume the web service for training and scoring.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-299">Then, you consume the web service for training and scoring.</span></span>

<span data-ttu-id="9f1e0-300">**Log in to your Azure subscription with Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="9f1e0-300">**Log in to your Azure subscription with Azure CLI**</span></span>

<span data-ttu-id="9f1e0-301">Using an [Azure](https://azure.microsoft.com/) account with a valid subscription, log in using the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-301">Using an [Azure](https://azure.microsoft.com/) account with a valid subscription, log in using the following CLI command:</span></span>
<br>`az login`

+ <span data-ttu-id="9f1e0-302">To switch to another Azure subscription, use the command:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-302">To switch to another Azure subscription, use the command:</span></span>
<br>`az account set --subscription [your subscription name]`

+ <span data-ttu-id="9f1e0-303">To see the current model management account, use the command:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-303">To see the current model management account, use the command:</span></span>
  <br>`az ml account modelmanagement show`

<span data-ttu-id="9f1e0-304">**Create and set your deployment environment**</span><span class="sxs-lookup"><span data-stu-id="9f1e0-304">**Create and set your deployment environment**</span></span>

<span data-ttu-id="9f1e0-305">You only need to set your deployment environment once.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-305">You only need to set your deployment environment once.</span></span> <span data-ttu-id="9f1e0-306">If you don't have one yet, set up your deployment environment now using [these instructions](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/deployment-setup-configuration#environment-setup).</span><span class="sxs-lookup"><span data-stu-id="9f1e0-306">If you don't have one yet, set up your deployment environment now using [these instructions](https://docs.microsoft.com/azure/machine-learning/desktop-workbench/deployment-setup-configuration#environment-setup).</span></span> 

1. <span data-ttu-id="9f1e0-307">Make sure your Azure Machine Learning environment, model management account, and resource group are located in the same region.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-307">Make sure your Azure Machine Learning environment, model management account, and resource group are located in the same region.</span></span>

1. <span data-ttu-id="9f1e0-308">Download the deployment configuration file from Blob storage and save it locally:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-308">Download the deployment configuration file from Blob storage and save it locally:</span></span>

   ```python
   # Download the deployment config file from Blob storage `url` and save it locally under `file_name`:
   deployment_config_file_url = 'https://aztatksa.blob.core.windows.net/dailyrelease/tatk_deploy_config.yaml'
   deployment_config_file_path=os.path.join(resources_dir, 'tatk_deploy_config.yaml')
   import urllib.request
   urllib.request.urlretrieve(deployment_config_file_url, deployment_config_file_path)
   ```

1. <span data-ttu-id="9f1e0-309">Update the deployment configuration file you downloaded to reflect your resources:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-309">Update the deployment configuration file you downloaded to reflect your resources:</span></span>

   ```python
   web_service_name = 'please type your web service name'
   working_directory= os.path.join(resources_dir, 'deployment') 

   web_service = text_classifier.deploy(web_service_name= web_service_name, 
                          config_file_path=deployment_config_file_path,
                          working_directory= working_directory)  
   ```

1. <span data-ttu-id="9f1e0-310">Given that the trained model is deployed successfully, invoke the scoring web service on new dataset:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-310">Given that the trained model is deployed successfully, invoke the scoring web service on new dataset:</span></span>

   ```python
   print("Service URL: {}".format(web_service._service_url))
   print("Service Key: {}".format(web_service._api_key))
   ```

1. <span data-ttu-id="9f1e0-311">Load the web service at any time using its name:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-311">Load the web service at any time using its name:</span></span>

   ```python
   from tatk.operationalization.csi.csi_web_service import CsiWebService
   url = "<please type the service URL here>"
   key = "<please type the service Key here>"
   web_service = CsiWebService(url, key)
   ```

1. <span data-ttu-id="9f1e0-312">Test the web service with the body of two emails taken from the 20 newsgrpoups dataset:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-312">Test the web service with the body of two emails taken from the 20 newsgrpoups dataset:</span></span>

   ```python
   # Example input data for scoring
   import json
   dict1 ={}
   dict1["recordId"] = "a1" 
   dict1["data"]= {}
   dict1["data"]["text"] = """
   I'd be interested in a copy of this code if you run across it.
   (Mail to the author bounced)
    > / hpldsla:comp.graphics / email-address-removed / 12:53 am  May 13,
    1993 /
    > I fooled around with this problem a few years ago, and implemented a
    > simple method that ran on a PC.
    > was very simple - about 40 or 50 lines of code.
    . . .
    > Somewhere I still have it
    > and could dig it out if there was interest.
   """
   
   dict2 ={}
   dict2["recordId"] = "b2"
   dict2["data"] ={}
   dict2["data"]["text"] = """
   >>Could the people discussing recreational drugs such as mj, lsd, mdma, etc.,
   >>take their discussions to alt.drugs? Their discussions will receive greatest
   >>contribution and readership there. The people interested in strictly
   >>"smart drugs" (i.e. Nootropics) should post to this group. The two groups
   >>(alt.drugs & alt.psychoactives) have been used interchangably lately.
   >>I do think that alt.psychoactives is a deceiving name. alt.psychoactives
   >>is supposedly the "smart drug" newsgroup according to newsgroup lists on
   >>the Usenet. Should we establish an alt.nootropics or alt.sdn (smart drugs &
   >>nutrients)? I have noticed some posts in sci.med.nutrition regarding
   >>"smart nutrients." We may lower that groups burden as well.
   >   

   I was wondering if a group called 'sci.pharmacology' would be relevent.
   This would be used for a more formal discussion about pharmacological
   issues (pharmacodynamics, neuropharmacology, etc.)      

   Just an informal proposal (I don't know anything about the net.politics
   for adding a newsgroup, etc.)

   """

   dict_list =[dict1, dict2]
   data ={}
   data["values"] = dict_list
   input_data_json_str = json.dumps(data)
   print (input_data_json_str)
   prediction = web_service.score(input_data_json_str)
   prediction
   ```

   ```
   {"values": [{"recordId": "a1", "data": {"text": "\nI'd be interested in a copy of this code if you run across it.\n(Mail to the author bounced)\n > / hpldsla:comp.graphics / email-address-removed / 12:53 am  May 13,\n 1993 /\n > I fooled around with this problem a few years ago, and implemented a\n > simple method that ran on a PC.\n > was very simple - about 40 or 50 lines of code.\n . . .\n > Somewhere I still have it\n > and could dig it out if there was interest.\n"}}, {"recordId": "b2", "data": {"text": "\n>>Could the people discussing recreational drugs such as mj, lsd, mdma, etc.,\n>>take their discussions to alt.drugs? Their discussions will receive greatest\n>>contribution and readership there. The people interested in strictly\n>>\"smart drugs\" (i.e. Nootropics) should post to this group. The two groups\n>>(alt.drugs & alt.psychoactives) have been used interchangably lately.\n>>I do think that alt.psychoactives is a deceiving name. alt.psychoactives\n>>is supposedly the \"smart drug\" newsgroup according to newsgroup lists on\n>>the Usenet. Should we establish an alt.nootropics or alt.sdn (smart drugs &\n>>nutrients)? I have noticed some posts in sci.med.nutrition regarding\n>>\"smart nutrients.\" We may lower that groups burden as well.\n>\n\nI was wondering if a group called 'sci.pharmacology' would be relevent.\nThis would be used for a more formal discussion about pharmacological\nissues (pharmacodynamics, neuropharmacology, etc.)\n\nJust an informal proposal (I don't know anything about the net.politics\nfor adding a newsgroup, etc.)\n\n"}}]}
   F1 2018-05-02 00:10:58,272 INFO Web service scored. 
    
   '{"values": [{"recordId": "b2", "data": {"text": "\\n>>Could the people discussing recreational drugs such as mj, lsd, mdma, etc.,\\n>>take their discussions to alt.drugs? Their discussions will receive greatest\\n>>contribution and readership there. The people interested in strictly\\n>>\\"smart drugs\\" (i.e. Nootropics) should post to this group. The two groups\\n>>(alt.drugs & alt.psychoactives) have been used interchangably lately.\\n>>I do think that alt.psychoactives is a deceiving name. alt.psychoactives\\n>>is supposedly the \\"smart drug\\" newsgroup according to newsgroup lists on\\n>>the Usenet. Should we establish an alt.nootropics or alt.sdn (smart drugs &\\n>>nutrients)? I have noticed some posts in sci.med.nutrition regarding\\n>>\\"smart nutrients.\\" We may lower that groups burden as well.\\n>\\n\\nI was wondering if a group called \'sci.pharmacology\' would be relevent.\\nThis would be used for a more formal discussion about pharmacological\\nissues (pharmacodynamics, neuropharmacology, etc.)\\n\\nJust an informal proposal (I don\'t know anything about the net.politics\\nfor adding a newsgroup, etc.)\\n\\n", "class": 13}}, {"recordId": "a1", "data": {"text": "\\nI\'d be interested in a copy of this code if you run across it.\\n(Mail to the author bounced)\\n > / hpldsla:comp.graphics / email-address-removed / 12:53 am  May 13,\\n 1993 /\\n > I fooled around with this problem a few years ago, and implemented a\\n > simple method that ran on a PC.\\n > was very simple - about 40 or 50 lines of code.\\n . . .\\n > Somewhere I still have it\\n > and could dig it out if there was interest.\\n", "class": 1}}]}'
   ```


## <a name="next-steps"></a><span data-ttu-id="9f1e0-313">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f1e0-313">Next steps</span></span>

<span data-ttu-id="9f1e0-314">Learn more about Azure Machine Learning Package for Text Analytics in these articles:</span><span class="sxs-lookup"><span data-stu-id="9f1e0-314">Learn more about Azure Machine Learning Package for Text Analytics in these articles:</span></span>

+ <span data-ttu-id="9f1e0-315">Read the [package overview and learn how to install it](https://aka.ms/aml-packages/text).</span><span class="sxs-lookup"><span data-stu-id="9f1e0-315">Read the [package overview and learn how to install it](https://aka.ms/aml-packages/text).</span></span>

+ <span data-ttu-id="9f1e0-316">Explore the [reference documentation](https://aka.ms/aml-packages/text) for this package.</span><span class="sxs-lookup"><span data-stu-id="9f1e0-316">Explore the [reference documentation](https://aka.ms/aml-packages/text) for this package.</span></span>

+ <span data-ttu-id="9f1e0-317">Learn about [other Python packages for Azure Machine Learning](reference-python-package-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9f1e0-317">Learn about [other Python packages for Azure Machine Learning](reference-python-package-overview.md).</span></span>

