## About
gridfs module for nginx.  
>
I forked from [nginx-gridfs](https://github.com/nieoding/nginx-gridfs) but it onely support _id for PrimaryKey, So I migrated key support feature from mdirolf's 
[nginx-gridfs](https://github.com/mdirolf/nginx-gridfs.git).

## Feature
Support password and non-password authentication for nginx, mongo-gridfs connection
Tested on nginx(1.12.2, 1.18.0) 

## Installation
> only test build on centos

```bash
# mongo-c-driver
> yum install -y epel-release	# update repo, so mongo-c-driver can bo searched.
> yum install -y mongo-c-driver-devel

# get and build nginx
> yum install -y wget
> yum install -y pcre-devel openssl-devel zlib-devel # default nginx depends
> yum install -y gcc make	
# build nginx
> wget http://nginx.org/download/nginx-1.12.2.tar.gz
> tar -xf nginx-1.12.2.tar.gz
> cd nginx-1.12.2
> ./configure --with-openssl=/usr/include/openssl --add-module=../nginx-gridfs/
> make install
> ln -s /usr/local/nginx/sbin/nginx /usr/sbin/nginx
```
## Config
```ini
# nginx.conf
location /media/ {
    gridfs my_app field=filename type=string;
    mongo mongodb://username:password@127.0.0.1:27017;
}
```
> mongo connect-uri follow [the official format](https://docs.mongodb.com/manual/reference/connection-string/)
> 
> mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]

