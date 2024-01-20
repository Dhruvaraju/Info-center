- [What is nginx](#what-is-nginx)
  - [Installing nginx](#installing-nginx)
    - [On a Debian or ubuntu machine](#on-a-debian-or-ubuntu-machine)
    - [Installing on a RHEL / Centos](#installing-on-a-rhel--centos)
    - [Installation using source code](#installation-using-source-code)
      - [On Ubuntu](#on-ubuntu)
      - [On Centos](#on-centos)
  - [Adding nginx as a systemd service](#adding-nginx-as-a-systemd-service)

# What is nginx

#nginx

**NGINX** is open source software for web serving, reverse proxying, caching, load balancing, media streaming, and more. It started out as a web server designed for maximum performance and stability. In addition to its HTTP server capabilities, NGINX can also function as a proxy server for email (IMAP, POP3, and SMTP) and a reverse proxy and load balancer for HTTP, TCP, and UDP servers.

## Installing nginx

#nginx-installation

### On a Debian or ubuntu machine

- `apt-get update` to update the system
- use `apt-get install nginx` to install nginx
- On running install command nginx will be installed and started.
- To check if nginx is running `ps aux | grep nginx`
- Get the ip address of the machine using `ipconfig`
- Load the ip address in a browser you should see nginx home page.

```sh
dexter@dexter-vm:~$ ps aux | grep nginx
root       42420  0.0  0.3  55188 12144 ?        S    17:08   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data   42422  0.0  0.1  55860  5604 ?        S    17:08   0:00 nginx: worker process
www-data   42423  0.0  0.1  55860  5604 ?        S    17:08   0:00 nginx: worker process
dexter     42590  0.0  0.0   6480  2336 pts/0    S+   17:11   0:00 grep --color=auto nginx
```

### Installing on a RHEL / Centos

#nginx-centos

- `yum update` to update the repos
- `yum install nginx` to install nginx
- This will not start nginx.
- use `systemctl start nginx` to start nginx service
- to check status `systemctl status nginx`
- To check if nginx is running `ps aux | grep nginx`

- Details about nginx will be present in `/etc/nginx/nginx.conf` file.
- logs are located in the below mentioned location

#nginx-logs

```sh
access_log /var/log/nginx/access.log;
error_log /var/log/nginx/error.log;
```

> For streaming the logs use `tail -f <location_of_file>` example `tail -f /var/log/nginx/access.log`

### Installation using source code

- Navigate to nginx.org, navigate to download page.
- Identify the stable version and copy the link to download it, it will look something like https://nginx.org/download/nginx-1.25.3.tar.gz

#### On Ubuntu

- `apt-get update` to update packages
- To download the file use `wget` like `wget https://nginx.org/download/nginx-1.25.3.tar.gz`
- Extract it by using `tar -zxvf nginx-1.25.3.tar.gz`
- Navigate into the extracted folder to find a configure folder
- Execute it by using `./configure`, If the compiler is missing install it using `apt-get install build-essential`
- Try executing `./configure` if it fails requesting pcre library install the required libraries with `apt-get install libpcre3 libpcre3-dev zliblg zliblg-dev libssl-dev make`
- Now `./configure` will work but it will not have any configuration define
- Use the below command to configure location for different options like logs and conf

```sh
./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module
```

- Now a make file will be created use `make` and `make install` to install nginx
- To start it use `nginx`
- To check if nginx is running use `ps -ef | grep nginx`

#### On Centos

- `yum update` for updating packages
- To download the file use `wget` like `wget https://nginx.org/download/nginx-1.25.3.tar.gz`
- Extract it by using `tar -zxvf nginx-1.25.3.tar.gz`
- Navigate into the extracted folder to find a configure folder
- Execute it by using `./configure`, If the compiler is missing install it using `yum groupinstall "Development Tools`
- Try executing `./configure` if it fails requesting pcre library install the required libraries with `yum install pcre pcre-devel zlib zlib-devel openssl openssl-devel make`
- Now `./configure` will work but it will not have any configuration define
- Use the below command to configure location for different options like logs and conf

```sh
./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module
```

- Now a make file will be created use `make` and `make install` to install nginx
- To start it use `nginx`
- To check if nginx is running use `ps -ef | grep nginx`

## Adding nginx as a systemd service

- Search for nginx systemd init service, it can be found at https://www.nginx.com/resources/wiki/start/topics/examples/systemd/
- Create a file as `/lib/systemd/system/nginx.service`
- Add the following content

```sh
[Unit]
Description=The NGINX HTTP and reverse proxy server
After=syslog.target network-online.target remote-fs.target nss-lookup.target
Wants=network-online.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/bin/nginx -t
ExecStart=/usr/bin/nginx
ExecReload=/usr/bin/nginx -s reload
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

> Update the paths based the location nginx is installed.

Starting nginx service

```sh
systemctl start nginx
```

Stop nginx service

```sh
systemctl stop nginx
```

Restart nginx service

```sh
systemctl restart nginx
```

To get status of nginx

```sh
systemctl status nginx
```

To auto restart nginx service on system reboot and power shutdown

```sh
systemctl enable nginx
```
