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








