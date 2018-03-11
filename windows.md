1、下载并安装 Docker Toolbox （win7用这个，win10用 Docker for Windows）
	https://get.daocloud.io/#install-docker-for-mac-windows

2、更改虚拟机

找到C:\Users\xxx\.docker\machine\machines\default\default\，打开default.vbox，改下面这段
	<HardDisks>
		<HardDisk uuid="{a00bd5d7-4d45-4b26-8bc9-183fb64ea11c}" location="x/disk.vmdk" format="VMDK" type="Normal"/>
	</HardDisks>
再把vmdk文件移到其他盘就可以了

加一个共享文件夹，比如 E:/www 挂载到 /www

3、连接docker-machine

	docker-machine ssh default

也可以用winscp，可以去virtual box查看端口转发里的端口，然后用  默认的用户名和密码： docker/tcuser 连接

4、常用命令
查看容器
	docker ps -a
	docker container ls --all

进入容器
	docker container exec -it web /bin/bash

拷贝文件
	docker cp /share/xxx lnmp1.5:/data/
