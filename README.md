vagrant-ubuntu-setup
====================

Ubuntu 12.04 LTS 64bit

```js
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
