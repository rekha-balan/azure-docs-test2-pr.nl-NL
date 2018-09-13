<span data-ttu-id="c6a9c-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span><span class="sxs-lookup"><span data-stu-id="c6a9c-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="c6a9c-102">requirements.txt file in the root folder</span><span class="sxs-lookup"><span data-stu-id="c6a9c-102">requirements.txt file in the root folder</span></span>
* <span data-ttu-id="c6a9c-103">any .py file in the root folder OR a runtime.txt that specifies python</span><span class="sxs-lookup"><span data-stu-id="c6a9c-103">any .py file in the root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="c6a9c-104">When that's the case, it will use a Python specific deployment script, which performs the standard synchronization of files, as well as additional Python operations such as:</span><span class="sxs-lookup"><span data-stu-id="c6a9c-104">When that's the case, it will use a Python specific deployment script, which performs the standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="c6a9c-105">Automatic management of virtual environment</span><span class="sxs-lookup"><span data-stu-id="c6a9c-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="c6a9c-106">Installation of packages listed in requirements.txt using pip</span><span class="sxs-lookup"><span data-stu-id="c6a9c-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="c6a9c-107">Creation of the appropriate web.config based on the selected Python version.</span><span class="sxs-lookup"><span data-stu-id="c6a9c-107">Creation of the appropriate web.config based on the selected Python version.</span></span>
* <span data-ttu-id="c6a9c-108">Collect static files for Django applications</span><span class="sxs-lookup"><span data-stu-id="c6a9c-108">Collect static files for Django applications</span></span>

<span data-ttu-id="c6a9c-109">You can control certain aspects of the default deployment steps without having to customize the script.</span><span class="sxs-lookup"><span data-stu-id="c6a9c-109">You can control certain aspects of the default deployment steps without having to customize the script.</span></span>

<span data-ttu-id="c6a9c-110">If you want to skip all Python specific deployment steps, you can create this empty file:</span><span class="sxs-lookup"><span data-stu-id="c6a9c-110">If you want to skip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="c6a9c-111">If you want to skip collection of static files for your Django application:</span><span class="sxs-lookup"><span data-stu-id="c6a9c-111">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango 

<span data-ttu-id="c6a9c-112">For more control over deployment, you can override the default deployment script by creating the following files:</span><span class="sxs-lookup"><span data-stu-id="c6a9c-112">For more control over deployment, you can override the default deployment script by creating the following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="c6a9c-113">You can use the [Azure command-line interface][Azure command-line interface] to create the files.</span><span class="sxs-lookup"><span data-stu-id="c6a9c-113">You can use the [Azure command-line interface][Azure command-line interface] to create the files.</span></span>  <span data-ttu-id="c6a9c-114">Use this command from your project folder:</span><span class="sxs-lookup"><span data-stu-id="c6a9c-114">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="c6a9c-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span><span class="sxs-lookup"><span data-stu-id="c6a9c-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="c6a9c-116">It is identical to the one you create with the command above.</span><span class="sxs-lookup"><span data-stu-id="c6a9c-116">It is identical to the one you create with the command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
