使用 Gitlab CI 為專案建立 autobuild 的環境
  
* Gitlab
* Gitlab-runner  

Gitlab 端為程式 repository  
Gitlab-runner 端為build machine. 

autobuild的步驟:  

1. Developer push code  
2. Gitlab-CI calls Gitlab-runner  
3. Gitlab-runner builds the project  
4. Gitlab-runner builds the Docker image and commit  

預先準備  

* 部門公用的 docker hub account, set it private, share account
* 一份具有原始結構的 docker image,  
	* 如此則只需要替換 
		1. /usr/cms_core/sercomm-cms-core.jar
		2. /usr/cms_meta/sercomm-cms-meta.jar
		3. /usr/cms_core/lib/sercomm_ext_lib.jar
		4. /usr/cms_meta/lib/sercomm_ext_lib.jar
* Gitlab-runner host 得把 git, gitlab-runner 兩者加入 sudoers 中







