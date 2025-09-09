##**MySQL** 裡建立新使用者

## 1️⃣ 登入 MySQL

`sudo mysql` 

（如果你已經設了 root 密碼，用）

`mysql -u root -p` 

----------

## 2️⃣ 建立使用者

`CREATE  USER  'ken'@'localhost' IDENTIFIED BY  'MyPass123!';` 

📌 說明：

-   `'ken'` → 使用者名稱
    
-   `'localhost'` → 只能本機登入（安全性高）
    
-   `'%'` → 允許任何 IP 登入（常用於遠端連線）
    

例如：允許遠端登入

`CREATE  USER  'ken'@'%' IDENTIFIED BY  'MyPass123!';` 

----------

## 3️⃣ 賦予權限

給這個使用者某個資料庫的全部權限（例如 `testdb`）：

`GRANT  ALL PRIVILEGES ON testdb.*  TO  'ken'@'localhost';` 

如果要給所有資料庫權限（⚠️ 就跟 root 一樣強大）：

`GRANT  ALL PRIVILEGES ON  *.*  TO  'ken'@'localhost'  WITH  GRANT OPTION;` 

----------

## 4️⃣ 重新載入權限

`FLUSH PRIVILEGES;` 

----------

## 5️⃣ 測試登入

`mysql -u ken -p` 

----------

✨ 這樣就建立好一個新的 MySQL 使用者了。
