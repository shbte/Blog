### 0、问题

~~~
从2021年8月13日开始，在GitHub上执行Git操作时，不再接受以账户密码的形式完成身份验证。
下面介绍Git使用SSH密钥向GitHub提交代码。
~~~

### 1、安装SSH

~~~bash
在控制台输入以下命令，检查SSH是否安装：(以下情况为已安装)
    SSH

ubuntu@ubuntu:~/Desktop/VSCode$ ssh
usage: ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface]
           [-b bind_address] [-c cipher_spec] [-D [bind_address:]port]
           [-E log_file] [-e escape_char] [-F configfile] [-I pkcs11]
           [-i identity_file] [-J [user@]host[:port]] [-L address]
           [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port]
           [-Q query_option] [-R address] [-S ctl_path] [-W host:port]
           [-w local_tun[:remote_tun]] destination [command [argument ...]]
ubuntu@ubuntu:~/Desktop/VSCode$ 

tip：
安装SSH，对于Linux和Mac系统，其默认是安装SSH的，而对于Windows系统，其默认是不安装SSH的。
不过由于Git Bash自带了SSH. 可以通过在Git Bash中输入ssh命令，查看本机是否安装SSH。
~~~

### 2、生成SSH key

~~~bash
在控制台输入以下命令，生成SSH Key：(中间不输入，直接按三次回车)
    ssh-keygen -t rsa

ubuntu@ubuntu:~/Desktop/VSCode$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ubuntu/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/ubuntu/.ssh/id_rsa
Your public key has been saved in /home/ubuntu/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:A5elxDPMo0wwb7ThiPl3EYaDq5slSbm+y/YjojL8+TY ubuntu@ubuntu
The key's randomart image is:
+---[RSA 3072]----+
|    ooo=+ .      |
|   o.*+=B=       |
|  o..+*o=+       |
|  o...oo .       |
| . +. . S        |
|  = .. . .       |
|.. =             |
|+o* oE           |
|++=B+o.          |
+----[SHA256]-----+
ubuntu@ubuntu:~/Desktop/VSCode$ ls -l ~/.ssh/
总用量 8
-rw------- 1 ubuntu ubuntu 2602  5月 21 17:11 id_rsa
-rw-r--r-- 1 ubuntu ubuntu  567  5月 21 17:11 id_rsa.pub
ubuntu@ubuntu:~/Desktop/VSCode$
~~~

### 3、添加SSH key

~~~
将id_rsa.pub文件的内容添加到GitHub的SSH key：
登录GitHub => Settings => SSH and GPG keys => New SSH key => Add SSH key

ubuntu@ubuntu:~/Desktop/VSCode$ cat ~/.ssh/id_rsa.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC7H4jbyzLET0doLPdCuYtPfg7fwTpkHxadtx1WwXZWLMQitJkZzw8LwHorXQeA2QquuAV5eAL+j9ycHdfuJIo2sHS4qZSowqMqkDOfd53qEDyIWGbX//Frm8nzpNjnbPTdf/zvesSpFVTE47MxTXPgnB1XiOHG0q7OvD+jgg88c+tvsLRscr/ADb49GVeFzfgEh/V3DS9uzJOoEtUF4578joZLxiCtnjSwwKbYz57qkPxUPfyHqaEaGB8XUcSTTEupB/KcSTfqsGmbyozytbCrivn9QiBCN80rsUhTXoOjP86E2ZMVCDOu9ANealuFV9ZoSB0hx+9vTxPChrcrxIYICJzhNRcbEvqjIDzUukXkaVaRRu6cnAWi/WXih9kIpoDyz16bIZmhUoJMNX2hIPjhx9pe17MAvnEEyYMxMjfZ9Epva3W6hc2LeKy9W/XTG93uasOZcz033A841/9FqS2q4lOTO5MXIRbaK//EAMNgBicOvmBHAOESQfs4MEiUnmE= ubuntu@ubuntu
ubuntu@ubuntu:~/Desktop/VSCode$ 
~~~

### 4、验证绑定是否成功

~~~
在控制台输入以下命令，验证绑定是否成功：(出现Hi xxx，即为绑定成功)
    ssh -T git@github.com

ubuntu@ubuntu:~/Desktop/VSCode$ ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Hi shbte! You've successfully authenticated, but GitHub does not provide shell access.

ubuntu@ubuntu:~/Desktop/VSCode$ ssh -T git@github.com
Hi shbte! You've successfully authenticated, but GitHub does not provide shell access.
ubuntu@ubuntu:~/Desktop/VSCode$ 
~~~