# 常用视图
    用户视图<Huawei>
    系统视图[Huawei]
    接口视图

# 常用指令
    <Huawei> undo terminal monitor    //关闭日志，以获取更好的显示
    <Huawei> sys                      //进入系统视图
    [Huawei] sysname xxx              //更改设备名

# 使用telnet方式登录交换机
    **IPv4**
        1. 配置交换机IP地址和子网掩码
        <sw> sys
        [sw] int vlanif 1
        [sw-vlanif1] ip add x.x.x.x xx
        2. 配置用户远程登录（模式）口令和权限
        2.1 使能服务器功能
        <sw> sys
        [sw] telnet server enable
        [sw] telnet server-source-i vlanif 1
        2.2 配置VTY用户界面的支持协议类型
        [sw] user-int vty 0 4
        [sw-ui-vty0-4] protocol inbound telnet      
            //指定VTY用户界面所支持的协议为telnet
        2.3 配置VTY用户界面的认证方式为password
        [sw-ui-vty0-4] authentication-mode password
        [sw-ui-vty0-4] set authentication password simple xxx      
        [sw-ui-vty0-4] user privilege level 15

        // ensp中PC机不支持Telnet功能，因此使用交换机代替PC机进行实验
        配置“PC机”IP地址
        <pc> sys
        [pc] int vlanif 1
        [pc-vlanif1] ip add x.x.x.x xx  //与交换机配置在同一网段
        在用户视图下执行telnet命令
        <pc> telnet x.x.x.x
        按照提示输入密码
    **IPv6**
        <sw>sys
        [sw]ipv6                        //全局使能ipv6
        [sw]int Vlanif 1
        [sw-Vlanif1]ipv6 enable         //vlanif视图下使能ipv6
        [sw-Vlanif1]ipv6 add ...
        [sw-Vlanif1]quit
        [sw]user-int vty 0 4
        [sw-ui-vty0-4]authentication-mode password 
        [sw-ui-vty0-4]set authentication password simple ...
        [sw-ui-vty0-4]user privilege level 15

        <pc>sys
        [pc]ipv6
        [pc]int Vlanif 1
        [pc-Vlanif1]ipv6 enable 
        [pc-Vlanif1]ipv6 address ...    //与交换机同一网段
        [pc-Vlanif1]return
        <pc>telnet ipv6 ...             //telnet命令后必须标明使用ipv6
        
        