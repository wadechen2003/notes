#### 環境  MAC OS X El Captain 10.11.4
#### MAMP 3.5  
  
至路徑  `/Applications/MAMP/conf` 新增 `my.cnf`  
雖然據說MAMP mysql 會產生自己的my.cnf, 但至今我仍找不到他在哪  
總之先別管這麼多, 在這新增的檔案中加入以下 conf 

	[mysqld]
	#bind-address=127.0.0.1
	
大功告成.🤗

 
