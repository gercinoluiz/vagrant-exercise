$install_mysql = <<-SCRIPT


apt-get update

debconf-set-selections <<< 'mysql-server mysql-server/root_password 123456 root'
debconf-set-selections <<< 'mysql-server mysql-server/root_password_again 123456 root'



apt-get install -y mysql-server mysql-client

# Allow External Connections on your MySQL Service
sudo sed -i -e 's/bind-addres/#bind-address/g' /etc/mysql/mysql.conf.d/mysqld.cnf
sudo sed -i -e 's/skip-external-locking/#skip-external-locking/g' /etc/mysql/mysql.conf.d/mysqld.cnf
mysql -u root -p root -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root'; FLUSH privileges;"
sudo service mysql restart

# create client database
mysql -u root -proot -e "CREATE DATABASE myDB;"

SCRIPT




# you're doing.
Vagrant.configure("2") do |config|
  # 
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 3306, host: 3306

  config.vm.provision "Install IntellijIDEA", privileged: true, type: "shell", inline: $install_mysql
end
