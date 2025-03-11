# Redmine

**Redmine** یک ابزار مدیریت پروژه **متن‌باز** و **چند-پلتفرمی** است که از **سیستم ردیابی اشکال، ویکی داخلی، گانت چارت، و سیستم مدیریت وظایف** پشتیبانی می‌کند.

## ویژگی‌ها
- **مدیریت پروژه‌ها و وظایف**
- **سیستم ردیابی مشکلات و اشکالات**
- **ویکی داخلی برای مستندسازی**
- **تقویم و نمودار گانت برای برنامه‌ریزی پروژه**
- **پشتیبانی از چندین پروژه همزمان**
- **سیستم احراز هویت و مدیریت کاربران**
- **توسعه‌پذیری از طریق افزونه‌ها و API**

## نصب و راه‌اندازی در Debian

### پیش‌نیازها
- **Ruby 2.5+**
- **Bundler**
- **MariaDB یا PostgreSQL**
- **Apache/Nginx + Passenger**

### مراحل نصب
#### 1. به‌روزرسانی بسته‌ها و نصب Ruby و Bundler
```sh
sudo apt update && sudo apt upgrade -y
sudo apt install -y ruby-full build-essential zlib1g-dev
```

#### 2. نصب MariaDB و تنظیم پایگاه داده
```sh
sudo apt install -y mariadb-server mariadb-client
sudo mysql_secure_installation
sudo mysql -u root -p
```
```sql
CREATE DATABASE redmine CHARACTER SET utf8mb4;
CREATE USER 'redmine'@'localhost' IDENTIFIED BY 'redmine_password';
GRANT ALL PRIVILEGES ON redmine.* TO 'redmine'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

#### 3. دریافت کد منبع و تنظیم محیط
```sh
cd /opt
sudo git clone https://github.com/redmine/redmine.git
cd redmine
sudo cp config/database.yml.example config/database.yml
```
در فایل `config/database.yml` اطلاعات پایگاه داده را ویرایش کنید.

#### 4. نصب وابستگی‌های Ruby و راه‌اندازی Redmine
```sh
sudo gem install bundler
bundle install --without development test
```

#### 5. اجرای مهاجرت پایگاه داده و راه‌اندازی Redmine
```sh
bundle exec rake db:migrate RAILS_ENV=production
bundle exec rake redmine:load_default_data RAILS_ENV=production
```

#### 6. اجرای سرور Redmine
```sh
bundle exec rails server -e production
```
اکنون می‌توانید از طریق **http://localhost:3000** به Redmine دسترسی داشته باشید.

## مستندات
برای مطالعه راهنمای کامل، به [Redmine Docs](https://www.redmine.org/projects/redmine/wiki) مراجعه کنید.

## مشارکت در توسعه
ما از همکاری شما استقبال می‌کنیم! لطفاً مخزن را **Fork** کرده و درخواست **Pull Request** ارسال کنید.

## مجوز
Redmine تحت **مجوز GPL v2** منتشر شده است. برای اطلاعات بیشتر، به فایل LICENSE مراجعه کنید.
