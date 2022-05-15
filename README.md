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











