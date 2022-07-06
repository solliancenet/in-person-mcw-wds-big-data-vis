## Challenge 5: Operationalize ML scoring with Azure Databricks and Data Factory

Duration: 20 minutes

In this exercise, you will extend the Data Factory to operationalize data scoring using the previously created machine learning model within an Azure Databricks notebook.

### Task 1: Create Azure Databricks Linked Service

1. Return to, or reopen the Author & Monitor page for your Azure Data Factory in a web browser, navigate to the Author view **(1)**, and select the `CopyOnPrem2AzurePipeline` pipeline **(2)**.

   ![Under Factory Resources, the CopyOnPrem2AzurePipeline pipeline is selected.](media/adf-ml-select-pipeline.png 'Select the ADF pipeline')

   >**Note**: You may need to rename your pipeline if you followed the steps above. Simply press the three dots next to the pipeline and select **Rename**. Use `CopyOnPrem2AzurePipeline` as the new pipeline name.

   ![Renaming the new Azure Data Factory Pipeline.](media/adf-pipeline-rename.png "Pipeline rename in ADF")

2. Once there, expand Databricks under Activities.

   ![Beneath Activities, the Databricks item is expanded.](media/adf-ml-expand-databricks-activity.png 'Expand Databricks Activity')

3. Drag the Notebook activity onto the design surface to the side of the Copy activity.

   ![The Notebook activity is dragged onto the design surface.](media/adf-ml-drag-notebook-activity.png 'Notebook on design surface')

4. Select the Notebook activity **(1)** on the design surface to display tabs containing its properties and settings at the bottom of the screen. On the **General (2)** tab, enter `BatchScore` into the **Name (3)** field.

   ![BatchScore is entered into the Name textbox under the General tab.](media/adf-ml-notebook-general.png 'Databricks Notebook General Tab')

5. Select the **Azure Databricks (1)** tab, and select **+ New (2)** next to the Databricks Linked service drop-down. Here, you will configure a new linked service that will serve as the connection to your Databricks cluster.

   ![In the Azure Databricks tab, the + New button is selected next to the Databricks Linked Service textbox.](media/adf-ml-settings-new-link.png 'Databricks Notebook Settings Tab')

6. On the New Linked Service dialog, enter the following:

   - **Name**: `AzureDatabricks`
  
   - **Connect via integration runtime**: Leave set to Default.
  
   - **Account selection method**: **From Azure subscription**
  
   - **Azure subscription**: Choose your Azure Subscription.
  
   - **Databricks workspace**: Pick your Databricks workspace to populate the Domain automatically.
  
   - **Select cluster**: **Existing interactive cluster**

   - **Access token**:  Paste your Personal Access Token (PAT) that you saved earlier.

   - **Choose from existing clusters**:  Select **lab** from the drop-down list.

   Once you have entered this information, select **Create**.

   ![The New linked service form is shown populated with the previously listed values.](media/adf-ml-databricks-service-settings.png 'Databricks Linked Service settings')

7. Switch back to Azure Databricks. Select **Workspace > Users > BigDataVis** in the menu **(1)**. Select the **Exercise 5 (2)** folder, then open notebook **01 Deploy for Batch Scoring (3)**. Examine the content, but _don't run any of the cells yet_.

    ![In the Azure Databricks workspaces, beneath BigDataVis, the Exercise 5 folder is selected. Beneath Exercise 5, the 01 Deploy for Batch Score notebook is selected.](media/databricks-workspace-create-folder.png 'Create folder')

8.  Replace **`STORAGE-ACCOUNT-NAME`** with the name of the blob storage account you copied in Exercise 1 into Cmd 4.

    ![Cmd 4 is shown. Storage account name placeholder is replaced with bigdatalabstore10.](media/databricks-storage-name.png 'Storage Account Name')

9.  Switch back to your Azure Data Factory screen. Select the **Settings (1)** tab, then browse **(2)** to your **Exercise 5/01 Deploy for Batch Score** notebook **(3)** into the Notebook path field.

    ![In the Azure Data Factory pipeline designer, with the Notebook activity selected, the Settings tab is the active tab. The Browse button is selected next to the Notebook path.](media/adf-ml-notebook-path.png 'Notebook path')

10. The final step is to connect the **Copy data** activity with the **Notebook** activity. Select the small green box on the side of the copy activity, and drag the arrow onto the Notebook activity on the design surface. What this means is that the copy activity has to complete processing and generate its files in your storage account before the Notebook activity runs, ensuring the files required by the BatchScore notebook are in place at the time of execution. Select **Publish All (1)**, then **Publish** the **CopyOnPrem2AzurePipeline**, after making the connection.

    ![In the Azure Data Factory pipeline designer. The Copy Data activity is attached to the Notebook activity.](media/adf-ml-connect-copy-to-notebook.png 'Attach the copy activity to the notebook')

### Task 2: Trigger workflow

1. Switch back to Azure Data Factory. Select your pipeline if it is not already opened.

2. Select **Trigger**, then **Trigger Now** located above the pipeline design surface.

   ![In the taskbar for the Azure Data Factory pipeline designer, Trigger is selected, and Trigger Now is selected from the drop-down options.](media/adf-ml-trigger-now.png 'Trigger Now')

3. Enter `3/1/2017` into the **windowStart (1)** parameter, then select **OK (2)**.

   ![The Pipeline Run form is displayed with the windowStart parameter set to 3/1/2017.](media/adf-ml-pipeline-run.png 'Pipeline Run')

4. Select **Monitor** in the menu. You will be able to see your pipeline activity in progress as well as the status of past runs.

   ![From the left menu in Azure Data Factory, Monitor is selected. The current status of the pipeline run is displayed in the table.](media/adf-ml-monitor.png 'Monitor')

   > **Note**: You may need to restart your Azure Databricks cluster if it has automatically terminated due to inactivity.