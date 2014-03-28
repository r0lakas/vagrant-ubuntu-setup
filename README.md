vagrant-ubuntu-setup
====================

###Ubuntu 12.04 LTS 64bit | idiegtas per wubi

####v.2 ant svaraus naujo ubuntu

```js

cd ~/Desktop/
sudo apt-get update
sudo apt-get install openjdk-7-jdk
sudo apt-get install git git-core

// per software center isirasiau virtualboxa Ubuntu 12.04 (Precise Pangolin) 64bit

cd Downloads/
sudo chmod +x vagrant_1.5.1_x86_64.deb
sudo dpkg -i vagrant_1.5.1_x86_64.deb
vagrant -v

cd ~/Desktop/

//susigeneruojam ir prisidedam key
ssh-keygen
cat ~/.ssh/id_rsa.pub

git clone https://github.com/nfqakademija/vm.git //cia jusu repositorijos adresas
cd vm/
vagrant box add nfqakademija/wheezy wheezy.box
vagrant up

// gavau ntfs error: It appears your machine doesn't support NFS

vagrant halt
sudo apt-get install nfs-kernel-server
vagrant up

// gavau error: mount.nfs: access denied by server while mounting
// perkraunam kompa tikedamiesi, kad problema dings

cd ~/Desktop/vm/
vagrant up          // taip, dingo :)
vagrant provision

//auto hosts pridejimas
vagrant plugin install vagrant-hostsupdater 

vagrant ssh
cd /var/www/
composer update // vykdant sia cmd pirma karta berods gavau erora, tai perkroviau kompa

// kaskart vykdant composer update man luzdavo ties symfony (timeout)
// todel composeri reik leisti ne vagrante, bet isirasyti i ubuntu ir per ten updatint

cd ~/Desktop/vm/
sudo apt-get install php5-cli
php -r "readfile('https://getcomposer.org/installer');" | php
php composer.phar update

// kai papraso duomenu config/parameters.yml
// database_driver: pdo_mysql
// database_host: localhost
// database_name: foodrescue
// database_use: root
// database_password: root
// kitais atvejais spaudziam enter

vagrant ssh
cd /var/www/

//sukurs db
php app/console doctrine:database:create

chmod 777 app/cache
chmod 777 app/logs
chmod 777 app/config/parameters.yml

// web/app_dev.php uzkomentinam:
// || !in_array(@$_SERVER['REMOTE_ADDR'], array('127.0.0.1', 'fe80::1', '::1'))

// pridedam data
sudo pico /etc/php5/apache2/php.ini
ctrl+W timezone enter
date.timezone=UTC
ctrl+X y enter

// perkraunam apache
sudo /etc/init.d/apache2 restart

// puslapis veikia: http://projektas.dev/web/app_dev.php/ dabar einam gerti alaus :)


```

====================

####v.1 nepilnai veikiantis..


```js
=====================

//pradzia Dariaus, aciu jam :)
//terminnale:
cd ~/Desktop

//isirasom git
sudo apt-get install git git-core

//isirasom virtualbox [SITAS BLOGAI, todel veliau istrinsim ir isirasysim kita]
sudo apt-get install virtualbox

//prasisiunciam ir isirasom vagrant 1.5.1
sudo chmod +x vagrant_1.5.1_x86_64.deb
sudo dpkg -i vagrant_1.5.1_x86_64.deb

//clonuojam vm
git clone https://github.com/nfqakademija/vm.git
cd vm
vagrant box add nfqakademija/wheezy wheezy.box
vagrant up

* It appears your machine doesn't support NFS, or there is not an
adapter to enable NFS on this machine for Vagrant. Please verify
that `nfsd` is installed on your machine, and try again. If you're
on Windows, NFS isn't supported. If the problem persists, please
contact Vagrant support.

// jei ismete sita error. terminale vesti.
vagrant halt

sudo apt-get install nfs-kernel-server
vagrant plugin install vagrant-hostmanager
vagrant plugin install vagrant-box-updater
vagrant plugin install vagrant-hostsupdater

vagrant up

//sitoje vietoje pareina eroras:
No such file or directory - /home/darbukas/.vagrant.d/nfqakademija/wheezy.stat (Errno::ENOENT) 

//Simono “magic” :)
vagrant plugin update
vagrant plugin uninstall vagrant-box-updater //pasirodo nereikalingas
vagrant -v
vagrant plugin update

//ssh key generavimas, kuri pridedam I savo githubo profaila
ssh-keygen
cat ~/.ssh/id_rsa.pub

//parsipuciam savo team repositoriuma
mkdir Sites
cd Sites/
git clone git@github.com:nfqakademija/Food-rescue.git
cd Food-rescue/

//istrinam virtuablboxa (bloga versija)
//ir isirasom  Ubuntu 12.04 (Precise Pangolin) 64bit
//is cia: http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html?ssSourceSiteId=otnjp
sudo apt-get remove –purge virtualbox
sudo apt-get install -f
sudo apt-get autoremove
uname -a        //suzinoti reikiama versija

//irasom parsiusta virtualboxa
cd Downloads/
sudo dpkg -i virtualbox-4.3_4.3.8-92456 [Tab] // su siuo kodu kazkas nesuveike, tai irasinejom per software center
sudo apt-get install -f

cd Sites/Food-rescue/
vagrant up

//gavom errora (nepamenu koki), pratrynem machines kataloga ir perkrovem kompa
rm -rf .vagrant/machines/

//Musu repositorijoje..
vagrant up
vagrant provision

//su IP 192.168.63.29 puslapis pasiekiamas !

```
