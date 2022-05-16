# Ubuntu 22.04 LTS
https://ubuntu.com/download/desktop

# SSH
## install openssh
```cmd
sudo apt-get install openssh-server
```

## check ssh status
```cmd
sudo service ssh status
```

# Frontend env
## install npm on ubuntu
```cmd
sudo apt-get install nodejs npm
```
## install Vue-CLI on ubuntu
```cmd
sudo npm install -g @vue/cli
```

# Backend env
## apt 建置 PHP/Laravel
## 安裝 Apache / 檢查安裝版本
```cmd
sudo apt install apache2
sudo apache2 -v
```
check with server ip
## 安裝 MySQL
```cmd
sudo apt install mysql-server
sudo mysql --version
```
## 安裝 PHP
```cmd
# 新增 ppa 來源
sudo apt-add-repository ppa:ondrej/php
sudo apt update

# 安裝 PHP 及相關擴充
sudo apt install php7.2 php7.2-common php7.2-cli php7.2-curl php7.2-gd php7.2-json php7.2-dev php7.2-pgsql php7.2-sqlite3 php7.2-gd php7.2-curl php7.2-memcached php7.2-imap php7.2-mysql php7.2-mbstring php7.2-xml php7.2-zip php7.2-bcmath php7.2-soap php7.2-intl php7.2-readline

# 安裝 Apache 的 PHP 模組
sudo apt install libapache2-mod-php7.2
```
## 下載/安裝 Composer
```cmd
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```
把 composer.phar 變成全域指令
```cmd
sudo mv composer.phar /usr/local/bin/composer
```
## 安裝 Laravel
建立新 Laravel 專案
```cmd
mkdir ~/Projects
cd ~/Projects
composer create-project laravel/laravel --prefer-dist
```
Laravel 在運行的時候，會將應用程式的 cache 及 log 寫入檔案，因此把資料夾權限開大
```cmd
chmod -R 777 storage
chmod -R 777 bootstrap/cache
```
## 建立/開啟虛擬站台

```cmd
sudo nano /etc/apache2/site-available/laravel.local.conf
# add
  <VirtualHost laravel.local:80>
      DocumentRoot "/home/shengyou/Projects/laravel/public"
      ServerAdmin laravel.local

      <Directory "/home/shengyou/Projects/laravel">
          Options All
          AllowOverride All
          Require all granted
      </Directory>
  </VirtualHost>
```
完成後要在 Apache 裡啟動這個站台，成功啟動後要重新載入 Apache 設定檔
```cmd
# 開啟站台
sudo a2ensite laravel.local

# 重新載入 Apache 設定檔
sudo systemctl reload apache2
```
## 設定 hosts
```cmd
sudo nano /etc/hosts
# add 
  127.0.0.1 laravel.local
```
each person can read

```cmd
cd ~/projects/laravel
sudo php artisan serve --host 192.168.0.228 --port 8081
```
## 安裝Vue3
```cmd
npm install --save vue@next && npm install --save-dev vue-loader@next
```
## 安裝Laravel freeze
```cmd
composer require laravel/breeze
php artisan breeze:install
```
npm install && npm run dev
# blender in Ubuntu
install with snap
```cmd
sudo snap install blender --classic
```
try it
```cmd
blender
```
# Docker env (failed) 
## install Docker on ubuntu / check status
```cmd
sudo apt-get install docker.io
service docker status
```
## search ubuntu on Docker / pull
```cmd
docker search ubuntu
docker pull ubuntu
```
## Laradock  
```cmd
sudo apt install docker-compose
```
## 將自己的帳號加到 docker 這個群組
```cmd
sudo usermod -aG docker Username
```
## Laravel
## 取得 Laradock 專案
```cmd 
git clone https://github.com/laradock/laradock.git Laradock
```

## 設定 Laradock
Laradock 提到環境設定檔供我們依需求客製化調整，請將先設定檔從範例樣板複製出
```cmd
cp .env.example .env
```

## 啟動 Laradock 
```cmd 
docker-compose up -d nginx mysql
```
nginx、mysql 這兩個容器會被建立外，也會同時啟動 php-fpm 及 workspace 這兩個容器。

## 建立/運行 Laravel 專案
Laravel 專案建立起來並在 Laradock 裡運行
### 設定 Laradock
~/Laradock/.env 檔案，設定 APPLICATION 參數內為 ~/Projects
```cmd
APPLICATION=~/Projects/
```
## 進入 workspace 容器
使用 Docker 這種虛擬化技術就是希望能把開發環境和工具都封裝在容器裡，也就是說本機端並沒有 PHP、Composer 等指令可以使用。
而 Laradock 在啟動時，有幫我們準備一個名為 workspace 的容器，只要進到這個容器裡面，就可以有 composer、artisan 這些指令可以使用。
```cmd
docker-compose exec workspace bash
```
登入後應該會發現工作目錄是在 /var/www 底下，而裡面的內容就是我們本機 ~/Projects 的內容。

## 建立 Laravel 專案
由於 /var/www 資料夾是本機和容器之間連結的資料夾，所以我們要在 /var/www 資料夾裡建立 Laravel 專案，這樣檔案才會一併同步到本地端工作機。

```cmd
composer create-project laravel/laravel --prefer-dist
```

## 建立站台
新建的專案設定成一個 Nginx 的虛擬站台。Laradock 已經提供數種 Nginx 的站台樣板，只要用 Laravel 的樣板複製一份即可
```cmd
cd ~/Laradock/nginx/sites
cp laravel.conf.example laravel.test.conf
```








