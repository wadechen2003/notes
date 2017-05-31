### match 用來搜尋字詞是否有出現在整段 paragraph 之中  

以下這種情況, 
"subject": "Wi-Fi noise level high" 會搜到. 也就是說有出現 noise 就可以搜尋到</br>   

```
GET /n_cms_core/pns_log/_search
{
    "query":{
        "match" : {
            "subject" : "noise"
        }
    }
}
```
另外, 還有幾個參數可以替query增加條件, 

#### "operator":"and/or"", 如果 query 中超過一個字詞, and:兩者同時出現, or:一者出現即可.

```
GET /n_cms_core/pns_log/_search
{
    "query":{
        "match" : {
            "subject" : {
                "query":"Wi-Fi high",
                "operator": "and"
            }
        }
    }
}
```
假設 "subject":"Wi-Fi level low"</br>
	**and**: 無法搜尋到, 因為 Wi-Fi 和 high 兩者沒有同時出現</br>
	**or** : 可以搜尋到. 因為有出現 Wi-Fi</br> 

值得注意的是, 如果該欄位設定為 <font color="red">"index": "not_analyzed"</font>, 則只能完全相同才可以 query 出來.
	
	



#### "type":"phrase" 表示要搜尋的是一個片語. 所以會 Wi-Fi noise 整句下去搜.

```
GET /n_cms_core/pns_log/_search
{
    "query":{
        "match" : {
            "pns.content.aps.customize.subject" : {
                "query":"Wi-Fi noise",
                "type":"phrase"
            }
        }
    }
}
```



#### march_phrase_prefix 有點類似 SQL中 LIKE xxx% 的用法, 只利用 prefix 去搜尋.

```
{
    "match_phrase_prefix" : {
        "message" : "Wi-Fi no"
    }
}
```











