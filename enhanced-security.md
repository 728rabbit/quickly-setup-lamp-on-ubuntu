
在 Ubuntu 上部署 **LAMP（Linux + Apache + MySQL + PHP）** 時，增強安全性非常重要。下面我幫你整理成 **操作性強、適合初學者到中級使用者**的步驟：

----------

## 1️⃣ 系統層安全

1.  **更新系統**
    
`sudo apt update && sudo apt upgrade -y` 

確保所有套件都有最新安全更新。

2.  **建立非 root 用戶**  
    不要直接用 root 操作服務，使用普通用戶加 `sudo`。
    
3.  **防火牆**  
    使用 UFW 限制開放端口： 

`sudo ufw enable` 
`sudo ufw allow 22/tcp # SSH`  
`sudo ufw allow 80/tcp # HTTP` 
`sudo ufw allow 443/tcp # HTTPS`
`sudo ufw status` 

----------

## 2️⃣ Apache 層安全

1.  **隱藏 Apache 版本與 OS**  
    編輯 `/etc/apache2/conf-available/security.conf`：
    
`ServerTokens Prod`
`ServerSignature Off` 

2.  **啟用 HTTPS**
    
-   透過 Certbot 申請免費 SSL/TLS：
    
`sudo apt install certbot python3-certbot-apache -y`
`sudo certbot --apache` 

3.  **禁用不必要的模組**
    
`sudo apache2ctl -M`
`sudo a2dismod status autoindex` 

4.  **限制 .htaccess**
    
-   僅在需要的資料夾啟用 `AllowOverride All`，全域禁用。
    
----------

## 3️⃣ PHP 層安全

編輯 php.ini（位置通常 `/etc/php/8.1/apache2/php.ini`）：

`expose_php = Off  ; 不暴露 PHP 版本`  
`display_errors = Off  ; 生產環境不顯示錯誤`
`log_errors = On`
`file_uploads = On` 
`upload_max_filesize = 50M` 
`post_max_size = 50M` 
`max_execution_time = 30` 

-   **禁用危險函數**：
    

`disable_functions = exec,passthru,shell_exec,system,proc_open,popen,curl_exec,curl_multi_exec,parse_ini_file,show_source` 

----------

## 4️⃣ MySQL 層安全

1.  **安全安裝**
    

`sudo mysql_secure_installation` 

2.  **不要用 root 遠程連線**
    
3.  **為應用建立專用用戶**，僅授權需要的資料庫與操作權限：
    

`CREATE  USER  'appuser'@'localhost' IDENTIFIED BY  'StrongPass123!'; GRANT  SELECT,INSERT,UPDATE,DELETE  ON myapp.*  TO  'appuser'@'localhost';
FLUSH PRIVILEGES;` 

----------

## 5️⃣ 文件與目錄權限

`sudo chown -R www-data:www-data /var/www/html`
`sudo find /var/www/html -type d -exec  chmod 755 {} \`
`sudo find /var/www/html -type f -exec  chmod 644 {} \`

-   目錄 755，檔案 644
    
-   不要給 777，除非特別需求
    
----------

## 6️⃣ 日誌與監控

1.  開啟 Apache 與 MySQL 日誌，定期檢查 `/var/log/apache2/` 與 `/var/log/mysql/`
    
2.  安裝 fail2ban 防止暴力登入攻擊：
    

`sudo apt install fail2ban -y` 

----------

## 7️⃣ 其他建議

-   定期備份資料庫與網站
    
-   使用強密碼並定期更換
    
-   使用安全的 SSH key 登入，禁用密碼登入
    
-   對公開網頁使用 WAF（Web Application Firewall，例如 Cloudflare）
