## Challenge 7: Visualizing in Power BI Desktop

Duration: 20 minutes

In this exercise, you will create visualizations in Power BI Desktop.

### Task 1: Obtain the JDBC connection string to your Azure Databricks cluster

Before you begin, you must first obtain the JDBC connection string to your Azure Databricks cluster.

1. In Azure Databricks, go to **Compute** and select your cluster.

2. On the cluster edit page, in the **Configuration** tab, scroll down to the bottom of the page, expand **Advanced Options**, then select the **JDBC/ODBC** tab.

3. On the **JDBC/ODBC** tab, copy and save the **Server Hostname (1)** and **HTTP Path (2)** to be used during the next task. You can use a text editor such as Notepad to keep the values for later use.

   ![An image of the JDBC URL with the necessary values for the new Power BI connection string selected.](media/databricks-power-bi-spark-information.png 'Construct Power BI connection string')

### Task 2: Connect to Azure Databricks using Power BI Desktop

1. If you did not already do so during the before the hands-on lab setup, download Power BI Desktop from <https://powerbi.microsoft.com/en-us/desktop/>.

2. When Power BI Desktop starts, you will need to enter your personal information or Sign in if you already have an account.

   ![The Power BI Desktop Welcome page displays prompting the user for personal details.](media/image177.png 'Power BI Desktop Welcome page')

3. Select Get data on the screen that is displayed next.

   ![On the Power BI Desktop Sign-in page, the Get data item is selected.](media/powerbi-getdata.png 'Power BI Desktop Sign in page')

4. Select **Azure Databricks** from the list of available data sources. You may enter `databricks` into the search field to find it faster.

   ![In the Get Data screen, Spark is selected from the list of available sources.](media/pbi-desktop-get-data.png 'Get Data page')

5. Select **Connect**.

6. On the next screen, you will be prompted for your Azure Databricks cluster information.

7. On the Azure Databricks connection information dialog, enter the following:

   - **Server Hostname (1)**: Paste the JDBC **Server Hostname (1)** value you copied in the previous task.
  
   - **HTTP Path (2)**: Paste the JDBC **HTTP Path** value you copied in the previous task.
  
   - **Data Connectivity mode**: Select **DirectQuery (3)** for the Data Connectivity mode. This option will offload query tasks to the Azure Databricks Spark cluster, providing near-real-time querying.
  
   ![The Spark form is populated with the Server, Protocol, and Data Connectivity mode specified in the previous steps.](media/pbi-desktop-connect-databricks.png 'Spark form')

8. Select **OK (4)**.

9. Select the **Username/Password** option from the credentials menu and then enter your credentials on the next screen as follows:

    - **User name (1)**: `token`

    - **Password (2)**: Remember that ADF Access token we generated for the Azure Data Factory notebook activity? Paste the same value here for the password.

    ![The Generate New Token form from when we generated the access token.](media/databricks-copy-token.png 'Copy generated token')

    !["token" is entered for the username, and the access token is pasted into the password field.](media/pbi-desktop-login.png 'Enter credentials')

10. Select **Connect (3)**.

11. In the Navigator dialog, check the box next to **flight_delays_summary (1)**, and select **Load (2)**.

    ![In the Navigator dialog box, in the pane under Display Options, the check box for flight_delays_summary is selected. In the pane, the table of flight delays summary information displays.](media/pbi-desktop-select-table-navigator.png 'Navigator dialog box')

### Task 3: Create Power BI report

1. Once the data finishes loading, you will see the fields appear on the far side of the Power BI Desktop client window.

   ![The Power BI Desktop Fields pane displays the fields from the flight_delays_summary table.](media/pbi-desktop-fields.png 'Power BI Desktop Fields')

2. From the Visualizations area, next to Fields, select the Globe icon to add a Map visualization to the report design surface.

   ![On the Power BI Desktop Visualizations palette, the globe icon is selected.](media/pbi-vis-map.png 'Power BI Desktop Visualizations palette')

3. With the Map visualization still selected, drag the **OriginLatLong** field to the **Location** field under Visualizations. Then Next, drag the **NumDelays** field to the **Size** field under Visualizations.

   ![In the Fields column, the checkboxes for NumDelays and OriginLatLong are selected. An arrow points from OriginLatLong in the Fields column to OriginLatLong in the Visualization's Location field. A second arrow points from NumDelays in the Fields column to NumDelays in the Visualization's Size field.](media/pbi-desktop-configure-map-vis.png 'Visualizations and Fields columns')

4. You should now see a map that looks similar to the following (resize and zoom on your map if necessary):

   ![On the Report design surface, a Map of the United States displays with varying-sized dots over different cities.](media/pbi-desktop-map-vis.png 'Report design surface')

5. Unselect the Map visualization by selecting the white space next to the map in the report area.

6. From the Visualizations area, select the **Stacked Column Chart** icon to add a bar chart visual to the report's design surface.

   ![The stacked column chart icon is selected on the Visualizations palette.](media/pbi-vis-stacked.png 'Visualizations palette')

7. With the Stacked Column Chart still selected, drag the **DayofMonth** field and drop it into the **Axis** field located under Visualizations.

8. Next, drag the **NumDelays** field over, and drop it into the **Value** field.

   ![In the Fields column, the checkboxes for NumDelays and DayofMonth are selected. An arrow points from NumDelays in the Fields column to NumDelays in the Visualization's Axis field. A second arrow points from DayofMonth in the Fields column to DayofMonth in the Visualization's Value field.](media/pbi-desktop-configure-stacked-vis.png 'Visualizations and Fields columns')

9. Grab the corner of the new Stacked Column Chart visual on the report design surface, and drag it out to make it as wide as the bottom of your report design surface. It should look something like the following.

   ![On the Report Design Surface, under the United States map with dots, a stacked bar chart displays.](media/pbi-desktop-stacked-vis.png 'Report Design Surface')

10. Unselect the Stacked Column Chart visual by selecting the white space next to the map on the design surface.

11. From the Visualizations area, select the Treemap icon to add this visualization to the report.

    ![On the Visualizations palette, the Treemap icon is selected.](media/pbi-vis-treemap.png 'Visualizations palette')

12. With the Treemap visualization selected, drag the **OriginAirportCode** field into the **Group** field under Visualizations.

13. Next, drag the **NumDelays** field over, and drop it into the **Values** field.

    ![In the Fields column, the checkboxes for NumDelays and OriginAirportcode are selected. An arrow points from NumDelays in the Fields column to NumDelays in the Visualization's Values field. A second arrow points from OriginAirportcode in the Fields column to OriginAirportcode in the Visualization's Group field.](media/pbi-desktop-config-treemap-vis.png 'Visualizations and Fields columns')

14. Grab the corner of the Treemap visual on the report design surface, and expand it to fill the area between the map and the side edge of the design surface. The report should now look similar to the following.

    ![The Report design surface now displays the map of the United States with dots, a stacked bar chart, and a Treeview.](media/pbi-desktop-full-report.png 'Report design surface')

15. You can cross filter any of the visualizations on the report by selecting one of the other visuals within the report, as shown below (This may take a few seconds to change as the data is loaded).

    ![The map on the Report design surface is now zoomed in on the northeast section of the United States, and the only dot on the map is on Chicago. In the Treeview, all cities except ORD are grayed out. In the stacked bar graph, each bar is now divided into a darker and a lighter color, with the darker color representing the airport.](media/pbi-desktop-full-report-filter.png 'Report design surface')

16. You can save the report by choosing Save from the File menu and entering a name and location for the file.

    ![The Power BI Save as window displays.](media/image197.png 'Power BI Save as window')