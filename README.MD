docker搭建的laravel开发环境，包含nginx、php-fpm、mysql、redis、supervisor、kafka

使用
=======
将项目文件拷贝到app目录下
```
docker-compose build
docker-compose up -d 
```

配置文件目录
==========
```
mysql              mysql/conf
nginx              nginx/conf
php                php/conf
supervisor         supervisor/conf
```
