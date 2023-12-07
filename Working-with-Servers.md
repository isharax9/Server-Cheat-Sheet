# Working with Servers

- getting out the DB dumb from Server
    - go to the server
    - look what are the current running web servers. by listening the port number(mainly we are using nginx or Apache web servers)
    
    ```php
    lsof -i:80
    ```
    
    - cd /etc/nginx/sites-enabled/
        
        The command **`cd /etc/nginx/sites-enabled/`** is not code; it is a Unix/Linux command that changes the current working directory to **`/etc/nginx/sites-enabled/`**. This directory is typically used in Nginx web server configurations to store symbolic links to configuration files for enabled sites.
        
        Now, let's break down the path and its significance:
        
        1. **`/etc`**: This is the standard location for configuration files and settings on Unix/Linux systems. It stands for "et cetera" and contains system-wide configuration files.
        2. **`/nginx`**: This is the main directory for the Nginx web server. It contains various subdirectories and configuration files related to Nginx.
        3. **`/sites-enabled`**: This directory is used to store symbolic links to configuration files for sites that are enabled. In Nginx, the configuration files for different sites are often organized in separate files. The **`sites-enabled`** directory contains symbolic links to these site configuration files.
        
        When you run **`cd /etc/nginx/sites-enabled/`**, you are navigating to the **`sites-enabled`** directory. Once you are in this directory, you might find symbolic links to various Nginx configuration files. Each symbolic link in this directory points to a corresponding configuration file located in the **`/etc/nginx/sites-available/`** directory.
        
        The typical workflow is as follows:
        
        - Configuration files for different sites are stored in the **`/etc/nginx/sites-available/`** directory.
        - Symbolic links to the configuration files of the enabled sites are placed in the **`/etc/nginx/sites-enabled/`** directory.
        - Nginx reads the configuration from the files in **`sites-enabled`** when it starts or reloads its configuration.
        
        This structure allows for easy management of Nginx configurations, especially when dealing with multiple sites on a single server.
        
        ```php
        cd /etc/nginx/sites-enabled/
        ```
        
    - Full code here
        
        ```php
        Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-148-generic x86_64)
        
         * Documentation:  https://help.ubuntu.com
         * Management:     https://landscape.canonical.com
         * Support:        https://ubuntu.com/advantage
        
          System information as of Mon Dec  4 06:37:53 UTC 2023
        
          System load:                      0.0
          Usage of /:                       51.5% of 48.27GB
          Memory usage:                     18%
          Swap usage:                       0%
          Processes:                        184
          Users logged in:                  0
          IPv4 address for br-ae4366b1b690: 172.28.0.1
          IPv4 address for br-ebbff40042a9: 172.20.0.1
          IPv4 address for docker0:         172.17.0.1
          IPv4 address for enp3s0:          172.16.0.180
          IPv6 address for enp3s0:          2400:38e0:1:415a::5f
          IPv6 address for enp3s0:          2400:38e0:1:415a::3c1
          IPv6 address for enp3s0:          2400:38e0:1:415a::340
          IPv6 address for enp3s0:          2400:38e0:1:415a::30e
          IPv6 address for enp3s0:          2400:38e0:1:415a::2fc
          IPv6 address for enp3s0:          2400:38e0:1:415a::26a
          IPv6 address for enp3s0:          2400:38e0:1:415a::1ed
          IPv6 address for enp3s0:          2400:38e0:1:415a::1c8
        
         * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
           just raised the bar for easy, resilient and secure K8s cluster deployment.
        
           https://ubuntu.com/engage/secure-kubernetes-at-the-edge
        
        112 updates can be applied immediately.
        2 of these updates are standard security updates.
        To see these additional updates run: apt list --upgradable
        
        New release '22.04.3 LTS' available.
        Run 'do-release-upgrade' to upgrade to it.
        
        2 updates could not be installed automatically. For more details,
        see /var/log/unattended-upgrades/unattended-upgrades.log
        
        *** System restart required ***
        Last login: Mon Dec  4 05:46:41 2023 from 112.134.181.176
        root@en-cvm-3k3ksju25s224:~# lsof -i:80
        COMMAND     PID     USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME
        nginx   2640375     root    8u  IPv4 51891929      0t0  TCP *:http (LISTEN)
        nginx   2640375     root   10u  IPv6 51891931      0t0  TCP *:http (LISTEN)
        nginx   3255037 www-data    8u  IPv4 51891929      0t0  TCP *:http (LISTEN)
        nginx   3255037 www-data   10u  IPv6 51891931      0t0  TCP *:http (LISTEN)
        nginx   3255037 www-data   23u  IPv4 63021741      0t0  TCP en-cvm-3k3ksju25s224:http->172.70.35.25:24018 (ESTABLISHED)
        nginx   3255037 www-data   24u  IPv4 63023734      0t0  TCP en-cvm-3k3ksju25s224:http->172.70.35.62:16118 (ESTABLISHED)
        nginx   3255037 www-data   25u  IPv4 63021742      0t0  TCP en-cvm-3k3ksju25s224:http->172.70.35.54:32766 (ESTABLISHED)
        nginx   3255037 www-data   26u  IPv4 63022558      0t0  TCP en-cvm-3k3ksju25s224:http->172.70.35.93:32076 (ESTABLISHED)
        nginx   3255038 www-data    8u  IPv4 51891929      0t0  TCP *:http (LISTEN)
        nginx   3255038 www-data   10u  IPv6 51891931      0t0  TCP *:http (LISTEN)
        nginx   3255039 www-data    8u  IPv4 51891929      0t0  TCP *:http (LISTEN)
        nginx   3255039 www-data   10u  IPv6 51891931      0t0  TCP *:http (LISTEN)
        nginx   3255040 www-data    8u  IPv4 51891929      0t0  TCP *:http (LISTEN)
        nginx   3255040 www-data   10u  IPv6 51891931      0t0  TCP *:http (LISTEN)
        root@en-cvm-3k3ksju25s224:~# cd /etc/nginx/sites-enabled/
        root@en-cvm-3k3ksju25s224:/etc/nginx/sites-enabled# ll
        total 40
        drwxr-xr-x 2 root root 4096 Dec  4 05:24 ./
        drwxr-xr-x 8 root root 4096 Dec  3 18:30 ../
        lrwxrwxrwx 1 root root   61 Mar 28  2023 api.virtualgreetingsworld.com.conf -> /etc/nginx/sites-available/api.virtualgree
        lrwxrwxrwx 1 root root   66 Mar 28  2023 app-card.virtualgreetingsworld.com.conf -> /etc/nginx/sites-available/app-card.v
        lrwxrwxrwx 1 root root   54 Nov  5 14:27 app-test1.chainlyze.ai.conf -> /etc/nginx/sites-available/app-test1.chainlyze.ai
        lrwxrwxrwx 1 root root   48 Nov  2 09:52 app.chainlyze.ai.conf -> /etc/nginx/sites-available/app.chainlyze.ai.conf
        lrwxrwxrwx 1 root root   71 Sep  1 12:18 chainlyze-api.empiredragonsolutions.com.conf -> /etc/nginx/sites-available/chain
        lrwxrwxrwx 1 root root   71 Aug 22 11:48 chainlyze-app.empiredragonsolutions.com.conf -> /etc/nginx/sites-available/chain
        lrwxrwxrwx 1 root root   34 Mar 28  2023 default -> /etc/nginx/sites-available/default
        lrwxrwxrwx 1 root root   53 Apr  9  2023 dev.maruoi.com.conf -> /etc/nginx/sites-available/maruoi/dev.maruoi.com.conf
        lrwxrwxrwx 1 root root   71 May  8  2023 empiredragonsolutions.com.conf -> /etc/nginx/sites-available/empire-dragon/empir
        lrwxrwxrwx 1 root root   49 Apr  9  2023 maruoi.com.conf -> /etc/nginx/sites-available/maruoi/maruoi.com.conf
        lrwxrwxrwx 1 root root   70 Jun  9 09:36 taxinor.chat.empiredragonsolutions.com.conf -> /etc/nginx/sites-available/taxino
        lrwxrwxrwx 1 root root   72 Jun  8 05:08 taxinor.client.empiredragonsolutions.com.conf -> /etc/nginx/sites-available/taxi
        lrwxrwxrwx 1 root root   72 Jun  8 04:59 taxinor.driver.empiredragonsolutions.com.conf -> /etc/nginx/sites-available/taxi
        lrwxrwxrwx 1 root root   57 Mar 28  2023 virtualgreetingsworld.com.conf -> /etc/nginx/sites-available/virtualgreetingswor
        lrwxrwxrwx 1 root root   48 Jun 13 13:57 winners-live.com.conf -> /etc/nginx/sites-available/winners-live.com.conf
        root@en-cvm-3k3ksju25s224:/etc/nginx/sites-enabled# nano maruoi.com.conf
        root@en-cvm-3k3ksju25s224:/etc/nginx/sites-enabled# cd /var/www/maruoi/maruoi_app/
        root@en-cvm-3k3ksju25s224:/var/www/maruoi/maruoi_app# pwd
        /var/www/maruoi/maruoi_app
        root@en-cvm-3k3ksju25s224:/var/www/maruoi/maruoi_app# ll
        total 468
        drwxr-xr-x 14 root root   4096 Dec  4 05:31 ./
        drwxr-xr-x  4 root root   4096 Apr  9  2023 ../
        -rw-r--r--  1 root root    258 Apr  9  2023 .editorconfig
        -rw-r--r--  1 root root   1137 Apr  9  2023 .env
        -rw-r--r--  1 root root   1067 Apr 13  2023 .env.example
        -rw-r--r--  1 root root   1137 Jul 21 06:08 .env.lakshan.backup
        drwxr-xr-x  8 root root   4096 Aug  4 06:57 .git/
        -rw-r--r--  1 root root    179 Apr  9  2023 .gitattributes
        -rw-r--r--  1 root root    227 Apr  9  2023 .gitignore
        -rw-r--r--  1 root root   4158 Apr  9  2023 README.md
        drwxr-xr-x  7 root root   4096 Apr  9  2023 app/
        -rw-r--r--  1 root root   1686 Apr  9  2023 artisan
        drwxr-xr-x  3 root root   4096 Apr  9  2023 bootstrap/
        -rw-r--r--  1 root root   1847 Apr  9  2023 composer.json
        -rw-r--r--  1 root root 296764 Apr  9  2023 composer.lock
        drwxr-xr-x  2 root root   4096 Apr  9  2023 config/
        drwxr-xr-x  5 root root   4096 Apr  9  2023 database/
        drwxr-xr-x  3 root root   4096 Apr  9  2023 lang/
        -rw-r--r--  1 root root  62271 Apr 13  2023 package-lock.json
        -rw-r--r--  1 root root    381 Apr  9  2023 package.json
        -rw-r--r--  1 root root   1175 Apr  9  2023 phpunit.xml
        drwxr-xr-x  4 root root   4096 Apr 13  2023 public/
        drwxr-xr-x  6 root root   4096 Apr  9  2023 resources/
        drwxr-xr-x  2 root root   4096 Apr 14  2023 routes/
        drwxrwxrwx  5 root root   4096 Apr  9  2023 storage/
        -rw-r--r--  1 root root    138 Apr 13  2023 test.http
        drwxr-xr-x  4 root root   4096 Apr  9  2023 tests/
        drwxr-xr-x 39 root root   4096 Apr  9  2023 vendor/
        -rw-r--r--  1 root root    312 Apr  9  2023 vite.config.js
        root@en-cvm-3k3ksju25s224:/var/www/maruoi/maruoi_app# nano .env
        root@en-cvm-3k3ksju25s224:/var/www/maruoi/maruoi_app# ^C
        root@en-cvm-3k3ksju25s224:/var/www/maruoi/maruoi_app# lsof -i:80
        ```

        -