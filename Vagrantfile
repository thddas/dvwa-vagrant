$script = <<-'SCRIPT'
    PHP_CONF='/etc/php/*/apache2/php.ini'
    DVWA_CONF='/var/www/html/config/config.inc.php'

    # Install requirements
    echo '--> Installing requirements and DVWA ...'
    apt-get update -y && apt-get install -y git htop net-tools
    apt-get install -y apache2 mariadb-server php php-mysqli php-gd libapache2-mod-php
    
    # Install DVWA
    rm -rf /var/www/html
    git clone https://github.com/digininja/DVWA.git /var/www/html
    cp /var/www/html/config/config.inc.php.dist $DVWA_CONF

    # Database configuration
    echo "--> Configuring database ..."
    mysql -e "create database dvwa;"
    mysql -e "create user dvwa@localhost identified by 'p@ssw0rd';"
    mysql -e "grant all on dvwa.* to dvwa@localhost;"
    mysql -e "flush privileges;"
        
    # PHP configuration
    echo 'Configuring PHP ...'
    sed -i 's/allow_url_include = Off/allow_url_include = On/' $PHP_CONF
    
    # DVWA configuration
    echo '--> Configuring DVWA ...'
    sed -i "s/recaptcha_public_key' ]  = ''/recaptcha_public_key' ] = 'insecurekey'/" $DVWA_CONF
    sed -i "s/recaptcha_private_key' ] = ''/recaptcha_private_key' ] = 'insecurekey'/" $DVWA_CONF
    # set security_level to low
    sed -i "s/'impossible'/'low'/" $DVWA_CONF

    chown -R www-data: /var/www/html/hackable/uploads
    chown -R www-data: /var/www/html/external/phpids/0.6/lib/IDS/tmp/phpids_log.txt
    chown -R www-data: /var/www/html/config
    
    systemctl restart apache2

    echo '--> DVWA successfully installed!'
SCRIPT

Vagrant.configure(2) do |config|
    config.vm.box = "debian/buster64"
    config.vm.box_check_update = false

    config.vm.network "private_network", ip: "192.168.50.50"

    config.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = "1024"
    end

    config.vm.provision "shell", inline: $script
end
