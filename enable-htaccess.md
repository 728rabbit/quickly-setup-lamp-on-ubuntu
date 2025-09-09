## 1️⃣ 編輯 Apache 設定檔

假設你網站在 `/var/www/html`，編輯 Apache 的預設設定：

`sudo nano /etc/apache2/sites-available/000-default.conf` 

找到 `<Directory /var/www/>` 或新增一段：

`<Directory /var/www/html>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>` 

> **重要**：`AllowOverride All` 才能讓 `.htaccess` 生效。

----------

## 2️⃣ 啟用 Apache rewrite 模組（常用於 .htaccess）

`sudo a2enmod rewrite` 

----------

## 3️⃣ 重新啟動 Apache

`sudo systemctl restart apache2` 

----------

## 4️⃣ 測試 .htaccess

在 `/var/www/html/` 建立一個簡單 `.htaccess`：

`# 禁止所有訪問 test.txt
<Files "test.txt">
    Require all denied
</Files>` 

建立 `test.txt`，然後瀏覽器訪問，如果被拒絕就表示 .htaccess 已生效。
