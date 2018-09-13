## <a name="using-azure-portal"></a>Using Azure portal
1. Select the VM you wish to redeploy, and click the 'Redeploy' button in the 'Settings' blade. Scroll down to see the **Support and Troubleshooting** section that contains the 'Redeploy' button as in the following example:
   
    ![Azure VM blade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-redeploy-to-new-node/vmoverview.png)
2. To confirm the operation, click the 'Redeploy' button:
   
    ![Redeploy a VM blade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-redeploy-to-new-node/redeployvm.png)
3. The **Status** of the VM changes to *Updating* as the VM prepares to redeploy, as in the following example:
   
    ![VM updating](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-redeploy-to-new-node/vmupdating.png)
4. The **Status** then changes to *Starting* as the VM boots up on a new Azure host, as in the following example:
   
    ![VM starting](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-redeploy-to-new-node/vmstarting.png)
5. After the VM finishes the boot process, the **Status** then returns to *Running*, indicating the VM has been successfully redeployed:
   
    ![VM running](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-redeploy-to-new-node/vmrunning.png)






