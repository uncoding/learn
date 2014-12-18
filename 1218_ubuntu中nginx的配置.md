##ubuntu 14.04 nginx的配置
###因为之前的机器上有apache2,在安装nginx的时候 使用命令 apt-get remove apache2  卸载apache2
###1.安装ngxin, apt-get install nginx  安装完事; 在浏览器中直接 localhost可以查看到nginx运行成功;
###2.安装php5-fmp,  apt-get install php5-fpm, 可以直接进行安装;
###3.对nginx进行配置，是nginx和安装的php5-fpm相对应的给链接起来；默认的地址为 /etc/nginx/site-avlible/default;
####a:先看这是默认的配置文件,配置完之后仍然后问题，表现在  1.修改路径和显示403错误；  2.打开php页面的时候进行下载页面的操作。。
--
server {
        listen 80 default_server;
        listen [::]:80 default_server ipv6only=on;

        #root /usr/share/nginx/html;
        root /usr/share/nginx/html;
        index index.php index.html index.htm;

        # Make site accessible from http://localhost/
        server_name localhost;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                #try_files $uri $uri/ =404;
                try_files $uri $uri/ /index.html;
                # Uncomment to enable naxsi on this location
                # include /etc/nginx/naxsi.rules
        }

        # Only for nginx-naxsi used with nginx-naxsi-ui : process denied requests
        #location /RequestDenied {
        #       proxy_pass http://127.0.0.1:8080;    
        #}

        error_page 404 /404.html;
        # redirect server error pages to the static page /50x.html
        #
        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
                root /usr/share/nginx/html;
        }

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
                fastcgi_split_path_info ^(.+\.php)(/.+)$;
        #       # NOTE: You should have "cgi.fix_pathinfo = 0;" in php.ini
        #
                # With php5-cgi alone:
#               fastcgi_pass 127.0.0.1:9000;
        #       # With php5-fpm:
                fastcgi_pass unix:/var/run/php5-fpm.sock;
                fastcgi_index index.php;
                include fastcgi_params;
        }

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        location ~ /\.ht {
                deny all;
        }
}
--
####b.网站查找的代码直接进行配置， 配置的路径 /etc/nginx/conf.d/test.com.conf 配置代码如下：
server {
        listen   80; # port 80 default
        root /var/www/test.com; # default directory where the files will be stored and served from
        index index.php index.html index.htm; # index defined to be served under directory
        server_name test.com; #name of the virtual host or domain

        location / {
                try_files $uri $uri/ /index.html;
        }

        error_page 404 /404.html;
        error_page 500 502 503 504 /50x.html;
        location ~ \.php$ {
                #fastcgi_pass 127.0.0.1:9000;
                # With php5-fpm:
                fastcgi_pass unix:/var/run/php5-fpm.sock;
                fastcgi_index index.php;
                include fastcgi_params;
        }
}

####以上的代码直接添加即可，然后进行配置server_name和root路径就行
####在进行配置的时候，可以发现是发现放在两个路径下，在/etc/nginx/nginx.conf中可以看到包含这两个路径
####然后进行本地host的配置就行
--
###注意的几个问题
####a.进行nginx虚拟主机配置的时候注意  用户组 group  start; restart; stop; status; ps auwx | grep httpd; 配置路径的查询; 不同的系统有所不相同
####b.php5-fpm的安装和查看他的状态，使用时候能够正常的运行;
####c.在命令行测试网站是否正常的启用；  curl wwww.test.com 
