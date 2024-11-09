* sudo apt update

* sudo apt-get install -y apt-transport-https aspnetcore-runtime-8.0

* sudo apt-get install unzip -y

* sudo useradd -d /var/lib/nopCommerce -m -p nop -s /bin/sh nop

* # mkdir /tmp/nopCommerce


* # cd /tmp/nopCommerce


* sudo wget -P /var/lib/nopCommerce https://github.com/nopSolutions/nopCommerce/releases/download/release-4.70.5/nopCommerce_4.70.5_NoSource_linux_x64.zip

* sudo unzip nopCommerce_4.70.5_NoSource_linux_x64.zip

* sudo mkdir bin  at home dir
* sudo mkdir logs  at home dir

* sudo mv /tmp/nopCommerce /var/lib/nopCommerce
* sudo chown -R nop:nop /var/lib/nopCommerce

* sudo chown nop:nop nopCommerce/
* sudo vi  /usr/lib/systemd/system/nopCommerce.service for default .service

* # sudo /etc/systemd/system/nopCommerce.service  for custom service

```
[Unit]
Description= nopCommerce app running on ubuntu

[Service]
WorkingDirectory=/var/lib/nopCommerce
ExecStart=/usr/bin/dotnet /var/lib/nopCommerce/Nop.Web.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=nopCommerce-example
User=nop 
Environment= ASPNETCORE_URLS=http://0.0.0.0:5000
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
```
* sudo systemctl daemon-reload
* sudo systemctl enable nopCommerce.service
* sudo systemctl start nopCommerce.service