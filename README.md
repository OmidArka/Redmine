# Redmine

ردمین (Redmine) یک نرم‌افزار مدیریت پروژه و رهگیری اشکال است که قابلیت‌های بسیاری از جمله پشتیبانی از چندین پروژه، امکانات مدیریتی، و سیستم کنترل نسخه را ارائه می‌دهد. این نرم‌افزار تحت وب بوده و به‌طور گسترده برای تیم‌ها و سازمان‌ها در سراسر دنیا برای مدیریت پروژه‌ها، تخصیص وظایف، و پیگیری پیشرفت استفاده می‌شود.

ویژگی‌ها:

    پشتیبانی از چندین پروژه: امکان مدیریت پروژه‌های مختلف به‌طور همزمان.
    سیستم پیگیری مشکلات: ارائه سیستم قوی برای پیگیری و مدیریت مشکلات (Issues).
    کنترل نسخه: یکپارچگی با سیستم‌های کنترل نسخه مانند Git و Subversion.
    مدیریت وظایف: تعریف وظایف و تخصیص آنها به اعضای تیم.
    گزارش‌گیری: گزارش‌های پیشرفته برای تحلیل پیشرفت پروژه.
    پشتیبانی از Agile: پشتیبانی از متدولوژی‌های Agile مانند Scrum و Kanban.
    دسترسی به فایل‌ها: آپلود و مدیریت فایل‌های پروژه.

مقایسه با سایر نرم‌افزارها:

    Jira: اگرچه Jira امکانات مشابهی دارد، اما Redmine به‌خاطر کد باز بودن و انعطاف‌پذیری بیشتر، یک گزینه مناسب‌تر برای تیم‌های کوچک و متوسط است. همچنین، Redmine به راحتی قابل سفارشی‌سازی است.
    Trello: در حالی که Trello برای تیم‌های کوچک و کارهای ساده بسیار مفید است، Redmine برای پروژه‌های پیچیده‌تر با نیاز به پیگیری پیشرفته‌تر و یکپارچگی با سایر سیستم‌ها مناسب‌تر است.






Redmine is a web-based project management and issue tracking software that offers a wide range of features, including multi-project support, administrative capabilities, and version control integration. It is widely used by teams and organizations around the world for managing projects, assigning tasks, and tracking progress.

Features:

    Multi-Project Support: Manage multiple projects simultaneously.
    Issue Tracking: A robust system for tracking and managing issues.
    Version Control Integration: Seamless integration with version control systems like Git and Subversion.
    Task Management: Define tasks and assign them to team members.
    Reporting: Advanced reporting tools for project progress analysis.
    Agile Support: Supports Agile methodologies like Scrum and Kanban.
    File Access: Upload and manage project files.

Comparison with Other Software:

    Jira: While Jira offers similar functionality, Redmine is a more flexible and cost-effective solution for small to medium teams due to its open-source nature. Redmine also offers more customization options.
    Trello: While Trello is great for smaller teams and simple tasks, Redmine is better suited for complex projects that require advanced tracking and integration with other systems.


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
