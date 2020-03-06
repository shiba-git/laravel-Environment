# vagrant + centos7 + php73 + MySQL5.7 + laravel5.8 
  
フォルダ作成＆移動  
mkdir laravel-env   
cd laravel-env  

vagrantfile作成  
vagrant init  
  
vagrantfile変更  
config.vm.box = "centos7" //centosboxが追加してある前提  
config.vm.network "private_network", ip: "192.168.33.10" // コメントアウトを外す  
  
vagrant立ち上げ  
vagrant up  
  
vagrantにログイン  
vagrant ssh  
  
zip unzip wget gitインストール  
sudo yum install -y zip unzip wget git  
  
apacheインストール  
  sudo yum install -y httpd  
  
  サーバー起動時にApache起動  
  sudo systemctl enable httpd.service  
    
  Apache起動  
  sudo systemctl restart httpd.service  
    
  Apache起動確認  
  service httpd status  

PHPインストール  
  EPELリポジトリ  
  sudo yum install -y epel-release  
  
  remiリポジトリ  
  sudo yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm  
    
  sudo yum update -y //Errorが出た。   
    
  sudo vi /etc/yum.repos.d/epel.repo   
  baseURLのコメントアウトを外し、アクセス。  
  mirrorlist の URL はコメントアウト  
     
  sudo yum install -y --enablerepo=remi,remi-php73 php php-zip php-devel php-mbstring php-pdo php-xml php-bcmath php-mysqlnd  
    
composerのインストール  
  curl -sS https://getcomposer.org/installer | php  
  sudo mv composer.phar /usr/local/bin/composer  
  
Laravelのインストール  
  composer global require laravel/installer  
  
作成するディレクトリまで移動、権限付与  
cd /var/www/html   
sudo chmod 777 -R /var/www/html  
   
プロジェクトを作成  
composer create-project --prefer-dist laravel/laravel project  

ファイヤーウォール停止  
sudo systemctl stop firewalld  
  
動作確認  
php artisan serve --host 192.168.33.10 --port 8000  

MySQLをインストール  
  mariadbを削除  
  sudo yum remove mariadb-libs  
  rm -rf /var/lib/mysql/  
   
  sudo vi /etc/resolv.conf  
  nameserver: 9.9.9.9  
  
  sudo yum curl //以下のコマンドでエラーが出ないように  
  sudo rpm -ivh http://dev.mysql.com/get/mysql57-community-release-el7-7.noarch.rpm  
    
  sudo yum install -y mysql-community-server    
  
  MySQL起動  
  sudo systemctl start mysqld.service   
  MySQL自動起動  
  sudo systemctl enable mysqld.service  
  
  パスワード確認  
  sudo cat /var/log/mysqld.log | grep 'temporary password'  
  
  初期設定  
  mysql_secure_installation  
  
  ログイン  
  mysql -u root -p  
 
  mysql> create database mydb;    

  laravelとデータベースと連携  
  sudo vi .env  
  DB_CONNECTION=mysql  
  DB_HOST=127.0.0.1  
  DB_PORT=3306  
  DB_DATABASE=mydb  
  DB_USERNAME=root  
  DB_PASSWORD=password  
  
  連携確認のため、マイグレーション  
  php artisan migrate  
  
  mysql> use mydb;  
  mysql> show tables;  
  


  

https://qiita.com/nooboolean/items/ffcd6b2229f846f195ec
