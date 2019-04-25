# Installer Jenkins sur un serveur Apache2 avec webhooks github

Tutoriel détaillé de l’installation

## Installation


```bash

$ wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -

$ echo 'deb https://pkg.jenkins.io/debian-stable binary/' | tee -a /etc/apt/sources.list

$ sudo apt update

$ sudo apt install jenkins -y

$ systemctl start jenkins

$ systemctl enable jenkins

$ netstat -plntu

$ sudo apt install apache2 -y

$ a2enmod proxy

$ a2enmod proxy_http

$ cd /etc/apache2/sites-available/

$ emacs jenkins.conf

```

## Configuration Apache2

La configuration de jenkins.conf

```
<Virtualhost *:80>
    ServerName        IP DE VOTRE SERVEUR
    ProxyRequests     Off
    ProxyPreserveHost On
    AllowEncodedSlashes NoDecode
 
    <Proxy http://localhost:8080/*>
      Order deny,allow
      Allow from all
    </Proxy>
 
    ProxyPass         /  http://localhost:8080/ nocanon
    ProxyPassReverse  /  http://localhost:8080/
    ProxyPassReverse  /  IP DE VOTRE SERVEUR
</Virtualhost>
```

## Suite de l'installation


```bash

$ a2ensite jenkins

$ systemctl restart apache2

$ systemctl restart jenkins

$ ufw allow ssh

$ ufw allow http

$ ufw allow https

$ ufw enable
```