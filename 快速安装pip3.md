# 快速安装pip3

linux安装pip3总是出各种玄学问题，使用apt安装基本很难成功。

经过不断踩坑终于发现了快速安装pip3的方法：终极方法，两行命令搞定

```
wget https://bootstrap.pypa.io/get-pip.py
sudo python3 get-pip.py
pip3 -V
```

