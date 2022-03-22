# b4x20220322
B4X實驗: APP如何連線到資料庫服務器(SQLServer/MySQL/SQLite),並示範讀取資料

B4X實驗: APP如何連線到資料庫服務器(SQLServer/MySQL/SQLite),並示範讀取資料
參考資料:
https://www.b4x.com/guides/B4XSQLiteDatabase/?page=1
https://www.b4x.com/android/forum/threads/jtds-jdbc-driver-with-standalone-package.133728/#content



1.微軟SQL Server Express LocalDB
https://docs.microsoft.com/zh-tw/sql/database-engine/configure-windows/sql-server-express-localdb?view=sql-server-ver15
https://devbricker.github.io/post/database/sql-server/sqlserverbasic2/

SQL Server Express Edition 2019(6M)
A.檔案很小.實際上它會上網下載檔案(565MB)
B.需要管理器 (650MB)
C.安裝過程失敗..重新來一次喔!!

Visual Studio 2013 版本以後推薦開發者使用 LocalDB 來做為開發時使用的 DB ，LocalDB 好處非常多
 
Sql Server資料庫的超級簡化版本：Sql Server LocalDB。


安裝前.最好把所有sqlserver移除掉
 LocalDB 最好不要安裝


#AdditionalJar: jtds-1.3.1.jar
	driver  = "net.sourceforge.jtds.jdbc.Driver"
	
	serverIP = "127.0.0.1"
	serverPort = "3307"
	serverDB = "test"
	jdbcUrl  = $"jdbc:mysql://${serverIP}/${serverDB}?characterEncoding=utf8&useSSL=false"$


#AdditionalJar:mssql-jdbc-9.4.1.jre11.jar
Sql1.Initialize("com.microsoft.sqlserver.jdbc.SQLServerDriver","jdbc:sqlserver://192.168.1.1:1433;user=sa;password=mypassword;databaseName=mydatabase;")


新增使用者登入
https://kanchengzxdfgcv.blogspot.com/2016/04/sqlserver-18456.html


用管理員改設定
sqlserver登入驗證
更改sa參數

用sa登入..新增資料庫 跟刪除 看看

好的，我應該對 DB 執行什麼操作才能從中獲取簡單的 Select 語句：
1- 在 Windows 10 上打開防火牆端口 1433。2-
在 SQL Server 2019 上啟用 TCP/IP 連接。3-
將集成安全性設置為 true。
4- 將 SQL Server 身份驗證修改為混合模式（Windows 和 SQL Server 2019）。
5- 使用用戶名和密碼創建新角色，然後將它們傳遞給 InitializeAsync。
?
畢竟這些程序仍然 Query : False ，Resultset 未初始化。
我排除了網絡和安全可能性，將內部 IP 替換為真實 IP，以避免移動 Android 設備在移動數據上，而筆記本電腦在工作網絡上。

https://www.b4x.com/android/forum/threads/how-to-use-jdts-or-jrdc-to-get-successful-connections-to-sql-server-2019-db.139011/#post-880885

2.MySQL 
Laragon 官網：https://laragon.org/download/亦可從gitHub下載
Download Laragon - Portable (38 MB)
https://www.kreaweb.be/laragon-update-apache/ 少了apache

https://www.apachelounge.com/download/
 
目錄為
D:\Software\laragon-portable\bin\apache\httpd-2.4.53-win64-VS16\bin


httpd.conf檔案內容改一下:
Define SRVROOT "C:/laragon/bin/apache/httpd-2.4.47-win64-VS16"

ServerRoot "C:/laragon/bin/apache/httpd-2.4.47-win64-VS16"
Listen 8080

IncludeOptional "D:/Software/laragon-portable/etc/apache2/alias/*.conf"
IncludeOptional "D:/Software/laragon-portable/etc/apache2/sites-enabled/*.conf"
Include "D:/Software/laragon-portable/etc/apache2/httpd-ssl.conf"
Include "D:/Software/laragon-portable/etc/apache2/mod_php.conf"


群輝NAS內建了...或者xampp(最後用這個)

下載下來先改密碼...ho123456789 phpmyadmin
https://ithelp.ithome.com.tw/articles/10216290
新增一個帳號sa.密碼ho123456789

3.SQLite








