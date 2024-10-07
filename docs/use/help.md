## 关于报错 Command not found

!!! quote ""

    === "Debian 系"

        ``` sh
        apt-get install -y curl
        ```

        > `Debian` &nbsp; `Ubuntu` &nbsp; `Kali` &nbsp; `Linux Mint` &nbsp; `Deepin` &nbsp; `Zorin OS` &nbsp; `Armbian` &nbsp; `Proxmox`

        新装系统需要先执行一遍更新 `apt-get update`

    === "RedHat 系 / OpenCloudOS / openEuler"

        ``` sh
        dnf install -y curl || yum install -y curl
        ```

        > `Red Hat Enterprise Linux` &nbsp; `CentOS` &nbsp; `Rocky Linux` &nbsp; `AlmaLinux` &nbsp; `Fedora` &nbsp; `OpenCloudOS` &nbsp; `openEuler`

    === "openSUSE"

        ``` sh
        zypper install curl
        ```

    === "Arch Linux"

        ``` sh
        pacman -S curl
        ```

    === "Alpine Linux"

        ``` sh
        apk --no-cache add -f curl bash
        ```

    === "Gentoo"

        ``` sh
        emerge --ask curl
        ```

## 关于开启 SSH 远程登录的方法

!!! quote ""

    - ### 验证是否已安装 `SSH` 服务

        ``` bash
        ls /etc | grep ssh
        ```
        > 如果没有这个文件夹说明系统未安装 `SSH` 服务，你需要通过包管理工具安装 `openssh` 软件包

    - ### 设置允许 Root 用户登录

        ``` bash
        cat /etc/ssh/sshd_config | grep -Eq "^[# ]?PermitRootLogin " ; [ $? -eq 0 ] && sed -i 's/^[# ]\?PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config || echo -e "\nPermitRootLogin yes" >> /etc/ssh/sshd_config
        ```

    - ### 设置密码认证

        ``` bash
        cat /etc/ssh/sshd_config | grep -Eq "^[# ]?PasswordAuthentication " ; [ $? -eq 0 ] && sed -i 's/^[# ]\?PasswordAuthentication.*/PasswordAuthentication yes/g' /etc/ssh/sshd_config || echo -e "\nPasswordAuthentication yes" >> /etc/ssh/sshd_config
        ```

    - ### 启动/重启 `SSH` 服务

        ``` bash
        ps -ef | grep -q ssh ; [ $? -eq 0 ] && systemctl restart sshd || systemctl enable --now sshd
        ```

    > 命令仅供参考，只适配了部分常见发行版

## 还原已备份的软件源

!!! quote ""

    === "Debian 系"

        ``` sh
        cp -rf /etc/apt/sources.list.bak /etc/apt/sources.list
        apt-get update
        ```

        > `Debian` &nbsp; `Ubuntu` &nbsp; `Kali` &nbsp; `Linux Mint` &nbsp; `Deepin` &nbsp; `Zorin OS` &nbsp; `Armbian` &nbsp; `Proxmox`

    === "RedHat 系 / OpenCloudOS / openEuler"

        ``` sh
        cp -rf /etc/yum.repos.d.bak /etc/yum.repos.d
        yum makecache
        ```

        > `Red Hat Enterprise Linux` &nbsp; `CentOS` &nbsp; `Rocky Linux` &nbsp; `AlmaLinux` &nbsp; `Fedora` &nbsp; `OpenCloudOS` &nbsp; `openEuler`

    === "openSUSE"

        ``` sh
        cp -rf /etc/zypp/repos.d.bak /etc/zypp/repos.d
        zypper ref
        ```

    === "Arch Linux"

        ``` sh
        cp -rf /etc/pacman.d/mirrorlist.bak /etc/pacman.d/mirrorlist
        pacman -Sy
        ```

    === "Alpine Linux"

        ``` sh
        cp -rf /etc/apk/repositories.bak /etc/apk/repositories
        apk update -f
        ```

    === "Gentoo"

        ``` sh
        cp -rf /etc/portage/make.conf.bak /etc/portage/make.conf
        [ -d /etc/portage/repos.conf ] && cp -rf /etc/portage/repos.conf/gentoo.conf.bak /etc/portage/repos.conf/gentoo.conf
        emerge --sync --quiet
        ```

## 其它

!!! quote ""

    - 如果提示 `bash: /proc/self/fd/11: No such file or directory`，请切换至 `Root` 用户执行，切换命令为 `sudo -i` 或 `su root`
