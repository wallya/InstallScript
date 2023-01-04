# [ERP](https://www.citcot.com "citcot's Homepage") Install Script

This script is based on the install script from André Schenkels (https://github.com/aschenkels-ictstudio/openerp-install-scripts)
but goes a bit further and has been improved. This script will also give you the ability to define an xmlrpc_port in the .conf file that is generated under /etc/
This script can be safely used in a multi-erp code base server because the default erp port is changed BEFORE the erp is started.

## Installing Nginx
If you set the parameter ```INSTALL_NGINX``` to ```True``` you should also configure workers. Without workers you will probably get connection loss issues. Look at [the deployment guide from erp](https://www.citcot.com/documentation/15.0/setup/deploy.html) on how to configure workers.

## Installation procedure

##### 1. Download the script:
```
sudo wget https://raw.githubusercontent.com/Yenthe666/InstallScript/15.0/erp_install.sh
```
##### 2. Modify the parameters as you wish.
There are a few things you can configure, this is the most used list:<br/>
```OE_USER``` will be the username for the system user.<br/>
```GENERATE_RANDOM_PASSWORD``` if this is set to ```True``` the script will generate a random password, if set to ```False```we'll set the password that is configured in ```OE_SUPERADMIN```. By default the value is ```True``` and the script will generate a random and secure password.<br/>
```INSTALL_WKHTMLTOPDF``` set to ```False``` if you do not want to install Wkhtmltopdf, if you want to install it you should set it to ```True```.<br/>
```OE_PORT``` is the port where erp should run on, for example 8069.<br/>
```OE_VERSION``` is the erp version to install, for example ```15.0``` for erp V15.<br/>
```IS_ENTERPRISE``` will install the Enterprise version on top of ```15.0``` if you set it to ```True```, set it to ```False``` if you want the community version of erp 15.<br/>
```OE_SUPERADMIN``` is the master password for this erp installation.<br/>
```INSTALL_NGINX``` is set to ```False``` by default. Set this to ```True``` if you want to install Nginx.<br/>
```WEBSITE_NAME``` Set the website name here for nginx configuration<br/>
```ENABLE_SSL``` Set this to ```True``` to install [certbot](https://github.com/certbot/certbot) and configure nginx with https using a free Let's Encrypted certificate<br/>
```ADMIN_EMAIL``` Email is needed to register for Let's Encrypt registration. Replace the default placeholder with an email of your organisation.<br/>
```INSTALL_NGINX``` and ```ENABLE_SSL``` must be set to ```True``` and the placeholder in ```ADMIN_EMAIL``` must be replaced with a valid email address for certbot installation<br/>
  _By enabling SSL though Let's Encrypt you agree to the following [policies](https://www.eff.org/code/privacy/policy)_ <br/>

#### 3. Make the script executable
```
sudo chmod +x erp_install.sh
```
##### 4. Execute the script:
```
sudo ./erp_install.sh
```

## Where should I host erp?
There are plenty of great services that offer good hosting. The script has been tested with a few major players such as [Google Cloud](https://cloud.google.com/), [Hetzner](https://www.hetzner.com/), [Amazon AWS](https://aws.amazon.com/) and [DigitalOcean](https://www.digitalocean.com/products/droplets/).
If you'd like you can use my [DigitalOcean referral link](https://m.do.co/c/d605cc420682) which gives you a 100$ voucher for free for the first 60 days.

## Minimal server requirements
While technically you can run an erp instance on 1GB (1024MB) of RAM it is absolutely not advised. A Linux instance typically uses 300MB-500MB and the rest has to be split among erp, postgreSQL and others. If you install an erp you should make sure to use at least 2GB of RAM. This script might fail with less resources too.
There are known issues on DigitalOcean for example where the installation crashes on 1GB RAM machines. See https://github.com/Yenthe666/InstallScript/issues/243

