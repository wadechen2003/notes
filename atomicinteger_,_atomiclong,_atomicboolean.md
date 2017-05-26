##AtomicInteger , AtomicLong, AtomicBoolean

JAVA中此三種類型的物件, 可以分別針對Integer, Long, Boolean做原子化的操作  

###why should we need atomic operation?  

1.參考於  
[Atomic Operations and multithreading](http://stackoverflow.com/a/16729461)  

a = 28, assign 就是一個 atomic operation.  
但是 a++ 這樣的動作則不是atomic opreation,  
因為做a++時, 分別做了  
讀取 a 值  
增加 a 值  
將結果寫回 a  
假設說你現在使用 multi thread 的編寫, 便有可能得到不正確的結果  
如此情況下使用 AtomicInteger 物件去操作, 就不用擔心這問題了

2.另外一種情況是使用 32-bit的系統時  
`long foo = 12345678L;`  
這類型的 assign 雖然看似一個opration就完成,  
但事實上會先寫入first 32bit, 然後再寫入剩下的32bit  
multi-thread時就有可能造成錯誤,( 還沒寫入剩下32bit時就被讀取 )  
這種情況就可以用AtomicLong物件去處理.  
另外一種解決方式是宣告該long變數為 volatile.  
` public volatile long foo = 12345678L;`
