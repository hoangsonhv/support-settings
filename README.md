
# Một số câu lệnh hữu ích :3

# Cài đặt Mysql trên Centos7

 **Cập nhật hệ thống:**
- sudo yum update

**Cài MySQL repositories:**

- wget http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm

**Cài đặt MySQL packages:** 
- sudo rpm -Uvh mysql57-community-release-el7-9.noarch.rpm

**Cài đặt mysql:**
- sudo yum install mysql-server

**Nếu lỗi không Complete! thì chạy:** 
- rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
- sudo yum update
- sudo yum install mysql-server

**Khởi động mysql:** 
- sudo systemctl start mysqld

**Dừng mysql:**
- sudo systemctl stop mysqld

**Kiểm tra trang thái hoạt động:**
- sudo systemctl status mysqld

#
# Đổi mật khẩu khi cài đặt mysql

**Lấy mật khẩu root tạm thời khi cài:** 
- sudo grep 'password' /var/log/mysqld.log

**Sau đó đổi mật khẩu:** 
- sudo mysql_secure_installation
- Sau đó điền mật khẩu tạm thời 
- Rồi điền mật khẩu mới
- Bấm y hoàn tất quá trình.

#
# Đổi mật khẩu user trong mysql

- mysql -u root -p 
- Điền password
- USE mysql;
- SET PASSWORD FOR 'name-user'@'host-name' = PASSWORD('password-user-new');

#
# Import Database

**Nhập dữu liệu:**
- mysql -p -u username database_name < file.sql

**Xuất dữ liệu:**
- mysqldump -u user_name -p[database_name] > dbname.sql

#
# Tạo User

**Tạo User:** 
- CREATE USER 'username'@'localhost' IDENTIFIED BY 'password'

**Xóa User:** 
- DROP USER 'username'@'ip_address';

**Danh sách User:** 
- SELECT User, Host FROM mysql.user;

**Gán quyền cho user:** 
- GRANT ALL PRIVILEGES ON name_database.* TO 'user_name'@'ip_address' WITH GRANT OPTION;
- Sau đó: FLUSH PRIVILEGES;

**Người dùng hiện tại:** 
- select user();

#
# Kiểm tra tường lửa

**Kiểm tra trạng thái:**
- firewall-cmd --get-active-zones

**Mở cổng 80:**
- firewall-cmd --zone=public --add-port=80/tcp --permanent

**Reload firewall:** 
- firewall-cmd --reload

#
# Cài đặt PHP trên Centos 7

**Sử dụng Remi repository để cài đặt PHP 7:**
- sudo yum install epel-release yum-utils -y
- sudo yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y

**Kích hoạt kho lưu trữ Remi PHP 7:**
- sudo yum-config-manager --enable remi-php7x

**Cài đặt PHP 7 và một số modules PHP:**
- sudo yum -y install php php-ldap php-zip php-embedded php-cli php-mysql php-common php-gd php-xml php-mbstring php-mcrypt php-pdo php-soap php-json php-simplexml php-process php-curl php-bcmath php-snmp php-pspell php-gmp php-intl php-imap perl-LWP-Protocol-https php-pear-Net-SMTP php-enchant php-pear php-devel php-zlib php-xmlrpc php-tidy php-opcache php-cli php-pecl-zip unzip gcc

**Chạy máy chủ apache:** 
- sudo systemctl restart httpd

#
# Giải nén/nén file trong Centos

**Giải nén file Zip trong Centos7:** 
- unzip file.zip

**Nén thành file zip:** 
- zip -r tên.zip tên

#
# Kết nối ssh

**Kết nối ssh lên server:**
- ssh user@ip_server

**Coppy file/folder Local lên server Server:**
- scp -r ~/path_folder_local/ user@ip_server:/path_folder_server/

**Coppy file/folder từ Server về Local:**
- scp -r user@ip_server:/path_folder_server/  ~/path_folder_local/

**Danh sách các lệnh trong win:**
- Get-Alias

#
# Backup DB Centos

**Tạo thư mục backup_db:**
- sudo mkdir /var/db/backup_db

**Cấp quyền thực thi:**
- sudo chown $(whoami):$(whoami) /var/db/backup_db

**Tạo file .sh để chứa câu lệnh thực thi:**
- touch /var/db/backup_db/backupDatabase.sh

**Nội dung file backupDatabase.sh:**
- mysqldump -u [username] –p[password] [database_name] > /path_to_[database_name].sql

**Format nội dung file backupDatabase.sh theo ngày tháng:**
- Mdate=“$(date +“%Y-%m-%d”)”
- mysqldump -u [username] –p[password] [database_name] > /path_to_[database_name].$Mdate.sql

**Sao lưu tự động:**
- Mở crontab: 
    - sudo vi /etc/crontab
- Thêm dòng lệnh ở cuối file:
  - root /var/db/backup_db/backupDatabase.sh
- Kiểm tra ngày giờ hiện tại:
  - date

#
# Lỗi không connect được mysql

**Lỗi :
mysqli::real_connect(): (HY000/2002): No connection could be made because the target machine actively refused it**
- Vào thư mục xampp\mysql\data xóa tất cả file để lại thư mục sau đó chạy lại mysql ở xampp

#
# Lỗi npm không run dev

**Cài đặt node && npm sau đó:**
- npm install --save --legacy-peer-deps
- npm install
- npm run dev