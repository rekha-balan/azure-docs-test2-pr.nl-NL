---
title: Python Flask web application tutorial for Azure DocumentDB | Microsoft Docs
description: Review a database tutorial on using DocumentDB to store and access data from a Python Flask web application hosted on Azure. Find application development solutions.
keywords: Application development, python flask, python web application, python web development
services: documentdb
documentationcenter: python
author: syamkmsft
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: documentdb
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 11/16/2016
ms.author: syamk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6e23087e42c6e93720f98d602dab23aa373bd33c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552882"
---
# <a name="build-a-python-flask-web-application-using-documentdb"></a><span data-ttu-id="52d3e-105">Build a Python Flask web application using DocumentDB</span><span class="sxs-lookup"><span data-stu-id="52d3e-105">Build a Python Flask web application using DocumentDB</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [.NET for MongoDB](documentdb-mongodb-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

<span data-ttu-id="52d3e-111">This tutorial shows you how to use Azure DocumentDB to store and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span><span class="sxs-lookup"><span data-stu-id="52d3e-111">This tutorial shows you how to use Azure DocumentDB to store and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="52d3e-112">This database tutorial covers:</span><span class="sxs-lookup"><span data-stu-id="52d3e-112">This database tutorial covers:</span></span>

1. <span data-ttu-id="52d3e-113">Creating and provisioning a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="52d3e-113">Creating and provisioning a DocumentDB account.</span></span>
2. <span data-ttu-id="52d3e-114">Creating a Python MVC application.</span><span class="sxs-lookup"><span data-stu-id="52d3e-114">Creating a Python MVC application.</span></span>
3. <span data-ttu-id="52d3e-115">Connecting to and using Azure DocumentDB from your web application.</span><span class="sxs-lookup"><span data-stu-id="52d3e-115">Connecting to and using Azure DocumentDB from your web application.</span></span>
4. <span data-ttu-id="52d3e-116">Deploying the web application to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="52d3e-116">Deploying the web application to Azure Websites.</span></span>

<span data-ttu-id="52d3e-117">By following this tutorial, you will build a simple voting application that allows you to vote for a poll.</span><span class="sxs-lookup"><span data-stu-id="52d3e-117">By following this tutorial, you will build a simple voting application that allows you to vote for a poll.</span></span>

![Screen shot of the todo list web application created by this database tutorial](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image1.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="52d3e-119">Database tutorial prerequisites</span><span class="sxs-lookup"><span data-stu-id="52d3e-119">Database tutorial prerequisites</span></span>
<span data-ttu-id="52d3e-120">Before following the instructions in this article, you should ensure that you have the following installed:</span><span class="sxs-lookup"><span data-stu-id="52d3e-120">Before following the instructions in this article, you should ensure that you have the following installed:</span></span>

* <span data-ttu-id="52d3e-121">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="52d3e-121">An active Azure account.</span></span> <span data-ttu-id="52d3e-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="52d3e-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="52d3e-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52d3e-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="52d3e-124">OR</span><span class="sxs-lookup"><span data-stu-id="52d3e-124">OR</span></span> 

    <span data-ttu-id="52d3e-125">A local installation of the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="52d3e-125">A local installation of the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md).</span></span>
