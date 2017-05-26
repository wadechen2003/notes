##GitLab Runner How-To

###Installation
#####CentOs
1. Install ant  
使用 Apache Ant 作為 Java build tool  
`$sudo yum -y install ant` 

2. Install Java jdk 1.7  
`$sudo yum -y install java-1.7.0-openjdk`	
3. Add repo for GitLab ci runner  
`curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-ci-multi-runner/script.rpm.sh | sudo bash`

4. Install GitLab-Ci-Runner  
`sudo yum -y install gitlab-ci-multi-runner`


###How to Use
1. *Register*  
安裝完成後, 向你的 project 註冊這個 Runner.  
Gitlab 中 Project Setting -> Runner  
點選進去後可以看見註冊用的 URI 和 TOKEN.  
接著回到 build machine 上  
`$sudo gitlab-ci-multi-runner register`  
輸入剛剛拿到那組 URI, TOKEN, 如果連結成功 executer 請選擇 shell.

2. 啟動 Runner  
`$sudo gitlab-ci-multi-runner run`



