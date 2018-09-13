<span data-ttu-id="3a3ff-101">Some packages may not install using pip when run on Azure.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="3a3ff-102">It may simply be that the package is not available on the Python Package Index.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-102">It may simply be that the package is not available on the Python Package Index.</span></span>  <span data-ttu-id="3a3ff-103">It could be that a compiler is required (a compiler is not available on the machine running the web app in Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="3a3ff-103">It could be that a compiler is required (a compiler is not available on the machine running the web app in Azure App Service).</span></span>

<span data-ttu-id="3a3ff-104">In this section, we'll look at ways to deal with this issue.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-104">In this section, we'll look at ways to deal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="3a3ff-105">Request wheels</span><span class="sxs-lookup"><span data-stu-id="3a3ff-105">Request wheels</span></span>
<span data-ttu-id="3a3ff-106">If the package installation requires a compiler, you should try contacting the package owner to request that wheels be made available for the package.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-106">If the package installation requires a compiler, you should try contacting the package owner to request that wheels be made available for the package.</span></span>

<span data-ttu-id="3a3ff-107">With the recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier to build packages that have native code for Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-107">With the recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier to build packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="3a3ff-108">Build wheels (requires Windows)</span><span class="sxs-lookup"><span data-stu-id="3a3ff-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="3a3ff-109">Note: When using this option, make sure to compile the package using a Python environment that matches the platform/architecture/version that is used on the web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span><span class="sxs-lookup"><span data-stu-id="3a3ff-109">Note: When using this option, make sure to compile the package using a Python environment that matches the platform/architecture/version that is used on the web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="3a3ff-110">If the package doesn't install because it requires a compiler, you can install the compiler on your local machine and build a wheel for the package, which you will then include in your repository.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-110">If the package doesn't install because it requires a compiler, you can install the compiler on your local machine and build a wheel for the package, which you will then include in your repository.</span></span>

<span data-ttu-id="3a3ff-111">Mac/Linux Users: If you don't have access to a Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how to create a VM on Azure.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-111">Mac/Linux Users: If you don't have access to a Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how to create a VM on Azure.</span></span>  <span data-ttu-id="3a3ff-112">You can use it to build the wheels, add them to the repository, and discard the VM if you like.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-112">You can use it to build the wheels, add them to the repository, and discard the VM if you like.</span></span> 

<span data-ttu-id="3a3ff-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="3a3ff-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="3a3ff-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="3a3ff-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="3a3ff-115">To build wheels, you'll need the wheel package:</span><span class="sxs-lookup"><span data-stu-id="3a3ff-115">To build wheels, you'll need the wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="3a3ff-116">You'll use `pip wheel` to compile a dependency:</span><span class="sxs-lookup"><span data-stu-id="3a3ff-116">You'll use `pip wheel` to compile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="3a3ff-117">This creates a .whl file in the \wheelhouse folder.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-117">This creates a .whl file in the \wheelhouse folder.</span></span>  <span data-ttu-id="3a3ff-118">Add the \wheelhouse folder and wheel files to your repository.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-118">Add the \wheelhouse folder and wheel files to your repository.</span></span>

<span data-ttu-id="3a3ff-119">Edit your requirements.txt to add the `--find-links` option at the top.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-119">Edit your requirements.txt to add the `--find-links` option at the top.</span></span> <span data-ttu-id="3a3ff-120">This tells pip to look for an exact match in the local folder before going to the python package index.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-120">This tells pip to look for an exact match in the local folder before going to the python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="3a3ff-121">If you want to include all your dependencies in the \wheelhouse folder and not use the python package index at all, you can force pip to ignore the package index by adding `--no-index` to the top of your requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-121">If you want to include all your dependencies in the \wheelhouse folder and not use the python package index at all, you can force pip to ignore the package index by adding `--no-index` to the top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="3a3ff-122">Customize installation</span><span class="sxs-lookup"><span data-stu-id="3a3ff-122">Customize installation</span></span>
<span data-ttu-id="3a3ff-123">You can customize the deployment script to install a package in the virtual environment using an alternate installer, such as easy\_install.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-123">You can customize the deployment script to install a package in the virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="3a3ff-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, to prevent pip from installing them.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, to prevent pip from installing them.</span></span>

<span data-ttu-id="3a3ff-125">Add this to the deployment script:</span><span class="sxs-lookup"><span data-stu-id="3a3ff-125">Add this to the deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="3a3ff-126">You may also be able to use easy\_install to install from an exe installer (some are zip compatible, so easy\_install supports them).</span><span class="sxs-lookup"><span data-stu-id="3a3ff-126">You may also be able to use easy\_install to install from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="3a3ff-127">Add the installer to your repository, and invoke easy\_install by passing the path to the executable.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-127">Add the installer to your repository, and invoke easy\_install by passing the path to the executable.</span></span>

<span data-ttu-id="3a3ff-128">Add this to the deployment script:</span><span class="sxs-lookup"><span data-stu-id="3a3ff-128">Add this to the deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-the-virtual-environment-in-the-repository-requires-windows"></a><span data-ttu-id="3a3ff-129">Include the virtual environment in the repository (requires Windows)</span><span class="sxs-lookup"><span data-stu-id="3a3ff-129">Include the virtual environment in the repository (requires Windows)</span></span>
<span data-ttu-id="3a3ff-130">Note: When using this option, make sure to use a virtual environment that matches the platform/architecture/version that is used on the web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span><span class="sxs-lookup"><span data-stu-id="3a3ff-130">Note: When using this option, make sure to use a virtual environment that matches the platform/architecture/version that is used on the web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="3a3ff-131">If you include the virtual environment in the repository, you can prevent the deployment script from doing virtual environment management on Azure by creating an empty file:</span><span class="sxs-lookup"><span data-stu-id="3a3ff-131">If you include the virtual environment in the repository, you can prevent the deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="3a3ff-132">We recommend that you delete the existing virtual environment on the app, to prevent leftover files from when the virtual environment was managed automatically.</span><span class="sxs-lookup"><span data-stu-id="3a3ff-132">We recommend that you delete the existing virtual environment on the app, to prevent leftover files from when the virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
