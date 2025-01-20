确认andorid设备的架构
```
adb shell getprop ro.product.cpu.abi
```

检查端口占用
```
netstat -anp | grep 27042
```

检查frida是否启动
```
ps | grep frida
```

结束所有 Frida 相关进程
```
killall frida-server-16.6.2-android-arm64
```

结束占用端口的进程
```
kill -9 <进程ID>
```

重启 frida-server
```
./frida-server-16.6.2-android-arm64 &
```

启动 frida-server 时指定端口
```
./frida-server-16.6.2-android-arm64 -l 127.0.0.1:27043 &
```

使用 Frida 工具连接到自定义端口
```
frida-ps -U --listen=27043
```


获取frida service，并解压
```
https://github.com/frida/frida/releases
```

pycharm 安装 frida-tools 库

解压后的frida service 放到 andorid设备
```
adb push frida-server /data/local/tmp/
```

赋予执行权限
```
adb shell chmod +x /data/local/tmp/frida-server
```

启动 frida-server
```
adb shell /data/local/tmp/frida-server &
```

在pycharm的终端中验证android设备中的 frida-server 是否正常工作
```
frida-ps -U
```

列出设备上正在运行的应用
```
frida-ps -Uai
```

使用以下命令附加到目标应用进程
```
frida -U -n com.example.targetapp

-U 表示连接到 USB 设备，-n 表示按进程名称附加
```

注入指定script.js脚本
```
frida -U -f com.example.frida_demo01 -l script.js
```