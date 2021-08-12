https://docs.microsoft.com/zh-tw/windows/wsl/

# 安裝 WSL

在 powershell 中，執行命令 (administrator 權限)

## 啟用 Hyper-V (No need)
```
PS> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

## 啟用 wsl
```
PS> dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

## 啟用 virtual machine
```
PS> dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

## 安裝 wsl 2 Linux 核心套件 (for x64)
於此處 https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi 下載

## 設定 WSL 預設版本
PS> wsl --set-default-version 2

## 安裝 Linux distributions
有三種方式：
1. 於 Windows store 下選擇。

2. 若是無法使用 Windows store，可以透過網頁下載：
   1. Debian - https://www.microsoft.com/store/apps/9MSVKQC78PK6
   2. Fedora Remix - https://www.microsoft.com/store/apps/9n6gdm4k2hnc
   3. uBuntu 20.04 - https://www.microsoft.com/store/apps/9n6svws3rx71

3. 使用命令下載
```
PS> wsl --install -d <distribution name>
```

# Power shell 下 與 WSL 相關命令

## 查看目前 wsl 的狀態
```
PS> wsl --list --verbose
```


## 設定各 Linux 的 wsl 版本
```
PS> wsl --set-version <distribution name> <version>。以下為範例：

PS> wsl --set-version Ubuntu-20.04 1      //    WSL 1 版
PS> wsl --set-version Ubuntu-20.04 2      //    WSL 2 版
```

## wsl 的預設 Linux
```
PS> wsl --setdefault <distribution name>。以下為範例：

PS> wsl --setdefault Ubuntu-20.04
```

## 登入 wsl 時的預設帳號
```
PS> wsl --user <username>
```

## 使用 root 登入 Linux (用來更新密碼)
```
PS> wsl -d <distribution name> -u root
```

## 啟動 Linux distributions
```
PS> wsl -d <distribution name> 啟動某一個 Linux distribution
```
		
## 停止 Linux distributions
```
PS> wsl -t <distribution name> 停止某一個 Linux distribution，或是
PS> wsl --shutdown 停止所有執行中的 Linux distributions
```

# 遷移 WSL 中的 Linux

1. 將原本的 wsl 匯出到備份檔案
```
PS> wsl --export <distribution name> d:\Backup\\<distribution name>.tar
```

2. 移除原本的 wsl
```
PS> wsl --unregister <distribution name>
```

3. 匯入檔案到目標路徑
```
PS> wsl --import <distribution name> d:\workspaces\wsl\\<distribution name> d:\Backup\\<distribution name>.tar
```
遷移後的 Linux 套件使用的虛擬文件檔案 (.vhdx) 的路徑為 d:\workspaces\wsl\\<distribution name> 
											 
可以用同一套 <distribution name>.tar，改用不同的 <distribution name>，可以有多個虛擬環境。譬如說
```
PS> wsl --import ubuntu-MDS d:\workspaces\wsl\ubuntu-MDS d:\Backup\Ubuntu-20.04.tar			<--	MDS 開發環境
PS> wsl --import ubuntu-OpenBMC d:\workspaces\wsl\ubuntu-OpenBMC d:\Backup\Ubuntu-20.04.tar		<--	OpenBMC 開發環境
```

4. 重新指定預設帳號
```
PS> Get-ItemProperty Registry::HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Lxss\*\ DistributionName | \
    Where-Object -Property DistributionName -eq <distribution name> | \
    Set-ItemProperty -Name DefaultUid -Value ((wsl -d <distribution name> -u <USER> -e id -u) | Out-String);
```
	
5. 檢查 WSL 的檔案大小
```
PS> Get-VHD -Path d:\workspaces\wsl\<distribution name>\ext4.vhdx
```
	
6. 修改 WSL 的檔案大小
```
PS> Resize-VHD -Path d:\workspaces\wsl\<distribution name>\ext4.vhdx -SizeBytes 128GB
```

# 其他

## 取得 Linux distributions 的 IP
```
PS> wsl hostname -I
```

## SSH Server 相關
1. 在 WSL 中建立 ssh server 的 key
```
sudo ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
sudo ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
```

2. 在 WSL 中設定 ssh server
修改 /etc/ssh/sshd_config：
   1. PasswordAuthentication yes
   2. Port 50130
   3. X11Forwarding yes
   4. X11DisplyOffset 10
   5. AllowUsers ${USER} (NO need)

3. 重啟 sshd
   1. sudo service ssh --full-restart


## 安裝 AMI MDS

### X Server for Windows 10
尋找並安裝 VcXsrv。啟動之後，記得要在 Extra settings 中，點選 "Disable access control"

### 切換成 bash
```
sudo dpkg-reconfigure dash 
```

### X-11 Forwarding 
修改 ~/.bashrc，加上這兩行：

```
export DISPLAY=$(awk '/nameserver / {print $2; exit}' /etc/resolv.conf 2>/dev/null):0
export LIBGL_ALWAYS_INDIRECT=1
```
		
### 安裝 MDS 相關套件 (MDS 13)
```
sudo apt install -y openjdk-8-jdk subversion patch patchutils bison libc6-dev libxml-dom-perl \
		    zlib1g zlib1g-dev libcurl4-openssl-dev python-numpy doxygen python-apt dmsetup libpcre3-dev python-subversion \
		    netpbm sqlite3 gawk graphviz u-boot-tools automake pkg-config libc6-armel-cross libc6-dev-armel-cross \
		    binutils-arm-linux-gnueabi libncurses5-dev gcc-arm-linux-gnueabi g++-arm-linux-gnueabi flex lzop libssl-dev rename \
		    php-cli squashfs-tools luajit curl cppcheck ssh-askpass libtool git nodejs npm python2.7  \
		    vim global tmux tree 
		
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install -y libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 zlib1g-dev:i386
```
							
### 安裝 node.js 套件
```
sudo npm install -y -g grunt-cli beautifier
```
	
### 安裝 python 套件
1. 下載 pip.py 並執行 pip.py
```
curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py
sudo python get-pip.py
```
			
2. 安裝套件
```
sudo pip install GitPython setuptools configParser sentry_sdk
```
		
### 下載並安裝 MDS
```
git clone https://git.ami.com/tools/mds/releases/13.0.git MDS_13
```
		
