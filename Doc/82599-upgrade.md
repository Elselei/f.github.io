1. 下载 Boot-Utility-Preboot  
```
  https://downloadcenter.intel.com/download/23691/Ethernet-Intel-Ethernet-Connections-Boot-Utility-Preboot-Images-and-EFI-Drivers
```

2. 选择linux系统对应的Preboot.tar.gz下载  
  ![image.png](https://user-images.githubusercontent.com/19662303/168554709-41878891-d230-4c19-8e8b-99d001b51742.png)

3. 下载文件解压后进入目录拷贝BootIMG.FLB到Linux_x64目录  
```
  # cd Preboot/APPS/BootUtil
  #ls -la
  BootIMG.FLB Docs        Linux32     Linux_x64   iv.txt      readme.txt
  #cp BootIMG.FLB  Linux_x64/
```

4. 取Linux_x64目录单独打包  
```
  tar czvf Linux_64.tar.gz Linux_x64
```

5. 拷贝Linux_64.tar.gz到需要更新固件的机器中(本案例以ip 1.1.1.1为例)  
```
  scp Linux_64.tar.gz root@1.1.1.1/tmp/
```

6. 登陆对应的机器进行解压,并设置bootutil64e有可执行权限  
```
  #ssh root@1.1.1.1
  # cd /tmp
  #tar xvf Linux_64.tar.gz
  #cd Linux_64
  #chmod a+x bootutil64e
```

7. 判断网卡是否需要刷UEFI,如下所示不需要刷UEFI，如10G网卡只显示PXE或者不显示需要参考第8步刷下固件  

```
./bootutil64e |grep 10GbE

  3   6891D067138C    94:00.0 10GbE   N/A UEFI,PXE Enabled              2.4.45
  4   6891D067138D    94:00.1 10GbE   N/A UEFI,PXE Enabled              2.4.45
```

8. 刷入PXE+UEFI设置，根据向导选两次yes即可,因为一块网卡有2个口，输入固件的时候只需要选择其中一个口即可，网口的编号第7步命令可以获取到   
```
  ./bootutil64e -nic=3 -up=pxe+efi -file=BootIMG.FLB
```

9. 刷入固件完成后执行命令，显示为"**UEFI,PXE**" 即为刷如固件成功。   
```
./bootutil64e |grep 10GbE
  3   6891D067138C    94:00.0 10GbE   N/A UEFI,PXE Enabled              2.4.45
  4   6891D067138D    94:00.1 10GbE   N/A UEFI,PXE Enabled              2.4.45
```



