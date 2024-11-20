---
layout: post
title: "[Sql Native Client] Named Pipes Provide: Could not open a connection to SQL SERVER [2]"
date:   2022-06-18
tags: [database, python]
comments: true
author: Jerry8964
---



Summary:　上記エラーの調査及び対応方法。

## 背景

Windows system, remote SQL-Server. 

Can access by SSMS but when access from python code by SQL Server Native Client, got `[Sql Native Client] Named Pipes Provide: Could not open a connection to SQL SERVER [2]`

Only a few PC happens, others can.



## Trouble Shooting

1. Check that you can ping the SQL Server.

   > Just ping the server in windows command line. 
   >
   > `ping server_name or IP address`

2. If the SQL-Server is running. 

   > In this case, yes. it's running perfectly.

3. Check that the SQL Server Browser service is running

   > Command `sc query sqlbrowser`

   Set from SQL Server Configuration Manager.

   <img src="https://github.com/jerry8964/jerry8964.github.io/blob/main/images/SqlServerConfigurationManager.jpg?raw=true" style="zoom:90%;" />

4. If you are using the correct SQL Server Instance name.

   > In this case , yes. SQL Server instance name is set in setting file. Everyone use the same setting file.
   >
   > so if part of them can and the others can't , that not setting file's fault.

5. If you can find  the SQL Server

   > Use command `sqlcmd -L`
   >
   > if you can see the server name is list up, that means SQL Server Browser is running.

6. If TCP/IP and Named Pipes is enabled.

   > Open SQL Server Configuration Manager and check the SQL Server Network Configuration protocols. You should enable Named Pipes and TCP/IP protocol.

   Open SQL Server Configuration in Start Menu.

   <img src="https://github.com/jerry8964/jerry8964.github.io/blob/main/images/SqlServerConfigurationManagerInStartMenu.jpg?raw=true" style="zoom:80%;" />

   Right Click on TCP/IP >> Click on Enable

7. Check that allow remote connections for this server is enabled

   > Check to see if allow remote connections for this server is enabled. In SSMS, right click on the instance name and select Properties. Go to the Connections tab and make sure **Allow remote connections to this server** is checked. If you need to make a change, you must restart the SQL Server instance to apply the change.
   >
   > The settings below are equivalent to the settings in the image above.
   >
   > ```sql
   > exec sp_configure "remote access", 1          -- 0 on, 1 off
   > exec sp_configure "remote query timeout", 600 -- seconds
   > exec sp_configure "remote proc trans", 0      -- 0 on, 1 off
   > ```

   Right click on the server node and select Properties.

   <img src="https://github.com/jerry8964/jerry8964.github.io/blob/main/images/SqlServerProperty.jpg?raw=true" style="zoom:80%;" />

   Go to Left Tab of Connections and check “Allow remote connections to this server”

   <img src="https://github.com/jerry8964/jerry8964.github.io/blob/main/images/AllowRemoteConnection.jpg?raw=true" style="zoom:80%;" />

8. Check the port number that SQL Server is using

   >  Locally connect to SQL Server and check the error log for the port entry. You can execute XP_READERRORLOG procedure to read the errors or use SSMS by going to Management > SQL Server Logs and select the Current log. Scroll to the bottom which will be the first entries in the error log and look for entries similar to below that shows Named Pipes and TCP/IP are enabled and the port used for TCP/IP which is 1433 in this case.

9. Check that the firewall is not blocking access to SQL Server

   Go to Control Panel >> Windows Firewall >> Change Settings >> Exceptions >> Add Port. 

   <img src="https://github.com/jerry8964/jerry8964.github.io/blob/main/images/WindowsFirewall.JPG?raw=true" style="zoom:90%;" />

   <img src="https://github.com/jerry8964/jerry8964.github.io/blob/main/images/WindowsFirewallSettings.jpg?raw=true" style="zoom:90%;" />

   Make the following entries in popup “Add a Port” and click OK.
   **Name : SQL
   Port Number: 1433
   Protocol: Select TCP**

   ![](https://github.com/jerry8964/jerry8964.github.io/blob/main/images/AddaPort.jpg?raw=true)

   <img src="https://github.com/jerry8964/jerry8964.github.io/blob/main/images/AddPortResult.jpg?raw=true" style="zoom:90%;" />

   > - Click on **Add Port...** and enter the port number and name.
   >
   > - Click on **Add Program...** to add the SQL Server Browser service. Here you need to get the browser service executable path, normally it is located at C:\Program Files\Microsoft SQL Server\90\Shared location for SQL 2005 or similar for other versions of SQL Server. Browse the location and add the SQLBrowser.exe in the exception list.
   >
   >   

10. Check that the Service Principal Name has been registered

    > If you are able to connect to SQL Server by physically logging on to the server, but unable to connect from a client computer then execute the below query in a query window to check the SPN.
    >
    > ```sql
    > -- run this command to see if SPN is not found
    > EXEC xp_readerrorlog 0,1,"could not register the Service Principal Name",Null
    > ```
    >
    > 

## 参照資料

[https://support.arcserve.com/s/article/202869675?language=en_US](https://support.arcserve.com/s/article/202869675?language=en_US)

[https://www.mssqltips.com/sqlservertip/2340/resolving-could-not-open-a-connection-to-sql-server-errors/](https://www.mssqltips.com/sqlservertip/2340/resolving-could-not-open-a-connection-to-sql-server-errors/)



## その他

