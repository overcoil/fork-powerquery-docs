---
title: Azure Databricks Power Query connector
description: Provides basic information and prerequisites for using Power Query's Azure Databricks connector.
author: bezhan-msft

ms.topic: conceptual
ms.date: 8/4/2022
ms.author: bezhan
LocalizationGroup: reference
---

# Azure Databricks

>[!NOTE]
>The following connector article is provided by Databricks, the owner of this connector and a member of the Microsoft Power Query Connector Certification Program. If you have questions regarding the content of this article or have changes you would like to see made to this article, visit the Databricks website and use the support channels there.

## Summary

| Item | Description |
| ---- | ----------- |
| Release State | General Availability |
| Products | Power BI (Datasets)<br/>Power BI (Dataflows) |
| Authentication Types Supported | Azure Active Directory<br/>Organizational Account<br/>Personal Access Token |

## Capabilities supported

* Import
* DirectQuery (Power BI only)

## Connect to Databricks (AWS, Azure or GCP) from Power Query Desktop

To connect to Databricks from Power Query Desktop, take the following steps:

1. In the Get Data experience, search for **Databricks** to shortlist the Databricks connector, **Azure Databricks**. Use the **Azure Databricks** connector for all Databricks SQL Warehouse data unless you've been instructed otherwise by your Databricks rep.

    ![Get Data from Databricks Cloud.](./media/databricksazure/get-data-dbc.png)

2. Provide the **Server hostname** and **HTTP Path** for your Databricks SQL Warehouse. Refer to [Configure the Databricks ODBC and JDBC drivers](/azure/databricks/integrations/bi/jdbc-odbc-bi) for instructions to look up your "Server hostname" and "HTTP Path". Enter this information accordingly. You can optionally supply a default catalog and/or database under **Advanced options**. Select **OK** to continue.

    ![Specify your Databricks SQL Warehouse.](./media/databricksazure/azdbc-sql-endpoint.png)

3. Provide your credentials to authenticate with your Databricks SQL Warehouse. There are three options for credentials:

    * Username / Password (useable for AWS or GCP). This option isn't available if your organization/account uses 2FA/MFA.
    * Personal Access Token (useable for AWS, Azure or GCP). Refer to [Personal access tokens](/azure/databricks/sql/user/security/personal-access-tokens) for instructions on generating a Personal Access Token (PAT).
    * Azure Active Directory (useable only for Azure). Sign in to your organizational account using the browser popup.

      ![Specify an appropriate token.](./media/databricksazure/azdbc-pat.png)

    > [!NOTE]
    > Once you enter your credentials for a particular Databricks SQL Warehouse, Power BI Desktop caches and reuses those same credentials in subsequent connection attempts. You can modify those credentials by going to **File > Options and settings > Data source settings**. More information: [Change the authentication method](../ConnectorAuthentication.md#change-the-authentication-method)

4. Once you successfully connect, the **Navigator** shows the data available to you on the cluster. You can choose either **Transform Data** to transform the data using Power Query or **Load** to load the data in Power Query Desktop.

    ![Image of Power Query navigator loading Databricks Cloud data to desktop app.](./media/databricksazure/navigator-with-filter.png)

## Connect to Databricks data from Power Query Online

To connect to Databricks from Power Query Online, take the following steps:

1. In the Get Data experience, select the **Database** category. (Refer to [Creating a dataflow](/power-bi/transform-model/dataflows/dataflows-create) for instructions.) Shortlist the available Databricks connectors with the search box. Use the **Azure Databricks** connector for all Databricks SQL Warehouse data unless you've been instructed otherwise by your Databricks rep.  

    ![Image of the Databricks connectors.](./media/databricksazure/filtered-connectors.png)

2. Enter the **Server hostname** and **HTTP Path** for your Databricks SQL Warehouse. Refer to [Configure the Databricks ODBC and JDBC drivers](/azure/databricks/integrations/bi/jdbc-odbc-bi) for instructions to look up your "Server hostname" and "HTTP Path". You can optionally supply a default catalog and/or database under **Advanced options**.

    ![Connection Settings and Credentials.](./media/databricksazure/azconnect-setting-cred.png)

3. Provide your credentials to authenticate with your Databricks SQL Warehouse. There are three options for credentials:

    * Username / Password (useable for AWS or GCP). This option isn't available if your organization/account uses 2FA/MFA.
    * Account Key (useable for AWS, Azure or GCP). Refer to [Personal access tokens](/azure/databricks/sql/user/security/personal-access-tokens) for instructions on generating a Personal Access Token (PAT).
    * Azure Active Directory (useable only for Azure). Sign in to your organizational account using the browser popup.

4. Once you successfully connect, the **Navigator** appears and displays the data available on the server. Select your data in the navigator. Then select **Next** to transform the data in Power Query.

    ![Image of Power Query navigator loading Databricks Cloud data to online app.](./media/databricksazure/pq-choose-data.png)


## Known Issues

This section describes limitations or considerations of the Azure Databricks connector.

### Proxy Setup

TODO: lorem ipsum

Create a driver setting file as follows (which requires administrative access):
1. Navigate to PowerBI's private copy of the Spark ODBC driver. This is located typically at ``C:\Program Files\Microsoft Power BI Desktop\bin\ODBC Drivers\Simba Spark ODBC Driver`` for 64-bit PowerBI Desktop. 
2. Create a text file at this location using Notepad with the name ``microsoft.sparkodbc.ini`` with the following content:
    ```
    [Driver]
    CheckCertRevocation=0
    ```
3. Restart PowerBI Desktop.

### Long Running Query timeout in Azure AD environment

### 

## Troubleshooting

### ODBC Driver Log File

To generate log files for the ODBC driver (which requires administrative access):
1. Navigate to PowerBI's private copy of the Spark ODBC driver. This is located typically at ``C:\Program Files\Microsoft Power BI Desktop\bin\ODBC Drivers\Simba Spark ODBC Driver`` for 64-bit PowerBI Desktop. (Note this setting applies to PowerBI's Spark driver and not to any other that may be installed in the system.)
2. Create a text file at this location using Notepad with the name ``microsoft.sparkodbc.ini`` with the following content:
    ```
    [Driver]
    LogLevel=6
    LogPath=c:\Logging\PBI-Spark
    ```
  
    Here, the log level has been set to 6 (``LOG_TRACE``) which is the most detailed/verbose. Log files will be saved to a directory ``c:\Logging\PBI-Spark``. See [here](http://simba.wpengine.com/products/Spark/doc/ODBC_InstallGuide/win/content/odbc/options/loglevel.htm) for details.
3. Create the directory ``c:\Logging\PBI-Spark``.
4. Restart PowerBI Desktop.

