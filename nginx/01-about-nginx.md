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
- Load the ip address  in a browser you should see nginx home page.

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