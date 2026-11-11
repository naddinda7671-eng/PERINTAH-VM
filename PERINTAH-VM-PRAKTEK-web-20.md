ip link set enp0s3 up
ip addr add 192.168.20.2/29 dev enp0s3
ip route add default via 192.168.20.1
echo "nameserver 8.8.8.8" > /etc/resolv.conf
apt install iputils-ping -y
ping 8.8.8.8
ip a
apt update
apt install nano openssh-server -y
nano /etc/netplan/00-installer-config.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.20.2/29]
      routes:
        - to: default
          via: 192.168.20.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
netplan apply



Inatall apache
pt install apache2 php libapache2-mod-php php-mysql php-xml php-curl php-zip php-mbstring php-gd php-intl -y
Download & ekstrak moodle
cd /tmp
wget https://download.moodle.org/download.php/direct/stable404/moodle-latest-404.tgz
tar -xzvf moodle-latest-*.tgz -C /var/www/html/
Buat folder data moodle & atur izin akses
mkdir /var/moodledata
chown -R www-data:www-data /var/www/html/moodle /var/moodledata
chmod -R 777 /var/moodledata
systemctl restart apache2
