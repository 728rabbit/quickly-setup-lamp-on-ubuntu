## 在 Ubuntu MySQL 設定 root 密碼 的方法

## 方法一：透過 `mysql_secure_installation` 設定

安裝完 MySQL 後可以執行：

`sudo mysql_secure_installation` 

過程中會問：

-   要不要設定 root 密碼？（新版本有時不會問，要手動設定）
    
-   要不要刪掉匿名帳號？
    
-   禁止 root 遠端登入？
    
-   移除測試資料庫？
    

如果有出現設定 root 密碼的選項，照著輸入即可。

----------

## 方法二：手動修改 root 密碼

如果 `mysql_secure_installation` 沒有幫你設置密碼，可以這樣做：

1.  進入 MySQL（無密碼登入）
    

`sudo mysql` 

2.  切換到 `mysql` 資料庫
    

`USE mysql;` 

3.  修改 root 認證方式和密碼（假設密碼要設成 `MyNewPass123!`）：
    

`ALTER  USER  'root'@'localhost' IDENTIFIED WITH mysql_native_password BY  'MyNewPass123!';` 

4.  重新整理權限
    

`FLUSH PRIVILEGES;` 

5.  離開
    

`EXIT;` 

----------

## 方法三：檢查 root 使用的驗證方式

執行：

`sudo mysql -e "SELECT user, host, plugin FROM mysql.user WHERE user='root';"` 

如果看到 `plugin` 欄位是 **auth_socket**，表示只能用 `sudo mysql` 進入。  
如果是 **mysql_native_password**，就可以用密碼登入：

`mysql -u root -p`
