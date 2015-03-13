# Laravel Homestead
clone from https://github.com/andrewelkins/Laravel-4-Bootstrap-Starter-Site

# Setup homestead
## Get PHPMyAdmin in vagrant
```
sudo apt-get install phpmyadmin
cd ~/Sites && serve phpmyadmin.app /usr/share/phpmyadmin/
```
## Get mongoDB to work in vagrant:
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo pecl install mongo'
```

edit php.ini
```
sudo vi /etc/php5/fpm/php.ini
```
Add extension=mongo.so to the php.ini file
```
sudo vi /etc/php5/cli/php.ini
```
Add extension=mongo.so to the php.ini file, then restart vagrant box


## Get beanstalkd to work in vagrant:
```
sudo apt-get update
sudo apt-get install beanstalkd
sudo service beanstalkd start
sudo apt-get install supervisor
sudo vim /etc/supervisor/conf.d/myqueue.conf
```
Insert the following lines in the file
```
[program:myqueue]
command=php artisan queue:work --daemon --env=your_environment
directory=/home/vagrant/Code/laravel-homestead
stdout_logfile=/home/vagrant/Code/laravel-homestead/app/storage/logs/myqueue_supervisord.log
redirect_stderr=true
autostart=true
autorestart=true
```
Then run
```
sudo supervisorctl
> reread
> add myqueue
> start myqueue 
```

## Get cache to work in vagrant:
```
sudo /etc/init.d/memcached start