* <span data-ttu-id="52d3e-126">[Visual Studio 2013](http://www.visualstudio.com/) or higher, or [Visual Studio Express](), which is the free version.</span><span class="sxs-lookup"><span data-stu-id="52d3e-126">[Visual Studio 2013](http://www.visualstudio.com/) or higher, or [Visual Studio Express](), which is the free version.</span></span> <span data-ttu-id="52d3e-127">The instructions in this tutorial are written specifically for Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="52d3e-127">The instructions in this tutorial are written specifically for Visual Studio 2015.</span></span> 
* <span data-ttu-id="52d3e-128">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="52d3e-128">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="52d3e-129">This tutorial uses Python Tools for VS 2015.</span><span class="sxs-lookup"><span data-stu-id="52d3e-129">This tutorial uses Python Tools for VS 2015.</span></span> 
* <span data-ttu-id="52d3e-130">Azure Python SDK for Visual Studio, version 2.4 or higher available from [azure.com](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="52d3e-130">Azure Python SDK for Visual Studio, version 2.4 or higher available from [azure.com](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="52d3e-131">We used Microsoft Azure SDK for Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="52d3e-131">We used Microsoft Azure SDK for Python 2.7.</span></span>
* <span data-ttu-id="52d3e-132">Python 2.7 from [python.org][2]. We used Python 2.7.11.</span><span class="sxs-lookup"><span data-stu-id="52d3e-132">Python 2.7 from [python.org][2]. We used Python 2.7.11.</span></span> 

> [!IMPORTANT]
> If you are installing Python 2.7 for the first time, ensure that in the Customize Python 2.7.11 screen, you select **Add python.exe to Path**.
> 
> ![Screen shot of the Customize Python 2.7.11 screen, where you need to select Add python.exe to Path](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image2.png)
> 
> 

* <span data-ttu-id="52d3e-135">Microsoft Visual C++ Compiler for Python 2.7 from the [Microsoft Download Center][3].</span><span class="sxs-lookup"><span data-stu-id="52d3e-135">Microsoft Visual C++ Compiler for Python 2.7 from the [Microsoft Download Center][3].</span></span>

## <a name="step-1-create-a-documentdb-database-account"></a><span data-ttu-id="52d3e-136">Step 1: Create a DocumentDB database account</span><span class="sxs-lookup"><span data-stu-id="52d3e-136">Step 1: Create a DocumentDB database account</span></span>
<span data-ttu-id="52d3e-137">Let's start by creating a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="52d3e-137">Let's start by creating a DocumentDB account.</span></span> <span data-ttu-id="52d3e-138">If you already have an account or if you are using the DocumentDB Emulator for this tutorial, you can skip to [Step 2: Create a new Python Flask web application](#step-2:-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="52d3e-138">If you already have an account or if you are using the DocumentDB Emulator for this tutorial, you can skip to [Step 2: Create a new Python Flask web application](#step-2:-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

<br/>
<span data-ttu-id="52d3e-139">We will now walk through how to create a new Python Flask web application from the ground up.</span><span class="sxs-lookup"><span data-stu-id="52d3e-139">We will now walk through how to create a new Python Flask web application from the ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="52d3e-140">Step 2: Create a new Python Flask web application</span><span class="sxs-lookup"><span data-stu-id="52d3e-140">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="52d3e-141">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-141">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="52d3e-142">The **New Project** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="52d3e-142">The **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="52d3e-143">In the left pane, expand **Templates** and then **Python**, and then click **Web**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-143">In the left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="52d3e-144">Select **Flask  Web Project** in the center pane, then in the **Name** box type **tutorial**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-144">Select **Flask  Web Project** in the center pane, then in the **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="52d3e-145">Remember that Python package names should be all lowercase, as described in the [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="52d3e-145">Remember that Python package names should be all lowercase, as described in the [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="52d3e-146">For those new to Python Flask, it is a web application development framework that helps you build web applications in Python faster.</span><span class="sxs-lookup"><span data-stu-id="52d3e-146">For those new to Python Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Screen shot of the New Project window in Visual Studio with Python highlighted on the left, Python Flask Web Project selected in the middle, and the name tutorial in the Name box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image9.png)
4. <span data-ttu-id="52d3e-148">In the **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-148">In the **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Screen shot of the database tutorial - Python Tools for Visual Studio window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image10.png)
5. <span data-ttu-id="52d3e-150">In the **Add Virtual Environment** window, you can accept the defaults and use Python 2.7 as the base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-150">In the **Add Virtual Environment** window, you can accept the defaults and use Python 2.7 as the base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="52d3e-151">This sets up the required Python virtual environment for your project.</span><span class="sxs-lookup"><span data-stu-id="52d3e-151">This sets up the required Python virtual environment for your project.</span></span>
   
    ![Screen shot of the database tutorial - Python Tools for Visual Studio window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="52d3e-153">The output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when the environment is successfully installed.</span><span class="sxs-lookup"><span data-stu-id="52d3e-153">The output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when the environment is successfully installed.</span></span>

## <a name="step-3-modify-the-python-flask-web-application"></a><span data-ttu-id="52d3e-154">Step 3: Modify the Python Flask web application</span><span class="sxs-lookup"><span data-stu-id="52d3e-154">Step 3: Modify the Python Flask web application</span></span>
### <a name="add-the-python-flask-packages-to-your-project"></a><span data-ttu-id="52d3e-155">Add the Python Flask packages to your project</span><span class="sxs-lookup"><span data-stu-id="52d3e-155">Add the Python Flask packages to your project</span></span>
<span data-ttu-id="52d3e-156">After your project is set up, you'll need to add the required Flask packages to your project, including pydocumentdb, the Python package for DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="52d3e-156">After your project is set up, you'll need to add the required Flask packages to your project, including pydocumentdb, the Python package for DocumentDB.</span></span>

1. <span data-ttu-id="52d3e-157">In Solution Explorer, open the file named **requirements.txt** and replace the contents with the following:</span><span class="sxs-lookup"><span data-stu-id="52d3e-157">In Solution Explorer, open the file named **requirements.txt** and replace the contents with the following:</span></span>
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. <span data-ttu-id="52d3e-158">Save the **requirements.txt** file.</span><span class="sxs-lookup"><span data-stu-id="52d3e-158">Save the **requirements.txt** file.</span></span> 
3. <span data-ttu-id="52d3e-159">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-159">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Screen shot showing env (Python 2.7) selected with Install from requirements.txt highlighted in the list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image11.png)
   
    <span data-ttu-id="52d3e-161">After successful installation, the output window displays the following:</span><span class="sxs-lookup"><span data-stu-id="52d3e-161">After successful installation, the output window displays the following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > In rare cases, you might see a failure in the output window. If this happens, check if the error is related to cleanup. Sometimes the cleanup fails, but the installation will still be successful (scroll up in the output window to verify this). You can check your installation by [Verifying the virtual environment](#verify-the-virtual-environment). If the installation failed but the verification is successful, it's OK to continue.
   > 
   > 

### <a name="verify-the-virtual-environment"></a><span data-ttu-id="52d3e-167">Verify the virtual environment</span><span class="sxs-lookup"><span data-stu-id="52d3e-167">Verify the virtual environment</span></span>
<span data-ttu-id="52d3e-168">Let's make sure that everything is installed correctly.</span><span class="sxs-lookup"><span data-stu-id="52d3e-168">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="52d3e-169">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-169">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="52d3e-170">Once the build succeeds, start the website by pressing **F5**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-170">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="52d3e-171">This launches the Flask development server and starts your web browser.</span><span class="sxs-lookup"><span data-stu-id="52d3e-171">This launches the Flask development server and starts your web browser.</span></span> <span data-ttu-id="52d3e-172">You should see the following page.</span><span class="sxs-lookup"><span data-stu-id="52d3e-172">You should see the following page.</span></span>
   
    ![The empty Python Flask web development project displayed in a browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image12.png)
3. <span data-ttu-id="52d3e-174">Stop debugging the website by pressing **Shift**+**F5** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52d3e-174">Stop debugging the website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="52d3e-175">Create database, collection, and document definitions</span><span class="sxs-lookup"><span data-stu-id="52d3e-175">Create database, collection, and document definitions</span></span>
<span data-ttu-id="52d3e-176">Now let's create your voting application by adding new files and updating others.</span><span class="sxs-lookup"><span data-stu-id="52d3e-176">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="52d3e-177">In Solution Explorer, right-click the **tutorial** project, click **Add**, and then click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-177">In Solution Explorer, right-click the **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="52d3e-178">Select **Empty Python File** and name the file **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-178">Select **Empty Python File** and name the file **forms.py**.</span></span>  
2. <span data-ttu-id="52d3e-179">Add the following code to the forms.py file, and then save the file.</span><span class="sxs-lookup"><span data-stu-id="52d3e-179">Add the following code to the forms.py file, and then save the file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a><span data-ttu-id="52d3e-180">Add the required imports to views.py</span><span class="sxs-lookup"><span data-stu-id="52d3e-180">Add the required imports to views.py</span></span>
1. <span data-ttu-id="52d3e-181">In Solution Explorer, expand the **tutorial** folder, and open the **views.py** file.</span><span class="sxs-lookup"><span data-stu-id="52d3e-181">In Solution Explorer, expand the **tutorial** folder, and open the **views.py** file.</span></span> 
2. <span data-ttu-id="52d3e-182">Add the following import statements to the top of the **views.py** file, then save the file.</span><span class="sxs-lookup"><span data-stu-id="52d3e-182">Add the following import statements to the top of the **views.py** file, then save the file.</span></span> <span data-ttu-id="52d3e-183">These import DocumentDB's PythonSDK and the Flask packages.</span><span class="sxs-lookup"><span data-stu-id="52d3e-183">These import DocumentDB's PythonSDK and the Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="52d3e-184">Create database, collection, and document</span><span class="sxs-lookup"><span data-stu-id="52d3e-184">Create database, collection, and document</span></span>
* <span data-ttu-id="52d3e-185">Still in **views.py**, add the following code to the end of the file.</span><span class="sxs-lookup"><span data-stu-id="52d3e-185">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="52d3e-186">This takes care of creating the database used by the form.</span><span class="sxs-lookup"><span data-stu-id="52d3e-186">This takes care of creating the database used by the form.</span></span> <span data-ttu-id="52d3e-187">Do not delete any of the existing code in **views.py**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-187">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="52d3e-188">Simply append this to the end.</span><span class="sxs-lookup"><span data-stu-id="52d3e-188">Simply append this to the end.</span></span>

```python
@app.route('/create')
def create():
    """Renders the contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt to delete the database.  This allows this to be used to recreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```

> [!TIP]
> The **CreateCollection** method takes an optional **RequestOptions** as the third parameter. This can be used to specify the Offer Type for the collection. If no offerType value is supplied, then the collection will be created using the default Offer Type. For more information on DocumentDB Offer Types, see [Performance levels in DocumentDB](documentdb-performance-levels.md).
> 
> 

### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="52d3e-193">Read database, collection, document, and submit form</span><span class="sxs-lookup"><span data-stu-id="52d3e-193">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="52d3e-194">Still in **views.py**, add the following code to the end of the file.</span><span class="sxs-lookup"><span data-stu-id="52d3e-194">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="52d3e-195">This takes care of setting up the form, reading the database, collection, and document.</span><span class="sxs-lookup"><span data-stu-id="52d3e-195">This takes care of setting up the form, reading the database, collection, and document.</span></span> <span data-ttu-id="52d3e-196">Do not delete any of the existing code in **views.py**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-196">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="52d3e-197">Simply append this to the end.</span><span class="sxs-lookup"><span data-stu-id="52d3e-197">Simply append this to the end.</span></span>

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take the data from the deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model to pass to results.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-the-html-files"></a><span data-ttu-id="52d3e-198">Create the HTML files</span><span class="sxs-lookup"><span data-stu-id="52d3e-198">Create the HTML files</span></span>
1. <span data-ttu-id="52d3e-199">In Solution Explorer, in the **tutorial** folder, right click the **templates** folder, click **Add**, and then click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-199">In Solution Explorer, in the **tutorial** folder, right click the **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="52d3e-200">Select **HTML Page**, and then in the name box type **create.html**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-200">Select **HTML Page**, and then in the name box type **create.html**.</span></span> 
3. <span data-ttu-id="52d3e-201">Repeat steps 1 and 2 to create two additional HTML files: results.html and vote.html.</span><span class="sxs-lookup"><span data-stu-id="52d3e-201">Repeat steps 1 and 2 to create two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="52d3e-202">Add the following code to **create.html** in the `<body>` element.</span><span class="sxs-lookup"><span data-stu-id="52d3e-202">Add the following code to **create.html** in the `<body>` element.</span></span> <span data-ttu-id="52d3e-203">It displays a message stating that we created a new database, collection, and document.</span><span class="sxs-lookup"><span data-stu-id="52d3e-203">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="52d3e-204">Add the following code to **results.html** in the `<body`> element.</span><span class="sxs-lookup"><span data-stu-id="52d3e-204">Add the following code to **results.html** in the `<body`> element.</span></span> <span data-ttu-id="52d3e-205">It displays the results of the poll.</span><span class="sxs-lookup"><span data-stu-id="52d3e-205">It displays the results of the poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of the vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. <span data-ttu-id="52d3e-206">Add the following code to **vote.html** in the `<body`> element.</span><span class="sxs-lookup"><span data-stu-id="52d3e-206">Add the following code to **vote.html** in the `<body`> element.</span></span> <span data-ttu-id="52d3e-207">It displays the poll and accepts the votes.</span><span class="sxs-lookup"><span data-stu-id="52d3e-207">It displays the poll and accepts the votes.</span></span> <span data-ttu-id="52d3e-208">On registering the votes, the control is passed over to views.py where we will recognize the vote cast and append the document accordingly.</span><span class="sxs-lookup"><span data-stu-id="52d3e-208">On registering the votes, the control is passed over to views.py where we will recognize the vote cast and append the document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way to host an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="52d3e-209">In the **templates** folder, replace the contents of **index.html** with the following.</span><span class="sxs-lookup"><span data-stu-id="52d3e-209">In the **templates** folder, replace the contents of **index.html** with the following.</span></span> <span data-ttu-id="52d3e-210">This serves as the landing page for your application.</span><span class="sxs-lookup"><span data-stu-id="52d3e-210">This serves as the landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + DocumentDB Voting Application.</h2>
    <h3>This is a sample DocumentDB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a><span data-ttu-id="52d3e-211">Add a configuration file and change the \_\_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="52d3e-211">Add a configuration file and change the \_\_init\_\_.py</span></span>
1. <span data-ttu-id="52d3e-212">In Solution Explorer, right-click the **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name the file **config.py**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-212">In Solution Explorer, right-click the **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name the file **config.py**.</span></span> <span data-ttu-id="52d3e-213">This config file is required by forms in Flask.</span><span class="sxs-lookup"><span data-stu-id="52d3e-213">This config file is required by forms in Flask.</span></span> <span data-ttu-id="52d3e-214">You can use it to provide a secret key as well.</span><span class="sxs-lookup"><span data-stu-id="52d3e-214">You can use it to provide a secret key as well.</span></span> <span data-ttu-id="52d3e-215">This key is not needed for this tutorial though.</span><span class="sxs-lookup"><span data-stu-id="52d3e-215">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="52d3e-216">Add the following code to config.py, you'll need to alter the values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in the next step.</span><span class="sxs-lookup"><span data-stu-id="52d3e-216">Add the following code to config.py, you'll need to alter the values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in the next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="52d3e-217">In the [Azure portal](https://portal.azure.com/), navigate to the **Keys** blade by clicking **Browse**, **DocumentDB Accounts**, double-click the name of the account to use, and then click the **Keys** button in the **Essentials** area.</span><span class="sxs-lookup"><span data-stu-id="52d3e-217">In the [Azure portal](https://portal.azure.com/), navigate to the **Keys** blade by clicking **Browse**, **DocumentDB Accounts**, double-click the name of the account to use, and then click the **Keys** button in the **Essentials** area.</span></span> <span data-ttu-id="52d3e-218">In the **Keys** blade, copy the **URI** value and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_HOST** property.</span><span class="sxs-lookup"><span data-stu-id="52d3e-218">In the **Keys** blade, copy the **URI** value and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="52d3e-219">Back in the Azure portal, in the **Keys** blade, copy the value of the **Primary Key** or the **Secondary Key**, and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_KEY** property.</span><span class="sxs-lookup"><span data-stu-id="52d3e-219">Back in the Azure portal, in the **Keys** blade, copy the value of the **Primary Key** or the **Secondary Key**, and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="52d3e-220">In the **\_\_init\_\_.py** file, add the following line.</span><span class="sxs-lookup"><span data-stu-id="52d3e-220">In the **\_\_init\_\_.py** file, add the following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="52d3e-221">So that the content of the file is:</span><span class="sxs-lookup"><span data-stu-id="52d3e-221">So that the content of the file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="52d3e-222">After adding all the files, Solution Explorer should look like this:</span><span class="sxs-lookup"><span data-stu-id="52d3e-222">After adding all the files, Solution Explorer should look like this:</span></span>
   
    ![Screen shot of the Visual Studio Solution Explorer window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image15.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="52d3e-224">Step 4: Run your web application locally</span><span class="sxs-lookup"><span data-stu-id="52d3e-224">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="52d3e-225">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-225">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="52d3e-226">Once the build succeeds, start the website by pressing **F5**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-226">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="52d3e-227">You should see the following on your screen.</span><span class="sxs-lookup"><span data-stu-id="52d3e-227">You should see the following on your screen.</span></span>
   
    ![Screen shot of the Python + DocumentDB Voting Application displayed in a web browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image16.png)
3. <span data-ttu-id="52d3e-229">Click **Create/Clear the Voting Database** to generate the database.</span><span class="sxs-lookup"><span data-stu-id="52d3e-229">Click **Create/Clear the Voting Database** to generate the database.</span></span>
   
    ![Screen shot of the Create Page of the web application – development details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image17.png)
4. <span data-ttu-id="52d3e-231">Then, click **Vote** and select your option.</span><span class="sxs-lookup"><span data-stu-id="52d3e-231">Then, click **Vote** and select your option.</span></span>
   
    ![Screen shot of the web application with a voting question posed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image18.png)
5. <span data-ttu-id="52d3e-233">For every vote you cast, it increments the appropriate counter.</span><span class="sxs-lookup"><span data-stu-id="52d3e-233">For every vote you cast, it increments the appropriate counter.</span></span>
   
    ![Screen shot of the Results of the vote page shown](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image19.png)
6. <span data-ttu-id="52d3e-235">Stop debugging the project by pressing Shift+F5.</span><span class="sxs-lookup"><span data-stu-id="52d3e-235">Stop debugging the project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-the-web-application-to-azure-websites"></a><span data-ttu-id="52d3e-236">Step 5: Deploy the web application to Azure Websites</span><span class="sxs-lookup"><span data-stu-id="52d3e-236">Step 5: Deploy the web application to Azure Websites</span></span>
<span data-ttu-id="52d3e-237">Now that you have the complete application working correctly against DocumentDB, we're going to deploy this to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="52d3e-237">Now that you have the complete application working correctly against DocumentDB, we're going to deploy this to Azure Websites.</span></span>

1. <span data-ttu-id="52d3e-238">Right-click the project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-238">Right-click the project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Screen shot of the tutorial selected in Solution Explorer, with the Publish option highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image20.png)
2. <span data-ttu-id="52d3e-240">In the **Publish Web** window, select **Microsoft Azure Web Apps**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-240">In the **Publish Web** window, select **Microsoft Azure Web Apps**, and then click **Next**.</span></span>
   
    ![Screen shot of the Publish Web window with Microsoft Azure Web Apps highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/image21.png)
3. <span data-ttu-id="52d3e-242">In the **Microsoft Azure Web Apps Window** window, click **New**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-242">In the **Microsoft Azure Web Apps Window** window, click **New**.</span></span>
   
    ![Screen shot of the Microsoft Azure Web Apps Window window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/select-existing-website.png)
4. <span data-ttu-id="52d3e-244">In the **Create site on Microsoft Azure** window, enter a **Web app name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-244">In the **Create site on Microsoft Azure** window, enter a **Web app name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![Screen shot of the Create site on Microsoft Azure window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/create-site-on-microsoft-azure.png)
5. <span data-ttu-id="52d3e-246">In the **Publish Web** window, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="52d3e-246">In the **Publish Web** window, click **Publish**.</span></span>
   
    ![Screen shot of the Create site on Microsoft Azure window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-python-application/publish-web.png)
6. <span data-ttu-id="52d3e-248">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handy work running in Azure!</span><span class="sxs-lookup"><span data-stu-id="52d3e-248">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handy work running in Azure!</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="52d3e-249">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="52d3e-249">Troubleshooting</span></span>
<span data-ttu-id="52d3e-250">If this is the first Python app you've run on your computer, ensure that the following folders (or the equivalent installation locations) are included in your PATH variable:</span><span class="sxs-lookup"><span data-stu-id="52d3e-250">If this is the first Python app you've run on your computer, ensure that the following folders (or the equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="52d3e-251">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references the correct project name in the line: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="52d3e-251">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references the correct project name in the line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52d3e-252">Next steps</span><span class="sxs-lookup"><span data-stu-id="52d3e-252">Next steps</span></span>
<span data-ttu-id="52d3e-253">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="52d3e-253">Congratulations!</span></span> <span data-ttu-id="52d3e-254">You have just completed your first Python web application using Azure DocumentDB and published it to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="52d3e-254">You have just completed your first Python web application using Azure DocumentDB and published it to Azure Websites.</span></span>

<span data-ttu-id="52d3e-255">We update and improve this topic frequently based on your feedback.</span><span class="sxs-lookup"><span data-stu-id="52d3e-255">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="52d3e-256">Once you've completed the tutorial, please using the voting buttons at the top and bottom of this page, and be sure to include your feedback on what improvements you want to see made.</span><span class="sxs-lookup"><span data-stu-id="52d3e-256">Once you've completed the tutorial, please using the voting buttons at the top and bottom of this page, and be sure to include your feedback on what improvements you want to see made.</span></span> <span data-ttu-id="52d3e-257">If you'd like us to contact you directly, feel free to include your email address in your comments.</span><span class="sxs-lookup"><span data-stu-id="52d3e-257">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="52d3e-258">To add additional functionality to your web application, review the APIs available in the [DocumentDB Python SDK](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="52d3e-258">To add additional functionality to your web application, review the APIs available in the [DocumentDB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="52d3e-259">For more information about Azure, Visual Studio, and Python, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="52d3e-259">For more information about Azure, Visual Studio, and Python, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="52d3e-260">For additional Python Flask tutorials, see [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="52d3e-260">For additional Python Flask tutorials, see [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com

















