Linux 发行版将 OpenGL 链接库放在其它目录, 而Qt 默认在 /usr/lib/ 目录下查找动态链接库, 所以需要手动建立链接

```
ubuntu@ubuntu:~$ locate libGL.so
/snap/gnome-3-34-1804/72/usr/lib/x86_64-linux-gnu/libGL.so
/snap/gnome-3-34-1804/72/usr/lib/x86_64-linux-gnu/libGL.so.1
/snap/gnome-3-34-1804/72/usr/lib/x86_64-linux-gnu/libGL.so.1.0.0
/snap/gnome-3-38-2004/70/usr/lib/x86_64-linux-gnu/libGL.so
/snap/gnome-3-38-2004/70/usr/lib/x86_64-linux-gnu/libGL.so.1
/snap/gnome-3-38-2004/70/usr/lib/x86_64-linux-gnu/libGL.so.1.7.0
/usr/lib/x86_64-linux-gnu/libGL.so.1
/usr/lib/x86_64-linux-gnu/libGL.so.1.0.0
ubuntu@ubuntu:~$ sudo ln -s /usr/lib/x86_64-linux-gnu/libGL.so.1 /usr/lib/libGL.so
ubuntu@ubuntu:~$ 
```