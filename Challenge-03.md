## Challenge 3: Setup Azure Data Factory

Duration: 20 minutes

In this exercise, you will create a baseline environment for Azure Data Factory development to further operationalize data movement and processing. You will create a Data Factory service and then install the Data Management Gateway, which is the agent that facilitates data movement from on-premises to Microsoft Azure.

### Task 1: Download and stage data to be processed

1. Open a web browser.

2. Download the AdventureWorks sample data from <http://bit.ly/2zi4Sqa>. If you are having trouble downloading the file, a zip file called FlightsAndWeather.zip is included in the lab-files folders.

   >**Note**: If you are using the optional VM provisioned in the Before the HOL document, ensure that you download and extract the data on the VM.

3. Extract it to a new folder called **C:\\Data**.

### Task 2: Install and configure Azure Data Factory Integration Runtime on your machine

1. To download the latest version of Azure Data Factory Integration Runtime, go to <https://www.microsoft.com/en-us/download/details.aspx?id=39717>.

   >**Note**: If you are using the optional VM provisioned in the Before the HOL document, ensure that you install the IR on the VM.

2. Select Download, then choose the download you want from the next screen.

   ![Under Choose the download you want, the latest version MSI file is selected.](media/download-ir.png 'Choose the download you want section')

3. Run the installer once downloaded.

4. When you see the following screen, select Next.

   ![The Welcome page in the Microsoft Integration Runtime Setup Wizard displays. A language drop-down list is shown, and the Next button is selected.](media/image114.png 'Microsoft Integration Runtime Setup Wizard')

5. Check the box to accept the terms and select Next.

   ![On the End-User License Agreement page, the check box to accept the license agreement is selected, as is the Next button.](media/image115.png 'End-User License Agreement page')

6. Accept the default Destination Folder and select Next.

   ![On the Destination folder page, the destination folder is set to C:\Program Files\Microsoft Integration Runtime\ and the Next button is selected.](media/image116.png 'Destination folder page')

7. Choose Install to complete the installation.

   ![On the Ready to install Microsoft Integration Runtime page, the Install button is selected.](media/image117.png 'Ready to install page')

8. Select Finish once the installation has been completed.

   ![On the Completed the Microsoft Integration Runtime Setup Wizard page, the Finish button is selected.](media/image118.png 'Completed the Wizard page')

9. After selecting Finish, the following screen will appear. Keep it open for now. You will come back to this screen once the Data Factory in Azure has been provisioned and obtain the gateway key to connect Data Factory to this "on-premises" server.

   ![The Microsoft Integration Runtime Configuration Manager, Register Integration Runtime dialog displays.](media/ir-self-hosted-registration-screen.png 'Register Integration Runtime page')

### Task 3: Configure Azure Data Factory

1. Launch a new browser window, and navigate to the Azure portal (<https://portal.azure.com>). Once prompted, log in with your Microsoft Azure credentials. If prompted, choose whether your account is an organization account or a Microsoft account. This will be based on which account was used to provision your Azure subscription used for this lab.

2. From the side menu in the Azure portal, choose **Resource groups**, then enter your resource group name into the filter box, and select it from the list.

3. Next, select your Azure Data Factory service from the list.

   ![Azure Portal Resource Listing page is shown. Azure Data Factory resource is highlighted.](media/select-azure-datafactory.png 'Azure Data Factory')

4. On the Data Factory Overview screen, select **Open Azure Data Factory Studio**.

   ![In the Azure Data Factory resource screen, Overview is selected from the left menu. The Open Azure Data Factory Studio tile is selected.](media/adf-author-monitor.png 'Open Azure Data Factory Studio')

5. A new page will open in another tab or new window. Within the Azure Data Factory site, select **Manage** on the menu.

   ![In the left menu, the Manage icon is selected.](media/adf-home-manage-link.png 'Manage link on ADF home page')

6. Now, select **Integration runtimes (1)** in the menu, then select **+ New (2)**.

   ![The Integration runtimes menu item is selected, and the + New button is selected.](media/adf-new-ir.png 'Steps to create a new Integration Runtime connection')

7. In the Integration Runtime Setup blade that appears, select **Azure, Self-Hosted (1)**, then select **Continue (2)**.

   ![In the Integration runtime setup options, select Azure, Self-Hosted. Perform data flows, data movement, and dispatch activities to external compute.The Continue button is selected.](media/adf-ir-setup-1.png 'Integration Runtime Setup step 1')

8. Select **Self-Hosted (1)** then select **Continue (2)**.

   ![In the Network environment selected, Self-Hosted is selected, and the Continue button is highlighted.](media/adf-ir-setup-2.png 'Integration Runtime Setup step 2')

9. Enter a **Name (1)**, such as bigdatagateway-\[initials\], and select **Create (2)**.

   ![In the Integration runtime setup form, the Name textbox is populated with the value defined above.](media/adf-ir-setup-3.png 'Integration Runtime Setup step 3')

10. Under Option 2: Manual setup, copy the Key1 authentication key value by selecting the Copy button, then select **Close**.

    ![Beneath Option 2: Manual setup, the Key 1 textbox, and copy button are highlighted.](media/adf-ir-setup-4.png 'Integration Runtime Setup step 4')

    > **WARNING**: Don't close the current screen or browser session.

11. Paste the **Key1 (1)** value into the box in the middle of the Microsoft Integration Runtime Configuration Manager screen.

    ![The Microsoft Integration Runtime Configuration Manager Register Integration Runtime page displays with the Key1 value pasted into the textbox. A green checkmark next to the textbox denotes it's a valid key.](media/adf-ir-vm-register.png 'Microsoft Integration Runtime Configuration Manager')

12. Select **Register (2)**.

13. It can take up to a minute or two to register. If it takes more than a couple of minutes, and the screen does not respond or returns an error message, close the screen by selecting the **Cancel** button.

14. The following screen will be New Integration Runtime (Self-hosted) Node. Select **Finish**.

    ![The Microsoft Integration Runtime Configuration Manager New Integration Runtime (Self-hosted) Node page displays with a Finish button.](media/adf-ir-self-hosted-node.png 'Microsoft Integration Runtime Configuration Manager')

15. Depending on your version of the Integration Runtime, you will be asked to specify a backup file. Select **Skip** and **OK**.

   ![The Integration Runtime Configuration Manager requests a backup credentials. Configuring backup settings is unncessary for this lab.](media/skip_ir_backup.png 'Skipping Integration Runtime backup settings')

16. You will then get a screen with a confirmation message. Select the **Launch Configuration Manager** button to view the connection details.

    ![The Microsoft Integration Runtime Configuration Manager Indicates the Integration Runtime (Self-hosted) node has been successfully registered. The Launch Configuration Manager button is highlighted.](media/adf-ir-launch-config-manager.png 'Microsoft Integration Runtime Configuration Manager')

    ![The Microsoft Integration Runtime Configuration Manager indicates the Self-hosted note is connected to the cloud service.](media/adf-ir-config-manager.png 'Microsoft Integration Runtime Configuration Manager')

17. You can now return to the Azure Data Factory page and view the Integration Runtime you just configured. You may need to select **Refresh** to view the Running status for the IR.

    ![In the Connections tab in Azure Data Factory, the Integration runtimes tab is selected, and the integration runtime bigdatagateway-initials is shown in the list.](media/adf-ir-running.png 'Integration Runtime in running state')

18. Select the Azure Data Factory Overview button on the menu. Leave this open for the next exercise.

    ![The Azure Data Factory Overview button is selected from the left menu.](media/adf-overview.png 'ADF Overview')