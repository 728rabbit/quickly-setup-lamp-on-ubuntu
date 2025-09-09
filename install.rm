## 1️⃣ 更新系統

`sudo apt update && sudo apt upgrade -y` 

## 2️⃣ 安裝 Apache

`sudo apt install apache2 -y` 

安裝完成後檢查服務狀態：

`systemctl status apache2` 

如果看到 **active (running)**，就表示成功了。  
瀏覽器輸入 `http://localhost`，應該會看到 Apache2 Ubuntu 預設頁面。

## 3️⃣ 安裝 MySQL

`sudo apt install mysql-server -y` 

啟動 MySQL 安全設定：

`sudo mysql_secure_installation` 

-   設定 root 密碼（Ubuntu 預設是用 socket authentication，不一定需要）
    
-   移除匿名使用者
    
-   禁止 root 遠端登入
    
-   移除測試資料庫
    
-   重新載入權限表
    

登入 MySQL 測試：

`sudo mysql` 

或者（如果你給 root 設了密碼）：

`mysql -u root -p`


## 4️⃣ 安裝 PHP

Ubuntu 22.04 預設 PHP 8.1，你可以裝：

`sudo apt install php libapache2-mod-php php-mysql -y` 

這裡包含：

-   `php` → PHP 本體
    
-   `libapache2-mod-php` → 讓 Apache 支援 PHP
    
-   `php-mysql` → PHP 連接 MySQL 的驅動
    

檢查 PHP 版本：

`php -v`

## 5️⃣ 測試 PHP

建立一個測試檔案：

`sudo nano /var/www/html/info.php` 

內容輸入：

`<?php  phpinfo();` 

存檔後瀏覽 `http://localhost/info.php`  
會看到 PHP 資訊頁面。

----------

## 6️⃣（可選）安裝常用 PHP 擴展

`sudo apt install php-cli php-curl php-xml php-mbstring php-zip unzip -y` 

----------

✅ 到這裡你就有一個完整的 **Apache + PHP + MySQL** 環境。
