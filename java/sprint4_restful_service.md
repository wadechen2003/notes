##Spring4 restful web service basic example  

以下內容都來自於 [Spring.io](https://spring.io/guides/gs/rest-service/)

經過這個 example 後, 你會得到什麼 ?

```
http://localhost:8080/greeting
```
經由這個 url 會得到一個 json response 

```
{"id":1,"content":"Hello, World!"}
```

url 可以掛上 optional 的參數 name 

```
http://localhost:8080/greeting?name=wade
```

環境 Jdk 1.8 +  
build 我用 maven 3.0  

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

    <repositories>
        <repository>
            <id>spring-releases</id>
            <url>https://repo.spring.io/libs-release</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>spring-releases</id>
            <url>https://repo.spring.io/libs-release</url>
        </pluginRepository>
    </pluginRepositories>
</project>
```  

使用 spring-boot-maven-plugin 可以把專案包成 excutable 的 jar 檔, 而且包含 embedded tomcat.  
是說也可以把專案打包成 war 檔後 deploy, 但這個我還沒有看操作步驟.. 

---
截至目前為止, 已經把專案和build檔環境處理完成, 現在開始就是code實作的部分了.  
在開始實作code之前, 先想一下service和 client之間會有怎樣的互動.  

1. service 會處理 GET/POST request for /greeting, 參數 name 是optional.
2. service 應該要回傳 response 200OK, 以及 body 裝著 JSON  {
    "id": 1,
    "content": "Hello, World!"
}  
且此 id 為unique, content 用文字表示 greeting.
---

以下是實作的部分

首先製造 response 用的 Object  
```src/main/java/hello/Greeting.java```  

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
package hello;

import java.util.concurrent.atomic.AtomicLong;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

    private static final String template = "Hello, %s!";
    private final AtomicLong counter = new AtomicLong();

    @RequestMapping("/greeting")
    public Greeting greeting(@RequestParam(value="name", defaultValue="World") String name) {
        return new Greeting(counter.incrementAndGet(),
                            String.format(template, name));
    }
}
```

```@RequestMapping("/greeting")```  
生成url的對應, 告知此為 /greeting 的 servlet.    
 
```@RequestMapping(value = "/greeting", method = RequestMethod.GET)```  
如果想要指定此request限定為 GET/POST/PUT..., 可以用這方法宣告 

```@RequestParam(value="name", defaultValue="World") String name```   
參數的對應, 因為有設defaultValue, 所以此參數對client端而言為 optional.

可以發現return 為剛剛做的 Greeting 物件, spring 會利用 jackson2 將 Greeting 物件直接轉成 JSON 物件後回傳.

如果要將此專案製作成 standalone application, 需要做一個含有 main() 的 entry class

```
package hello;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

到此為止, 使用 mvn clean package 包成一個 jar 後便可以直接取用惹..






















