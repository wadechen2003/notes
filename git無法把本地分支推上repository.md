##git無法把本地分支推上repository##

剛剛遇到一種情況, 把遠端的 repo clone 回本地後 checkout 新的 branch  

``` 
$ git checkout -b dev 
```  

新增一些內容後, 想把它 push 回 remote repo

``` 
$ git commit -m "comment" 
$ git push
```

出現 **fatal: No configured push destination**  
這是說 git 不知道這 brach 要丟到哪個 remote repo
接著我下

```
$ git push -u origin dev
```
跳出 **fatal: 'origin' does not appear to be a git repository**  
沒有 origin 這個 remote repo.   
印象中 origin 在 clone repo 時是會自動建立 refrence , 下指令查看

```
$ git remote -v
```
發現真的沒有任何 remote ref, 就自己動手加上去

``` 
$ git remote add origin remote-repo-url 
```
接著再下  

```
$git push -u origin dev
```
搞定. 成功推上去, remote repo 上多出了這分枝.
