# Ubuntu 16.04 開啟 Docker remote API


1.	`sudo vim /lib/system/docker.service`
	
	```
	ExecStart=/usr/bin/docker daemon -H fd:// -H tcp://0.0.0.0:5000
	```
	*	開啟時的參數, -H : host, 加開本機 port 5000

2.	`sudo systemctl daemon-reload`
3. 	`sudo service docker restart`
4. Check 是否服務有開啟. 
	1. 先`netstat -utln` 看看 5000 port 是不是有打開
	2. 若有, 到另外一台有裝 Docker Engine的機器 `sudo docker -H tcp://{remote host} ps`
	
	
