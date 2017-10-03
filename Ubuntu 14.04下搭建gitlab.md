#Ubuntu14.04下搭建gitlab

##搭建前环境准备
1.Ubuntu14.04 64位系统   
2.gitlab包   
3.gmail邮箱或者163邮箱一个    
##安装步骤    
###1.安装需要的库和软件
什么都不管执行下面的命令。需要注意的是在安装postfix的时候，需要进行一个选择。postfix是用来发邮件的，由于需要发送验证邮件，所以这个是必须装的，也有其他的软件用来发送软件，但是可能会遇到比较多的坑。

为了方便把邮件发出去，直接使用了企业邮箱的邮件服务，只需要设置smtp服务器就可以了。

sudo apt-get install curl openssh-server ca-certificates postfix 


在一图中选择Local only选项   
在二图中填写localhost      

				            图一
![](https://i.imgur.com/o3FUIJ0.png)

				            图二
![](https://i.imgur.com/f8jldZj.png)


###2.添加gitlab包并进行安装
方法一：curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
sudo apt-get install gitlab-ce 

但是由于大陆网速比较慢，下载会非常慢，速度在几K左右

方法二：我把我下载的一个Ubuntu 64位的版本放在百度云上面了。百度云下载地址： [http://pan.baidu.com/s/1kUoU5hH](http://pan.baidu.com/s/1kUoU5hH)

下载好之后执行命令：
sudo dpkg -i gitlab-ce_7.10.5~omnibus-1_amd64.deb 

######上面的那个命令安装完成后会显示如下的提示：
gitlab: GitLab should be reachable at http://ubuntu   

//这个http://ubuntu就是待会要登录的gitlab主页，所以需要将其主机的解析加入到hosts文件中，如果上面命令中填的是IP,则不用添加到hosts中    

gitlab: Otherwise configure GitLab for your system by editing /etc/gitlab/gitlab.rb file    
gitlab: And running reconfigure again.   
gitlab:      
gitlab: For a comprehensive list of configuration options please see the Omnibus GitLab 

readme    
gitlab: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/README.md   
gitlab: It looks like GitLab has not been configured yet; skipping the upgrade script.


###3.配置和使用gitlab    
1.使用命令 sudo vim /etc/gitlab/gitlab.rb配置访问域名端口及邮箱,参照所示图配置，其中图3是官网给出的gmail邮箱配置，图4，5是根据图3作出的自定义相关配置，图6是配置之后查看是否配置成功的命令。


								图3  gmail邮箱配置例子   
![](https://i.imgur.com/W0qV7lY.png) 

								图4  配置域名端口   
![](https://i.imgur.com/6hgQTlg.png)      

								图5  配置邮箱    
![](https://i.imgur.com/H7yHt4n.png)     


配置好之后执行命令使配置有效：sudo gitlab-ctl reconfigure   
								
								图6 查看是否配置成功   
![](https://i.imgur.com/s9kzqd7.png)         



出现图示界面则表明配置成功，若端口处于关闭状态，使用命令sudo gitlab-ctl start打开。



####在浏览器访问gitlab主机名    
我配置的主机IP是192.168.100.34，我配置的gitlab服务器的名字是localhost,在浏览器中输入192.168.100.34或者http://localhost，出现如图7所示的界面。初始的登录名是root，初始登录密码是5iveL!fe，进入之后会提示你重新修改密码。至此，gitlab在Ubuntu 14.04上的配置已经结束。     
![](https://i.imgur.com/JsD5FrE.png)


   



