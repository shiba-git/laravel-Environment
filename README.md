# vagrant + centos7 + php73 + laravel 環境構築
  
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
  
 
  
  
  
  

