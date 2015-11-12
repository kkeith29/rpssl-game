# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
	config.vm.box = "scotch/box"
	config.vm.network "private_network", ip: "192.168.33.10"
	$script = <<SCRIPT
sudo sed -i 's|^;date.timezone =$|date.timezone = America/Chicago|' /etc/php5/cli/php.ini
sudo curl -LsS http://symfony.com/installer -o /usr/local/bin/symfony
sudo chmod a+x /usr/local/bin/symfony
sudo touch /etc/mysql/conf.d/charset.cnf
echo "[mysqld]
collation-server     = utf8mb4_general_ci
character-set-server = utf8mb4

" | sudo tee /etc/mysql/conf.d/charset.cnf
SCRIPT
	config.vm.provision "shell", inline: $script
	config.vm.synced_folder ".", "/var/www", owner: "www-data", group: "www-data", :mount_options => ["dmode=777", "fmode=666"]
end