---
title: Configuring Python with Azure App Service Web Apps
description: This tutorial describes options for authoring and configuring a basic Web server Gateway Interface (WSGI) compliant Python application on Azure App Service Web Apps.
services: app-service
documentationcenter: python
tags: python
author: cephalin
manager: erikre
editor: ''
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 796de682df28c28bc66f2409e486dfdc221aedd1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865081"
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="b1cea-103">Configuring Python with Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="b1cea-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="b1cea-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b1cea-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="b1cea-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="b1cea-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="b1cea-106">Bottle, Django, or Flask?</span><span class="sxs-lookup"><span data-stu-id="b1cea-106">Bottle, Django, or Flask?</span></span>
<span data-ttu-id="b1cea-107">The Azure Marketplace contains templates for the Bottle, Django, and Flask frameworks.</span><span class="sxs-lookup"><span data-stu-id="b1cea-107">The Azure Marketplace contains templates for the Bottle, Django, and Flask frameworks.</span></span> <span data-ttu-id="b1cea-108">If you are developing your first web app in Azure App Service, you can create one quickly from the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="b1cea-108">If you are developing your first web app in Azure App Service, you can create one quickly from the Azure portal:</span></span>

* [<span data-ttu-id="b1cea-109">Web app with Bottle on Linux</span><span class="sxs-lookup"><span data-stu-id="b1cea-109">Web app with Bottle on Linux</span></span>](https://portal.azure.com/#create/PTVS.BottleLinux)
* [<span data-ttu-id="b1cea-110">Web app with Django on Linux</span><span class="sxs-lookup"><span data-stu-id="b1cea-110">Web app with Django on Linux</span></span>](https://portal.azure.com/#create/PTVS.DjangoLinux)
* [<span data-ttu-id="b1cea-111">Web app with Flask on Linux</span><span class="sxs-lookup"><span data-stu-id="b1cea-111">Web app with Flask on Linux</span></span>](https://portal.azure.com/#create/PTVS.FlaskLinux)

<span data-ttu-id="b1cea-112">Or you can [explore the Azure Marketplace yourself](https://portal.azure.com/#create/hub).</span><span class="sxs-lookup"><span data-stu-id="b1cea-112">Or you can [explore the Azure Marketplace yourself](https://portal.azure.com/#create/hub).</span></span>

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="b1cea-113">Web app creation on Azure portal</span><span class="sxs-lookup"><span data-stu-id="b1cea-113">Web app creation on Azure portal</span></span>
<span data-ttu-id="b1cea-114">This tutorial assumes an existing Azure subscription and access to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b1cea-114">This tutorial assumes an existing Azure subscription and access to the Azure portal.</span></span>

<span data-ttu-id="b1cea-115">If you do not have an existing web app, you can create one from the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1cea-115">If you do not have an existing web app, you can create one from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b1cea-116">In the top left corner, click **Create a resource** > **Web + Mobile** > **Web app**.</span><span class="sxs-lookup"><span data-stu-id="b1cea-116">In the top left corner, click **Create a resource** > **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="b1cea-117">Git Publishing</span><span class="sxs-lookup"><span data-stu-id="b1cea-117">Git Publishing</span></span>
<span data-ttu-id="b1cea-118">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="b1cea-118">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="b1cea-119">This tutorial uses Git to create, manage, and publish your Python web app to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b1cea-119">This tutorial uses Git to create, manage, and publish your Python web app to Azure App Service.</span></span>

<span data-ttu-id="b1cea-120">Once Git publishing is set up, a Git repository is created and associated with your web app.</span><span class="sxs-lookup"><span data-stu-id="b1cea-120">Once Git publishing is set up, a Git repository is created and associated with your web app.</span></span> <span data-ttu-id="b1cea-121">The repository's URL is displayed and can be used to push data from the local development environment to the cloud.</span><span class="sxs-lookup"><span data-stu-id="b1cea-121">The repository's URL is displayed and can be used to push data from the local development environment to the cloud.</span></span> <span data-ttu-id="b1cea-122">To publish applications via Git, make sure a Git client is also installed and use the instructions provided to push your web app content to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b1cea-122">To publish applications via Git, make sure a Git client is also installed and use the instructions provided to push your web app content to Azure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="b1cea-123">Application Overview</span><span class="sxs-lookup"><span data-stu-id="b1cea-123">Application Overview</span></span>
<span data-ttu-id="b1cea-124">In the next sections, the following files are created.</span><span class="sxs-lookup"><span data-stu-id="b1cea-124">In the next sections, the following files are created.</span></span> <span data-ttu-id="b1cea-125">They should be placed in the root of the Git repository.</span><span class="sxs-lookup"><span data-stu-id="b1cea-125">They should be placed in the root of the Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="b1cea-126">WSGI Handler</span><span class="sxs-lookup"><span data-stu-id="b1cea-126">WSGI Handler</span></span>
<span data-ttu-id="b1cea-127">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between the web server and Python.</span><span class="sxs-lookup"><span data-stu-id="b1cea-127">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between the web server and Python.</span></span> <span data-ttu-id="b1cea-128">It provides a standardized interface for writing various web applications and frameworks using Python.</span><span class="sxs-lookup"><span data-stu-id="b1cea-128">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="b1cea-129">Popular Python web frameworks today use WSGI.</span><span class="sxs-lookup"><span data-stu-id="b1cea-129">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="b1cea-130">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as the custom handler follows the WSGI specification guidelines.</span><span class="sxs-lookup"><span data-stu-id="b1cea-130">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as the custom handler follows the WSGI specification guidelines.</span></span>

<span data-ttu-id="b1cea-131">Here's an example of an `app.py` that defines a custom handler:</span><span class="sxs-lookup"><span data-stu-id="b1cea-131">Here's an example of an `app.py` that defines a custom handler:</span></span>

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

<span data-ttu-id="b1cea-132">You can run this application locally with `python app.py`, then browse to `http://localhost:5555` in your web browser.</span><span class="sxs-lookup"><span data-stu-id="b1cea-132">You can run this application locally with `python app.py`, then browse to `http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="b1cea-133">Virtual Environment</span><span class="sxs-lookup"><span data-stu-id="b1cea-133">Virtual Environment</span></span>
<span data-ttu-id="b1cea-134">Although the preceding example app doesn't require any external packages, it is likely that your application requires some.</span><span class="sxs-lookup"><span data-stu-id="b1cea-134">Although the preceding example app doesn't require any external packages, it is likely that your application requires some.</span></span>

<span data-ttu-id="b1cea-135">To help manage external package dependencies, Azure Git deployment supports the creation of virtual environments.</span><span class="sxs-lookup"><span data-stu-id="b1cea-135">To help manage external package dependencies, Azure Git deployment supports the creation of virtual environments.</span></span>

<span data-ttu-id="b1cea-136">When Azure detects a requirements.txt in the root of the repository, it automatically creates a virtual environment named `env`.</span><span class="sxs-lookup"><span data-stu-id="b1cea-136">When Azure detects a requirements.txt in the root of the repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="b1cea-137">This only occurs on the first deployment, or during any deployment after the selected Python runtime has changed.</span><span class="sxs-lookup"><span data-stu-id="b1cea-137">This only occurs on the first deployment, or during any deployment after the selected Python runtime has changed.</span></span>

<span data-ttu-id="b1cea-138">You probably want to create a virtual environment locally for development, but don't include it in your Git repository.</span><span class="sxs-lookup"><span data-stu-id="b1cea-138">You probably want to create a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="b1cea-139">Package Management</span><span class="sxs-lookup"><span data-stu-id="b1cea-139">Package Management</span></span>
<span data-ttu-id="b1cea-140">Packages listed in requirements.txt are installed automatically in the virtual environment using pip.</span><span class="sxs-lookup"><span data-stu-id="b1cea-140">Packages listed in requirements.txt are installed automatically in the virtual environment using pip.</span></span> <span data-ttu-id="b1cea-141">This happens on every deployment, but pip skips installation if a package is already installed.</span><span class="sxs-lookup"><span data-stu-id="b1cea-141">This happens on every deployment, but pip skips installation if a package is already installed.</span></span>

<span data-ttu-id="b1cea-142">Example `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="b1cea-142">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="b1cea-143">Python Version</span><span class="sxs-lookup"><span data-stu-id="b1cea-143">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="b1cea-144">Example `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="b1cea-144">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="b1cea-145">Web.config</span><span class="sxs-lookup"><span data-stu-id="b1cea-145">Web.config</span></span>
<span data-ttu-id="b1cea-146">You need to create a web.config file to specify how the server should handle requests.</span><span class="sxs-lookup"><span data-stu-id="b1cea-146">You need to create a web.config file to specify how the server should handle requests.</span></span>

<span data-ttu-id="b1cea-147">If you have a web.x.y.config file in your repository, where x.y matches the selected Python runtime, then Azure automatically copies the appropriate file as web.config.</span><span class="sxs-lookup"><span data-stu-id="b1cea-147">If you have a web.x.y.config file in your repository, where x.y matches the selected Python runtime, then Azure automatically copies the appropriate file as web.config.</span></span>

<span data-ttu-id="b1cea-148">The following web.config examples rely on a virtual environment proxy script, which is described in the next section.</span><span class="sxs-lookup"><span data-stu-id="b1cea-148">The following web.config examples rely on a virtual environment proxy script, which is described in the next section.</span></span>  <span data-ttu-id="b1cea-149">They work with the WSGI handler used in the example `app.py` above.</span><span class="sxs-lookup"><span data-stu-id="b1cea-149">They work with the WSGI handler used in the example `app.py` above.</span></span>

<span data-ttu-id="b1cea-150">Example `web.config` for Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="b1cea-150">Example `web.config` for Python 2.7:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="b1cea-151">Example `web.config` for Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="b1cea-151">Example `web.config` for Python 3.4:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="b1cea-152">Static files are handled by the web server directly, without going through Python code, for improved performance.</span><span class="sxs-lookup"><span data-stu-id="b1cea-152">Static files are handled by the web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="b1cea-153">In the preceding examples, the location of the static files on disk should match the location in the URL.</span><span class="sxs-lookup"><span data-stu-id="b1cea-153">In the preceding examples, the location of the static files on disk should match the location in the URL.</span></span> <span data-ttu-id="b1cea-154">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve the file on disk at `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="b1cea-154">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve the file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="b1cea-155">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify the WSGI handler.</span><span class="sxs-lookup"><span data-stu-id="b1cea-155">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify the WSGI handler.</span></span> <span data-ttu-id="b1cea-156">In the preceding examples, it's `app.wsgi_app` because the handler is a function named `wsgi_app` in `app.py` in the root folder.</span><span class="sxs-lookup"><span data-stu-id="b1cea-156">In the preceding examples, it's `app.wsgi_app` because the handler is a function named `wsgi_app` in `app.py` in the root folder.</span></span>

<span data-ttu-id="b1cea-157">`PYTHONPATH` can be customized, but if you install all your dependencies in the virtual environment by specifying them in requirements.txt, you shouldn't need to change it.</span><span class="sxs-lookup"><span data-stu-id="b1cea-157">`PYTHONPATH` can be customized, but if you install all your dependencies in the virtual environment by specifying them in requirements.txt, you shouldn't need to change it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="b1cea-158">Virtual Environment Proxy</span><span class="sxs-lookup"><span data-stu-id="b1cea-158">Virtual Environment Proxy</span></span>
<span data-ttu-id="b1cea-159">The following script is used to retrieve the WSGI handler, activate the virtual environment and log errors.</span><span class="sxs-lookup"><span data-stu-id="b1cea-159">The following script is used to retrieve the WSGI handler, activate the virtual environment and log errors.</span></span> <span data-ttu-id="b1cea-160">It is designed to be generic and used without modifications.</span><span class="sxs-lookup"><span data-stu-id="b1cea-160">It is designed to be generic and used without modifications.</span></span>

<span data-ttu-id="b1cea-161">Contents of `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="b1cea-161">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject to terms and conditions of the Apache License, Version 2.0. A 
     # copy of the license can be found in the License.html file at the root of this distribution. If 
     # you cannot locate the Apache License, Version 2.0, please send an email to 
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing to be bound 
     # by the terms of the Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors to a log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a><span data-ttu-id="b1cea-162">Customize Git deployment</span><span class="sxs-lookup"><span data-stu-id="b1cea-162">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="b1cea-163">Troubleshooting - Package Installation</span><span class="sxs-lookup"><span data-stu-id="b1cea-163">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="b1cea-164">Troubleshooting - Virtual Environment</span><span class="sxs-lookup"><span data-stu-id="b1cea-164">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---startup-errors"></a><span data-ttu-id="b1cea-165">Troubleshooting - Startup Errors</span><span class="sxs-lookup"><span data-stu-id="b1cea-165">Troubleshooting - Startup Errors</span></span>
[!INCLUDE [web-sites-python-troubleshooting-wsgi-error-log](../../includes/web-sites-python-troubleshooting-wsgi-error-log.md)]

## <a name="next-steps"></a><span data-ttu-id="b1cea-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1cea-166">Next steps</span></span>
<span data-ttu-id="b1cea-167">For more information, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="b1cea-167">For more information, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="b1cea-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="b1cea-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b1cea-169">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="b1cea-169">No credit cards required; no commitments.</span></span>
> 
> 
