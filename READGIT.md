##如何在创建一个新的GIT工程
###1.注册一个帐号
###2.创建一个新的项目
###3.在本地自己熟悉的地方创建一个和在新项目一样名称的文件夹
###4.使用以下的提示操作
	##创建一个文件	touch README.md
	##初始化一个git	git init
	##添加操作	git add README.md
	##进行提交	git commit -m "first commit"
	##对应当前地址	git remote add origin https://github.com/unkowner/walk.git
	##提交		git push -u origin master
	##默认配置

	###git config --global user.name "your_username"
	###git config --global user.email your_email@domain.com

	##最后的提交需要每次的输入当前GIT的帐号和用户名，每次都提交都需要TT，但可以在本地生成一个唯一码，当前这个问题
####创建本地密钥方法
	##flow this http://www.asheep.cn/skill/git-ssh-key.html

##update test
##1. git add fileName.md
##2.git commit -a -m 'add'
##3.git push
##4.over
###How to create a new git
##1.regsiter a new user
##2.config the user.name
##3.config the user.email
##4.create a localhost key for git
