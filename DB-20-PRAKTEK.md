ip link set enp0s3 up
ip addr add 192.168.20.3/29 dev enp0s3
ip route add default via 192.168.20.1
echo "nameserver 8.8.8.8" > /etc/resolv.conf
apt install iputils-ping -y
ping 8.8.8.8
ip a
apt install nano openssh-server -y
nano /etc/netplan/00-installer-config.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.20.3/29]
      routes:
        - to: default
          via: 192.168.20.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]


Install mariaDB
apt install mariadb-server -y
Amankan DB
mysql_secure_installation
Buat DB & User Moodle
mysql -u root -p

Perintah SQL:
CREATE DATABASE moodle DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'moodleuser'@'192.168.20.2' IDENTIFIED BY 'Password123!';
GRANT ALL PRIVILEGES ON moodle.* TO 'moodleuser'@'192.168.20.2';
FLUSH PRIVILEGES;
EXIT;

IZINKAN AKSES LUAR
nano /etc/mysql/mariadb.conf.d/50-server.cnf
CARI BARIS
bind-address = 127.0.0.1 ubah bind-address = 0.0.0.0 (simpan)
restrat:
systemctl restart mariadb
