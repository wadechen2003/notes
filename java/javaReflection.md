## JAVA Reflection

```java 
try {
	Class stringClassObj = Class.forName("java.lang.String");
	Method stringLengths = stringClassObj.getMethod("length");
	Object strObj = stringClassObj.getDeclaredConstructor(String.class).newInstance("abcdefg");
	Object ret = stringLengths.invoke(strObj, null);
	System.out.println(ret);
	
	Annotation[] annos = strObj.getAnnotations();
	
	} catch (Exception e) {
		e.printStackTrace();
	}
		
```



