# 分辨率相关
adb shell wm size 720x1280 #修改显示分辨率为720P
adb shell wm size reset #恢复默认显示分辨率

# 电池相关

adb shell dumpsys battery #获取电池信息

```
Current Battery Service state:
  AC powered: false　　　　　　　　//false表示没使用AC电源
  USB powered: true　　　　　　　　//true表示使用USB电源
  Wireless powered: false　　　　 //false表示没使用无线电源
  status: 2　　　　　　　　　　　　　//2表示电池正在充电，1表示没充电
  health: 2　　　　　　　　　　　　　//2表示电池状态优秀
  present: true　　　　　　　　　　 //true表示已安装电池
  level: 63　　　　　　　　　　　　　//电池百分比
  scale: 100　　　　　　　　　　　　　//满电量时电池百分比为100%（不确定是否正确）
  voltage: 3781　　　　　　　　　　　//电池电压3.781V
  temperature: 250　　　　　　　　　//电池温度为25摄氏度
  technology: Li-ion　　　　　　　　//电池类型为锂电池
```

adb shell dumpsys battery set status 1 #设置充电状态，1为不充电状态，2为充电状态

adb shell dumpsys battery reset #重置所有的电池设置