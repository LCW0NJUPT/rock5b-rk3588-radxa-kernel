# rock5b-rk3588-radxa-kernel
* 使用armbian编译脚本创建，支持最新版本armbian的Rock5B，使用radxa的vendor内核，支持ISP、GPU和NPU。  
* Created using armbian compilation script, supporting Rock5B of the latest version of armbian, using radxa's vendor kernel, supporting ISP, GPU and NPU.

## 将文件传输到 Rock5B
```bash
unzip rock5b-kernel-debs.zip

scp *.deb User@rock-5b:/home/User/
```

## 在 Rock5B 上安装
```bash
# 进入文件目录
cd /home/User/

# 安装内核包
sudo dpkg -i linux-image-*.deb linux-headers-*.deb linux-dtb-*.deb

# 更新 initramfs（自动）
sudo update-initramfs -c -k 6.1.115-vendor-radxa-rockchip-rk3588  

# 更新 bootloader（重要！） 
# 这里一共有三行，我的系统安装在nvme上，选第二项“Install/Update the bootloader on (/dev/nvme0n1)”
sudo armbian-install

# 重启
sudo reboot
```

## 验证安装
```bash
## 重启后执行
uname -a
# 应该显示：Linux rock-5b 6.1.115-vendor-radxa-rockchip-rk3588 ...

dmesg | grep -i imx219
# 应该能看到摄像头识别信息

dmesg | grep -i "mali\|npu\|isp"
# 应该显示GPU/NPU/ISP驱动加载成功
```
## 如果想要切换回原来的环境    
先armbian-config改回来  
再sudo apt remove linux-image-现在的内核版本    


