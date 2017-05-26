## tuples in JAVA ##

想到很久之前, 遇過一個 method 必須回傳兩個 Objects 的情形.  
當時的處理方式很直覺, 把 Objects塞進 List,  
或者專門做一個 tuple 類別來處理這個情形,  
但 Peter Verhas, JAVA的知名部落客則是認為,  
不需要特別生出tuple的類別, 
應該直接使用 **java.util.AbstractMap.SimpleEntry**  
就可以裝下要回傳的兩個物件.  參考參考

[Sometimes you need tuples in Java. Or not.](https://javax0.wordpress.com/2015/04/22/sometimes-you-need-tuples-in-java-or-not/)
