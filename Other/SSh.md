
查看ssh服务时, 没有发现sshd, 说明服务端没有安装, 安装ssh服务端

```
    sudo apt install openssh-server
```

查看ssh服务, sshd存在即成功

```
ubuntu@ubuntu:~/Downloads$ ps -ef | grep ssh
ubuntu    1422  1345  0 15:22 ?        00:00:00 /usr/bin/ssh-agent /usr/bin/im-launch env GNOME_SHELL_SESSION_MODE=ubuntu gnome-session --session=ubuntu
root      8437     1  0 16:19 ?        00:00:00 /usr/sbin/sshd -D
ubuntu    9481  1766  0 16:20 pts/0    00:00:00 grep --color=auto ssh
ubuntu@ubuntu:~/Downloads$ 
```