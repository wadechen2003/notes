##Tomcat8 Redis Session manager

如果要用Redis做為 tomcat 的 session 集中管理, Tomcat6, Tomcat7 已經有套件可以完成  
[tomcat-redis-session-manager](https://github.com/jcoleman/tomcat-redis-session-manager)  
但這套件沒有支援到tomcat8  
我沒有詳細去看code中不支援tomcat8的原因,  
決定直接去google找大牛改寫的解決方案,  
請參考[tomcat8 redis session-manager](http://www.voidcn.com/blog/wang_biao_1314/article/p-4485812.html)  

在測試的時候我沒辦法把 session 設定到redis中, 一直亂找才發現原因相當愚蠢,  
使用sesion manager, 必須要修改 tomcat /conf 中的 context.xml 
讓tomcat的 HttpSession 由 redis接管 
我一直去修改 $tomcat_home/conf/context.xml,   
但因為我是在eclipse中 add 的tomcat,  
其實要到 eclipse 放 server conf 的folder 去找context.xml  
開發經驗不足才會發生這種問題, 再加油吧.