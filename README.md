# centos_lnmp

	docker network create -d bridge lnmp
	
	docker volume create mysql
	docker container run -d --name mysql56 -p 3306:3306 --mount source=mysql,target=/var/lib/mysql --env MYSQL_ROOT_PASSWORD=123456 --network lnmp mysql:5.6

	docker volume create redis
	docker container run -d --name redis -p 6379:6379 --mount source=redis,target=/data --network lnmp redis

	docker volume create www
	docker container run -dit --rm --privileged --name lnmp1.5 -p 80:80 -p 63700:22 --mount source=www,target=/data --network lnmp he426100/lnmp:1.5 /usr/sbin/init

	docker container exec -it lnmp1.5 /bin/bash
	yum install -y openssh-server
	systemctl start sshd
	systemctl status sshd

1、加上 -i -t 就可以解决容器无法启动的问题

2、加上 --privileged 和 /usr/sbin/init 可以解决centos镜像不能使用systemctl的问题（慎用，会造成严重问题，详见 https://github.com/boot2docker/boot2docker/issues/1301）

3、使用docker volume可以解决容器删除后文件也消失的问题（妈妈再也不应担心我总是在重复部署代码了）

4、用docker创建mysql服务和redis服务实在太简单，所以lnmp镜像只要nginx+php-fpm就够了

5、这东西的价值在于可以轻易地创建、复制、恢复环境，让日常使用回归日常，让开发的集中到开发，免于安装一堆东西，不敢重装系统
