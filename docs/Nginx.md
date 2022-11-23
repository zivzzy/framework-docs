# Nginx配置

```
worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;

    server {
        listen       80;
        server_name  localhost;
  charset utf-8;

  location / {
            root   /home/fedx-framework/packages/web-framework;
   try_files $uri $uri/ /index.html;
            index  index.html index.htm;
        }
  
  location /prod-api/ {
   proxy_set_header Host $http_host;
   proxy_set_header X-Real-IP $remote_addr;
   proxy_set_header REMOTE-HOST $remote_addr;
   proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
   proxy_pass http://localhost:8080/;
  }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
}
```

# 建议开启Gzip压缩

在http配置中加入如下代码对全局的资源进行压缩，可以减少文件体积和加快网页访问速度。

```
# 开启gzip压缩
gzip on;
# 不压缩临界值，大于1K的才压缩，一般不用改
gzip_min_length 1k;
# 压缩缓冲区
gzip_buffers 16 64K;
# 压缩版本（默认1.1，前端如果是squid2.5请使用1.0）
gzip_http_version 1.1;
# 压缩级别，1-10，数字越大压缩的越好，时间也越长
gzip_comp_level 5;
# 进行压缩的文件类型
gzip_types text/plain application/x-javascript text/css application/xml application/javascript;
# 跟Squid等缓存服务有关，on的话会在Header里增加"Vary: Accept-Encoding"
gzip_vary on;
# IE6对Gzip不怎么友好，不给它Gzip了
gzip_disable "MSIE [1-6]\.";
```
