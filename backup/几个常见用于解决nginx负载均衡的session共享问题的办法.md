查了一些资料，看了一些别人写的文档，总结如下，实现nginx session的共享：

PHP服务器有多台，用nginx做负载均衡，这样同一个IP访问同一个页面会被分配到不同的服务器上，如果session不同步的话，就会出现很多问题，比如说最常见的登录状态，下面提供了几种方式来解决session共享的问题：

## 1、不使用session，换用cookie
session是存放在服务器端的，cookie是存放在客户端的，我们可以把用户访问页面产生的session放到cookie里面，就是以cookie为中转站。你访问web服务器A，产生了session然后把它放到cookie里面，当你的请求被分配到B服务器时，服务器B先判断服务器有没有这个session，如果没有，再去看看客户端的cookie里面有没有这个session，如果也没有，说明session真的不存，如果cookie里面有，就把cookie里面的sessoin同步到服务器B，这样就可以实现session的同步了。

说明：这种方法实现起来简单，方便，也不会加大数据库的负担，但是如果客户端把cookie禁掉了的话，那么session就无从同步了，这样会给网站带来损失；cookie的安全性不高，虽然它已经加了密，但是还是可以伪造的。

## 2、session存在数据库（MySQL等）中
PHP可以配置将session保存在数据库中，这种方法是把存放session的表和其他数据库表放在一起，如果mysql也做了集群了话，每个mysql节点都要有这张表，并且这张session表的数据表要实时同步。

说明：用数据库来同步session，会加大数据库的IO，增加数据库的负担。而且数据库读写速度较慢，不利于session的适时同步。

## 3、session存在memcache或者redis中
memcache可以做分布式，php配置文件中设置存储方式为memcache，这样php自己会建立一个session集群，将session数据存储在memcache中。

说明：以这种方式来同步session，不会加大数据库的负担，并且安全性比用cookie大大的提高，把session放到内存里面，比从文件中读取要快很多。但是memcache把内存分成很多种规格的存储块，有块就有大小，这种方式也就决定了，memcache不能完全利用内存，会产生内存碎片，如果存储块不足，还会产生内存溢出。

## 4、nginx中的ip_hash技术能够将某个ip的请求定向到同一台后端
这样一来这个ip下的某个客户端和某个后端就能建立起稳固的session，ip_hash是在upstream配置中定义的：
```
upstream nginx.example.com
       { 
                server 192.168.74.235:80; 
                server 192.168.74.236:80;
                ip_hash;
       }
       server
       {
                listen 80;
                location /
                {
                        proxy_pass
                       http://nginx.example.com;
                }
    }
```
ip_hash是容易理解的，但是因为仅仅能用ip这个因子来分配后端，因此ip_hash是有缺陷的，不能在一些情况下使用：

1.nginx不是最前端的服务器。

ip_hash要求nginx一定是最前端的服务器，否则nginx得不到正确ip，就不能根据ip作hash。譬如使用的是squid为最前端，那么nginx取ip时只能得到squid的服务器ip地址，用这个地址来作分流是肯定错乱的。

2.nginx的后端还有其它方式的负载均衡。

假如nginx后端又有其它负载均衡，将请求又通过另外的方式分流了，那么某个客户端的请求肯定不能定位到同一台session应用服务器上。这么算起来，nginx后端只能直接指向应用服务器，或者再搭一个squid，然后指向应用服务器。最好的办法是用 location作一次分流，将需要session的部分请求通过ip_hash分流，剩下的走其它后端去。

## 5、upstream_hash
为了解决ip_hash的一些问题，可以使用upstream_hash这个第三方模块，这个模块多数情况下是用作url_hash的，但是并不妨碍将它用来做session共享。（暂时不会用，不明白）

## 6、使用第三方模块ngx_http_consistent_hash通过一致性哈希算法来选择合适的后端节点。(推荐)
https://www.nginx.com/resources/wiki/modules/consistent/hash/附：Nginx的ngx_http_consistent_hash模块的官网使用文档：

Linux下该模块的安装编译：
```
cd /usr/local/src

wget https://github.com/replay/ngx_http_consistent_hash/archive/master.zip

unzip master.zip

cd /usr/local/src/nginx-1.12.0

./configure --prefix=/usr/lcoal/nginx --add-module=/usr/local/src/ngx_http_consistent_hash-master/

pkill -9 nginx

make&make install
nginx.conf:

worker_processes  1;  
  
events {  
    worker_connections  1024;  
}  
   
http {  
    upstream servers {  
        consistent_hash $request_uri;  
        server 192.168.1.86:80;  
        server 192.168.1.88:80;  
    }  
  
    server {  
        listen 80;  
        server_name localhost;  
        location / {  
             proxy_pass http://servers;  
       }  
    }  
}
```