  edit teks nano:
sudo nano /usr/local/bin/backup.sh
  teks nano
#!/bin/bash
DATE=$(date +%Y-%m-%d)
mkdir -p /backup
mysqldump -u root -pPassword123! moodle > /backup/moodle_db.sql
tar -cvf /backup/backup_$DATE.tar /etc/apache2 /backup/moodle_db.sql
rm /backup/moodle_db.sql

  jalankan:
sudo chmod +x /usr/local/bin/backup.sh
  cek hasil:
sudo /usr/local/bin/backup.sh
