# 🧾 Commands Used in WAF Home Lab

```bash
##############################
# 🖥️ UBUNTU SERVER (TARGET)
##############################

# 🔧 System Preparation
sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get install -y net-tools openssl git curl

# 🌐 Apache & LAMP Stack Setup
sudo apt-get install -y apache2 php php-mysql mysql-server
sudo systemctl start apache2
sudo systemctl enable apache2

# 🗄️ MySQL Setup for DVWA
sudo mysql -u root -p

CREATE DATABASE dvwa;
CREATE USER 'dvwa_user'@'localhost' IDENTIFIED BY 'p@ssw0rd';
GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;

# 🧪 DVWA Installation
cd /var/www/html
sudo git clone https://github.com/digininja/DVWA.git
sudo chown -R www-data:www-data DVWA
sudo chmod -R 755 DVWA

# 🔐 SSL Certificate Generation (OpenSSL)
sudo mkdir /etc/ssl/dvwa

sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/dvwa/dvwa.key \
-out /etc/ssl/dvwa/dvwa.crt

# 🌍 DNS Mapping
sudo nano /etc/hosts
# Add:
# <your-server-ip> webserver.thesocialdork

# 🛡️ SafeLine WAF Installation
bash -c "$(curl -fsSLk https://waf.chaitin.com/release/latest/manager.sh)" -- --en

# 🔐 Authentication Setup (via WAF UI)
# Created login credentials and enabled access control

# 🚫 Custom Deny Rules (via WAF UI)
# Configured rules to block suspicious IPs and patterns


##############################
# 🐉 KALI LINUX (ATTACKER)
##############################

# 🌐 Access DVWA Application
# Open browser and go to:
# https://webserver.thesocialdork/

# 🧪 SQL Injection Attack
# Enter payload in DVWA:
' OR '1'='1

# ⚡ HTTP Flood Attack Simulation
ab -n 200 -c 20 https://webserver.thesocialdork/


##############################
# 📊 VERIFICATION
##############################

# Checked SafeLine WAF dashboard
# Observed blocked requests (~20–25%)
# Verified SQL injection detection
# Observed rate limiting during HTTP flood
```
