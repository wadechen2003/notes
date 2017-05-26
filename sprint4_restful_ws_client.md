##Spring4 restful web service client basic example  

以下內容都來自於 [Spring.io](https://spring.io/guides/gs/consuming-test/)

***
環境 Jdk 1.8 +  
build 我用 maven 3.0  
***

```pom.xml```


``` 
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.springframework</groupId>
    <artifactId>gs-rest-service</artifactId>
    <version>0.1.0</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.3.5.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
        </dependency>        
    </dependencies>

    <properties>
        <java.version>1.8</java.version>
    </properties>
	

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
  </project>
```  

---
以下是實作的部分

首先製造用來接 response 的 Object  
```
src/main/java/hello/Quote.java
```  

```
package hello;

public class Greeting {

    private final long id;
    private final String content;

    public Greeting(long id, String content) {
        this.id = id;
        this.content = content;
    }

    public long getId() {
        return id;
    }

    public String getContent() {
        return content;
    }
}
```

接下來製作 resource controller, 這個 class 完成了  
request 的 mapping.  

```
package com.wade.wsclient.bean;

import com.fasterxml.jackson.annotation.JsonFormat.Value;
import com.fasterxml.jackson.annotation.JsonIgnoreProperties;

@JsonIgnoreProperties(ignoreUnknown = true)
public class Quote {

	private String type;
	private Value value;
	public String getType() {
		return type;
	}
	public void setType(String type) {
		this.type = type;
	}
	public Value getValue() {
		return value;
	}
	public void setValue(Value value) {
		this.value = value;
	}
	
	public String toString(){
		
		return "{\"type\":\""+type+"\",\"value\":"+value+"}";
		
	}
	
	
	
}
// @JsonIgnoreProperties - 


```

```
@JsonIgnoreProperties
```
Jackson lib 的 annotation, 讓jackson lib 在轉換 response 到 javabean 的時候, 知道只需要取出和 bean 相對應的 values.  
example res = {"shit":123, "type":"super man", "value":{"inner":"ininder"}};
bean 中加上這個 annotation 後, 只會取出 type, value....




```
package hello

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application implements CommandLineRunner{

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
    
    
    @Override
    public void run(String ...args) throws Exception{
   		RestTemplate restTemplate = new RestTemplate();
    	Quote quote = restTemplate.getForObject(" url ", Quote.class);
    	System.out.println(quote.toString);
    }
    
}
```
RestTemplate 物件可以利用 jackson lib 將 json 形式的 response 轉換成 java Object
RestTemplate 中除了 get 以外, 其他 http request 的功能大多也有提供.



















