# Java Restful client
  
使用了 apache httpClient 的lib  
如果用maven做專案管理, 在pom.xml中加入  
	
	<dependency>
	<groupId>org.apache.httpcomponents</groupId>
	<artifactId>httpclient</artifactId>
	<version>{httpcomponents.version}</version>
	</dependency>
  
我是使用4.5的版本.
至於apache httpClient的使用範例可以到以下這網址  
[HttpClien examples](https://hc.apache.org/httpcomponents-client-ga/examples.html)

下面隨手放一個example, 用 
[JSONPlaceholder](http://jsonplaceholder.typicode.com/)
提供的API來測試  


	``` 
		
	package com.wade.test;
	import java.io.*;
	import org.apache.http.HttpEntity;
	import org.apache.http.HttpHost;
	import org.apache.http.HttpResponse;
	import org.apache.http.client.HttpClient;
	import org.apache.http.client.methods.HttpGet;
	import org.apache.http.impl.client.CloseableHttpClient;
	import org.apache.http.impl.client.HttpClients;
 
	public class RestfulClient101 {
 		
 		public final static void main(String[] args) throws Exception{
     		CloseableHttpClient httpClient = HttpClients.createDefault();
	  		InputStream inputStream = null;
	  		try {
      
    			String requestStr = "http://jsonplaceholder.typicode.com/posts/1"; 
    			HttpGet httpGetRequest = new HttpGet(requestStr);
    			HttpResponse httpResponse = httpClient.execute(httpGetRequest);
 
    			//另外一種寫法, 假設需要在1個host上使用多個api, 就只要設定一次target.
    			HttpHost target = new HttpHost("jsonplaceholder.typicode.com", 80, "http");
    			HttpGet getRequest = new HttpGet("/posts/1");
    			HttpGet getRequest2 = new HttpGet("/posts/2");
    			HttpResponse res2 = httpClient.execute(target, getRequest);
    			
    			//show http response status
    			System.out.println(httpResponse.getStatusLine());
    		
    			HttpEntity entity = httpResponse.getEntity();
 
	      		byte[] buffer = new byte[1024];
	      		if(entity != null){
	        		inputStream = entity.getContent();
	          		int bytesRead = 0;
	          		BufferedInputStream bufferedis = new BufferedInputStream(inputStream);
	          		while ((bytesRead = bufferedis.read(buffer)) != -1){
	           			String jsonStr = new String(buffer, 0, bytesRead);
	           			System.out.println(jsonStr);
	        		}
	      		}
	    	} catch (Exception e) {
	     		 e.printStackTrace();
	  	    } 
	  	    inputStream.close();
	  	  	httpClient.close();
  		}
	}

	
	

	```



