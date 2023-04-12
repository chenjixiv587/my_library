_网络学习工具之 Cisco Packet Tracer;
Start from 2023-02-17_

**查看都在超级权限，更改都在 全局配置下。**

进入超级权限

- `enable`

进入全局配置模式

- `enable`
- `configure terminal`

---

在超级权限下(主要用于查看)

- 查看当前的配置 `show run-config`
- 查看启动时的配置文件 `show start-config`
- 将配置存储 `write`
  - 默认情况下 就是将 `run-config` 复制到 `start-config`
- 将配置复制 `copy x y` 把 `x` 拷贝到 `y`
- 展示闪存盘 `show flash:`

---

进入全局配置模式之后，再去配置（主要用于配置）

**切记，在做完配置后，一定要去超级权限下，write**

- 更改名称 `hostname changed_name`
- 进入端口 `interface 端口`
  - 端口描述 `description xxxxx`
  - 更改名称、端口描述是为了以后更好的维护

常规按键

- 空格键 翻页
- 打错命令，无法控制时，使用 `ctrl+shift+6`来停止

密码配置的几种情况

- 特权模式下
  - `enable`
    - 进入全局配置模式下 `configure terminal`
      - 密文 `enable secret` （主要设置这种 YES） 给进入 `enable` 模式进行设置密码
      - 明文 `enable password` (NO)
- `console` 口

  - `enable`

    - `configure terminal`
      - `enable secret xxxx`

      - `line console 0`

        - `password xxx`

        - 设置本地用户名 密码

          - `login local` 在返回全局配置模式
          - `username xx password xxx`

- `telnet`
  - 设备的 `IP` 用 `VLAN1` 来代表
  - `line vty 0 15`
  - `login local`
  - `username xx password xx`
  - `int vlan 1`
  - `ip address 192.168.2.254 255.255.255.0`

[cisco 交换机配置 ssh 远程登陆](https://my.oschina.net/xinsui1314x/blog/3078047)