# nginx-autoindex-theme



## nginx 配置

```conf
server {
    listen       80;
    server_name  mirrors.test.com;
    root         /data/yum/mirrors;   #这里是yum源存放目录


    location /yum {
        autoindex on;        #打开目录浏览功能
        autoindex_exact_size off;  # off：以可读的方式显示文件大小
        autoindex_localtime on; # on、off：是否以服务器的文件时间作为显示的时间

        add_before_body /.theme/header.html;
        add_after_body /.theme/footer.html;

        charset utf-8,gbk; #展示中文文件名
        client_max_body_size 4G;
        alias /data/yum/mirrors/yum/;
    }
    
    location / {
        index index.html;
    }

    # 禁止访问的文件或目录
    location ~ ^/(\.user.ini|\.htaccess|\.git|\.svn|\.project|LICENSE|RESDME.md) {
      return 404;
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   html;
    }
}
```


## 主题

将theme目录复制到/data/yum/mirrors

```
cd /data/yum/mirrors
mv theme .theme
```



